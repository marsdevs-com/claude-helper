# 02 — Context Management
> Part of the [Claude Code Team Playbook](../README.md) by [MarsDevs](https://www.marsdevs.com)

Context is your most valuable resource. Claude Code has a finite context window — stale or irrelevant context degrades output quality. Managing it well is the single biggest lever for better results.

## Core Commands

| Command | What it does | When to use |
|---------|-------------|-------------|
| `/clear` | Wipes conversation, starts fresh | Between unrelated tasks |
| `/compact` | Summarizes conversation, frees space | Mid-task when context is large |
| `/rewind` | Undoes the last turn (code + conversation) | Claude went off-track |

## The #1 Rule: `/clear` Between Tasks

```
Task: Fix login bug          ← /clear
Task: Add export feature     ← /clear
Task: Update API docs        ← /clear
```

New task = new `/clear`. Old context from a different task actively hurts the next one.

## When to `/compact`

You're deep into a task and Claude starts:
- Forgetting decisions made earlier in the conversation
- Repeating work it already did
- Giving less precise responses

Run `/compact`. It summarizes the conversation so Claude remembers key decisions without the noise.

## When to `/rewind`

Claude made a wrong turn — edited the wrong file, went down a rabbit hole, or misunderstood you. Instead of explaining what went wrong:

1. Hit `Esc` twice to open the rewind menu
2. Pick the point before the mistake
3. Rephrase your request more clearly

This is faster and cleaner than course-correcting within a polluted context.

## Subagents for Isolation

When you need to research something without polluting your current context, let Claude spawn a subagent:

> "Explore the auth module and tell me how token refresh works — use a subagent so we don't lose our current context."

The subagent gets its own context window, does its work, and returns a summary. Your main session stays clean.

## Avoid Kitchen-Sink Sessions

**Bad**: "Fix the login bug, then refactor the user module, then update the README, then add the export feature."

**Good**: One logical unit of work per session.

Kitchen-sink sessions lead to:
- Stale context from early tasks interfering with later ones
- Claude losing track of what's done vs what's pending
- Longer time to get anything right

## Practical Checklist

- [ ] Start every new task with `/clear`
- [ ] Use `/compact` when responses start degrading
- [ ] Use `/rewind` instead of explaining mistakes
- [ ] Offload research to subagents
- [ ] One logical task per session
