# 06 — Subagents
> Part of the [Claude Code Team Playbook](../README.md) by [MarsDevs](https://www.marsdevs.com)

Subagents are isolated Claude Code instances spawned from your main session. They get their own context window, do focused work, and return a summary — keeping your main session clean.

## Why Use Subagents

1. **Context isolation** — research doesn't pollute your working context
2. **Parallel processing** — multiple independent tasks run simultaneously
3. **Specialization** — custom agents with specific tools and instructions

## Built-in Subagent Spawning

Claude Code can spawn subagents automatically. You can also request it explicitly:

```
"Use a subagent to find all the places we handle authentication
tokens across the codebase."

"Spawn subagents to review these three modules in parallel:
- @src/auth/
- @src/payments/
- @src/notifications/"
```

The main session receives a summary, not the raw exploration. Your context stays focused.

## Custom Agents

Define specialized agents in `.claude/agents/`:

```
.claude/agents/
├── researcher.md      # Read-only exploration
├── reviewer.md        # Code review
└── refactorer.md      # Refactoring specialist
```

### Agent File Anatomy

```markdown
---
name: researcher
description: "Read-only codebase exploration agent"
tools:
  - Read
  - Glob
  - Grep
  - Bash
---

You are a research specialist. Only read, never modify.

## Rules
- Never modify files
- Provide file paths and line numbers
- Quote exact code when relevant

## Output Format
1. Answer
2. Evidence (file:line references)
3. Related files
```

**Frontmatter fields:**
- `name` — identifier used to invoke the agent
- `description` — shown when listing agents
- `tools` — which tools the agent can use (restricts capabilities)

**Body** — the agent's system prompt. Define its role, rules, and output format.

## Running Custom Agents

```
> /agent:researcher "How does the caching layer work?"
> /agent:reviewer "Review the changes in the last commit"
> /agent:refactorer "Simplify the error handling in @src/api/handlers.ts"
```

## Practical Use Cases

| Use Case | Agent | Why |
|----------|-------|-----|
| Understand unfamiliar code | researcher | Explores without risk, clean summary |
| Pre-merge review | reviewer | Consistent checklist, doesn't modify |
| Clean up after feature work | refactorer | Focused scope, runs tests before/after |
| Investigate a bug | researcher | Searches broadly without cluttering main context |
| Parallel module reviews | reviewer (x3) | Review 3 modules simultaneously |

## Tips

- Keep agent system prompts focused — one role per agent
- Read-only agents (researcher, reviewer) should not have Write/Edit tools
- Test your agents on a known task before relying on them
- Agents inherit your CLAUDE.md and rule files — no need to duplicate rules

See `boilerplates/dot-claude/agents/` for ready-to-use agent definitions.
