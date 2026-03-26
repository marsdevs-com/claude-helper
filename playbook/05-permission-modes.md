# 05 — Permission Modes
> Part of the [Claude Code Team Playbook](../README.md) by [MarsDevs](https://www.marsdevs.com)

Permission modes control how much autonomy Claude has. Choose the right mode for the situation.

## The Four Modes

| Mode | File Edits | Bash Commands | Best For |
|------|-----------|---------------|----------|
| **default** | Asks permission | Asks permission | Getting started, sensitive work |
| **acceptEdits** | Auto-approved | Asks permission | Iterating on code quickly |
| **plan** | Blocked | Blocked | Exploration and planning |
| **auto** | Auto-approved | Auto-approved | Long-running autonomous tasks |

Cycle through modes with **Shift+Tab** during a session.

## Mode Details

### Default Mode
Every file edit and bash command requires your approval. Safest but slowest. Use when:
- You're new to Claude Code
- Working in sensitive areas (auth, payments, infra)
- You want to review every change

### Accept Edits Mode
Claude writes code freely but asks before running commands. The sweet spot for most development. Use when:
- You're actively developing and want to move fast
- You trust Claude's code changes but want to control what runs
- You're in a well-tested codebase

### Plan Mode
Claude can only read — no writes, no commands. Use when:
- Exploring the codebase before making changes
- Designing an approach for a complex task
- You want Claude to analyze without touching anything

Launch directly: `claude --plan` or switch mid-session with Shift+Tab.

### Auto Mode
Claude runs everything without asking. Use when:
- The task is well-scoped and low-risk
- You have good test coverage as a safety net
- Running long autonomous workflows

Launch directly: `claude --auto`

## Permission Allowlists

Pre-approve common commands so Claude doesn't ask every time:

```json
{
  "permissions": {
    "allow": [
      "Bash(npm test:*)",
      "Bash(npm run lint:*)",
      "Bash(git status:*)",
      "Bash(git diff:*)"
    ]
  }
}
```

Put this in `.claude/settings.json` (shared) or `.claude/settings.local.json` (personal).

The `:*` suffix allows any arguments. Without it, only the exact command is allowed.

## Recommended Progression for Teams

```
Week 1-2:   default mode        → Learn what Claude does, build trust
Week 3-4:   acceptEdits mode    → Speed up, still control commands
Month 2+:   acceptEdits + auto  → acceptEdits for dev, auto for well-tested tasks
Always:     plan mode           → Use for exploration before any big change
```

## Tips

- Start each complex task in plan mode, then switch to acceptEdits for implementation
- Use auto mode sparingly — it's powerful but you lose review opportunities
- Add your test/lint/build commands to the allowlist early — it eliminates the most common permission prompts
