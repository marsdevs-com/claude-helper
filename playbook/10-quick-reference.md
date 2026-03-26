# 10 — Quick Reference
> Part of the [Claude Code Team Playbook](../README.md) by [MarsDevs](https://www.marsdevs.com)

## Keyboard Shortcuts

| Shortcut | Action |
|----------|--------|
| `Esc` | Stop Claude mid-action |
| `Esc` x2 | Open rewind menu |
| `Shift+Tab` | Cycle permission modes |
| `Ctrl+G` | Open plan in editor |
| `Option+T` | Toggle extended thinking |
| `Tab` | Accept suggestion |

## Session Commands

| Command | Action |
|---------|--------|
| `/clear` | Wipe conversation, start fresh |
| `/compact` | Summarize conversation to free context |
| `/rewind` | Undo last turn (code + conversation) |
| `/resume` | List and resume past sessions |
| `/init` | Generate CLAUDE.md from your codebase |
| `/help` | Show help |
| `!command` | Run a shell command without leaving Claude |

## CLI Flags

| Flag | Action |
|------|--------|
| `--continue` / `-c` | Resume most recent session |
| `-n "name"` | Name your session |
| `--worktree name` | Isolated git worktree session |
| `--auto` | Full autonomy mode |
| `--plan` | Read-only plan mode |

## File References

| Syntax | Example |
|--------|---------|
| `@file` | `@src/auth/middleware.ts` |
| `@directory/` | `@src/auth/` |
| `@url` | `@https://docs.example.com/api` |

## Permission Modes

| Mode | Edits | Commands | Shortcut |
|------|-------|----------|----------|
| default | Ask | Ask | — |
| acceptEdits | Auto | Ask | Shift+Tab |
| plan | Blocked | Blocked | Shift+Tab |
| auto | Auto | Auto | Shift+Tab |

## Project Files

| File | Committed | Purpose |
|------|-----------|---------|
| `CLAUDE.md` | Yes | Shared team instructions |
| `~/.claude/CLAUDE.md` | No | Personal preferences |
| `.claude/settings.json` | Yes | Shared hooks & permissions |
| `.claude/settings.local.json` | No | Personal permissions |
| `.claude/rules/*.md` | Yes | File-specific rules |
| `.claude/agents/*.md` | Yes | Custom agent definitions |

## Prompting Patterns

```bash
# Point to specific files
"Fix the bug in @src/api/handler.ts:42"

# Reference a pattern
"Follow the pattern in @src/routes/users.ts"

# Include verification
"...and run npm test after making changes"

# Scope the change
"Only modify files in src/auth/"

# State constraints
"Do not add new dependencies"

# Describe symptoms
"The API returns 500 after ~100 concurrent requests"
```

## Workflow Cheat Sheet

```
New task?          → /clear first
Complex task?      → Plan mode → Explore → Plan → Implement → Verify
Quick fix?         → Just do it + verify
Need to research?  → Subagent (keeps main context clean)
Stuck after 2 tries? → /clear and rewrite prompt
Done?              → Always verify (tests, curl, typecheck)
```
