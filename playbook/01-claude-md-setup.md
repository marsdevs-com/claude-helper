# 01 — CLAUDE.md Setup
> Part of the [Claude Code Team Playbook](../README.md) by [MarsDevs](https://www.marsdevs.com)

CLAUDE.md is the file Claude Code reads at the start of every session. It's your team's instructions to the AI — the better it is, the less you repeat yourself.

## The Golden Rule: Under 200 Lines

Long CLAUDE.md files bury important rules in noise. Claude's attention degrades when instructions are too long. Keep it concise.

**If you're over 200 lines, split into `.claude/rules/` files** (covered below).

## Getting Started

Generate a starter from your codebase:

```bash
claude /init
```

This analyzes your project and creates a reasonable starting point. Edit it from there.

Or copy the template from `boilerplates/CLAUDE.md` in this repo.

## Recommended Structure

```markdown
# Project Name
One-line description.

## Tech Stack
## Architecture (directory layout)
## Key Files (@file references)
## Conventions
## Rules (hard constraints)
## Common Commands (build, test, lint, deploy)
```

Each section should be 5-15 lines. If a section needs more, it belongs in a rule file.

## Team vs Personal

| File | Committed? | Scope |
|------|-----------|-------|
| `CLAUDE.md` | Yes | Shared team rules |
| `~/.claude/CLAUDE.md` | No | Your personal preferences |
| `.claude/settings.local.json` | No | Your personal permissions |

Put team conventions in `CLAUDE.md`. Put personal preferences (like "I prefer verbose explanations" or "always use vim keybindings in examples") in your home directory's `~/.claude/CLAUDE.md`.

## Rule Files: `.claude/rules/`

When rules are specific to certain file types, use rule files instead of stuffing them into CLAUDE.md:

```markdown
---
globs: ["**/*.test.*", "**/tests/**"]
description: "Testing standards"
---

- Follow Arrange-Act-Assert pattern
- Each test tests one behavior
- Run tests after writing them
```

Claude automatically loads matching rules based on the files being worked on. This keeps context focused and CLAUDE.md lean.

See `boilerplates/dot-claude/rules/` for ready-to-use examples.

## @Imports

Reference external docs without bloating CLAUDE.md:

```markdown
## API Standards
See @docs/api-conventions.md for our REST API conventions.
```

Claude will read the referenced file when it needs that context.

## Anti-Patterns

- Pasting your entire style guide into CLAUDE.md (use a rule file or @import)
- Contradictory rules ("always add error handling" + "don't add code beyond what's asked")
- Rules that duplicate what's already in linter configs (Claude reads those too)
- Instructions about things Claude already does well by default
