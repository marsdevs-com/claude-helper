# 08 — Session Management
> Part of the [Claude Code Team Playbook](../README.md) by [MarsDevs](https://www.marsdevs.com)

Claude Code sessions persist your conversation history. Managing them well lets you pick up where you left off and run parallel workstreams.

## Core Commands

### Continue Last Session

```bash
claude --continue
# or
claude -c
```

Resumes your most recent session with full conversation history. Use when you step away and come back to the same task.

### Name Your Sessions

```bash
claude -n "auth-refactor"
claude -n "PROJ-123-fix-login"
```

Named sessions are easy to find later. Convention: use ticket numbers or descriptive slugs.

### Resume Any Session

```
/resume
```

Lists your recent sessions interactively — pick one to continue.

### Jump to a Specific Named Session

```bash
# Continue a specific named session directly
claude --continue -n "auth-refactor"

# Resume the most recent session with that name
claude -c -n "PROJ-123-fix-login"
```

This lets you jump between named sessions without scrolling through `/resume`. Useful when you're running multiple workstreams:

```bash
# Morning: work on auth
claude -c -n "auth-refactor"
# ... do work, exit ...

# Afternoon: switch to the billing feature
claude -c -n "PROJ-456-billing"
# ... do work, exit ...

# Back to auth with full context preserved
claude -c -n "auth-refactor"
```

**Key point**: each named session retains its full conversation history independently. Jumping between them is like switching browser tabs — you pick up exactly where you left off.

### List Sessions

```bash
# See all recent sessions (names, timestamps, last message preview)
claude sessions list
```

Helpful for finding a session when you forgot the exact name.

### Worktrees for Parallel Work

```bash
claude --worktree feature-auth
```

Creates an isolated git worktree — a separate copy of your repo. Claude works in the worktree without affecting your main checkout. Perfect for:
- Working on two features simultaneously
- Testing a risky approach without touching your branch
- Running a long autonomous task while you keep working

## Session Strategy for Teams

1. **Name by ticket**: `claude -n "PROJ-123-add-sso"` makes sessions searchable
2. **One task per session**: `/clear` between unrelated tasks
3. **Continue, don't restart**: use `-c` to resume rather than re-explaining context
4. **Jump between workstreams**: use `-c -n "name"` to switch contexts instantly
5. **Worktrees for parallel tracks**: don't juggle branches in one session

## When to Start Fresh vs Continue

| Situation | Action |
|-----------|--------|
| Same task, took a break | `claude -c` |
| Jump to a different workstream | `claude -c -n "session-name"` |
| Same task, context is stale | `/compact` then continue |
| New, unrelated task | `/clear` or new `claude` session |
| Parallel feature work | `claude --worktree feature-name` |
| Find an old session | `claude sessions list` or `/resume` |
| Previous session went off-track | New session with clearer prompt |

## Tips

- Sessions auto-save — you don't need to do anything special
- `/clear` within a session starts fresh without leaving the session
- Worktrees are git worktrees under the hood — you can see them with `git worktree list`
- Long-running tasks work well in named sessions: start with `claude -n "migration"`, come back later with `/resume`
