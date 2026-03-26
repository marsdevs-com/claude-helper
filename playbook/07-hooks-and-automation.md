# 07 — Hooks and Automation
> Part of the [Claude Code Team Playbook](../README.md) by [MarsDevs](https://www.marsdevs.com)

Hooks are shell commands that run automatically at specific points in Claude Code's lifecycle. They eliminate repetitive manual steps and enforce guardrails.

## Hook Types

| Hook | When it runs | Common use |
|------|-------------|------------|
| `PreToolUse` | Before Claude uses a tool | Block edits to protected files |
| `PostToolUse` | After Claude uses a tool | Auto-format after file edits |
| `Notification` | When Claude wants your attention | Desktop alerts for long tasks |
| `Stop` | When Claude finishes a response | Re-inject context, run checks |

## Configuration

Hooks live in `.claude/settings.json`:

```json
{
  "hooks": {
    "PostToolUse": [
      {
        "matcher": "Write|Edit",
        "hooks": [
          {
            "type": "command",
            "command": "npx prettier --write \"$CLAUDE_FILE_PATH\""
          }
        ]
      }
    ]
  }
}
```

- `matcher` — which tool triggers the hook (regex pattern)
- `command` — shell command to run
- `$CLAUDE_FILE_PATH` — the file Claude just modified (injected by Claude Code)

## Practical Examples

### 1. Auto-Format After Edits

Never see unformatted Claude output again:

```json
{
  "PostToolUse": [
    {
      "matcher": "Write|Edit",
      "hooks": [
        {
          "type": "command",
          "command": "npx prettier --write \"$CLAUDE_FILE_PATH\""
        }
      ]
    }
  ]
}
```

Replace with your formatter: `ruff format`, `gofmt -w`, `rustfmt`, etc.

### 2. Block Edits to Protected Files

Prevent Claude from modifying lock files, generated code, or migrations:

```json
{
  "PreToolUse": [
    {
      "matcher": "Write|Edit",
      "hooks": [
        {
          "type": "command",
          "command": "if echo \"$CLAUDE_FILE_PATH\" | grep -qE '(package-lock\\.json|yarn\\.lock|\\.generated\\.)'; then echo 'BLOCKED: Do not edit generated/lock files'; exit 1; fi"
        }
      ]
    }
  ]
}
```

When the hook exits with code 1, the edit is blocked and Claude sees the error message.

### 3. Auto-Lint After Edits

Run your linter on every file change:

```json
{
  "PostToolUse": [
    {
      "matcher": "Write|Edit",
      "hooks": [
        {
          "type": "command",
          "command": "npx eslint --fix \"$CLAUDE_FILE_PATH\" 2>/dev/null || true"
        }
      ]
    }
  ]
}
```

### 4. Desktop Notification on Completion

Get notified when a long-running task finishes (macOS):

```json
{
  "Stop": [
    {
      "hooks": [
        {
          "type": "command",
          "command": "osascript -e 'display notification \"Claude finished the task\" with title \"Claude Code\"'"
        }
      ]
    }
  ]
}
```

## Tips

- Hooks run locally in your shell — they can do anything your shell can do
- Keep hooks fast — slow hooks delay every tool call
- Use `|| true` at the end of non-critical hooks so failures don't block Claude
- Test hooks manually before adding them to settings
- Combine auto-format + protected-files for a solid baseline setup

See `boilerplates/dot-claude/settings.json` for a starter configuration.
