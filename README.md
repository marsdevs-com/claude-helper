# Claude Code Team Playbook

**By [MarsDevs](https://www.marsdevs.com)** — Your partner in building better software, faster.

A practical playbook and reusable boilerplates for teams using Claude Code. Read the playbook to level up your workflow, copy the boilerplates into your projects to get started fast.

## Quick Start

Pick the boilerplate that matches your stack:

### Generic (any project)

```bash
cp boilerplates/CLAUDE.md your-project/CLAUDE.md
cp -r boilerplates/dot-claude your-project/.claude
cat boilerplates/dot-gitignore-claude >> your-project/.gitignore
```

### FastAPI (Python)

```bash
cp boilerplates/fastapi/CLAUDE.md your-project/CLAUDE.md
cp -r boilerplates/fastapi/dot-claude your-project/.claude
cat boilerplates/fastapi/dot-gitignore-claude >> your-project/.gitignore
```

Includes: ruff auto-format hooks, pytest permissions, API route rules, SQLAlchemy/Pydantic patterns, Alembic migration guards, async testing standards.

### Next.js (TypeScript)

```bash
cp boilerplates/nextjs/CLAUDE.md your-project/CLAUDE.md
cp -r boilerplates/nextjs/dot-claude your-project/.claude
cat boilerplates/nextjs/dot-gitignore-claude >> your-project/.gitignore
```

Includes: Prettier + ESLint auto-format hooks, Server vs Client component rules, App Router patterns, Server Actions with Zod validation, Vitest + RTL testing standards, Prisma migration guards.

Then customize every `<!-- TODO -->` marker in the copied files.

---

## Playbook

| # | Chapter | What you'll learn |
|---|---------|-------------------|
| 01 | [CLAUDE.md Setup](playbook/01-claude-md-setup.md) | Write effective instructions, use rules and imports |
| 02 | [Context Management](playbook/02-context-management.md) | /clear, /compact, /rewind — your most important habits |
| 03 | [Explore, Plan, Implement, Verify](playbook/03-explore-plan-implement.md) | The core workflow for non-trivial changes |
| 04 | [Effective Prompting](playbook/04-effective-prompting.md) | @file references, verification criteria, scoping |
| 05 | [Permission Modes](playbook/05-permission-modes.md) | default, acceptEdits, plan, auto — when to use each |
| 06 | [Subagents](playbook/06-subagents.md) | Custom agents, parallel processing, context isolation |
| 07 | [Hooks and Automation](playbook/07-hooks-and-automation.md) | Auto-format, protected files, notifications |
| 08 | [Session Management](playbook/08-session-management.md) | Named sessions, --continue, worktrees |
| 09 | [Common Pitfalls](playbook/09-common-pitfalls.md) | Anti-patterns and how to avoid them |
| 10 | [Quick Reference](playbook/10-quick-reference.md) | Shortcuts, commands, and patterns cheat sheet |

## Boilerplates

### Generic (any project)

| File | Purpose |
|------|---------|
| [CLAUDE.md](boilerplates/CLAUDE.md) | Starter template for project instructions |
| [dot-claude/settings.json](boilerplates/dot-claude/settings.json) | Hooks: auto-format, protected files, permissions |
| [dot-claude/rules/](boilerplates/dot-claude/rules/) | Rules for testing, code review, commits |
| [dot-claude/agents/](boilerplates/dot-claude/agents/) | Agents: researcher, reviewer, refactorer |
| [dot-gitignore-claude](boilerplates/dot-gitignore-claude) | .gitignore entries for .claude/ directory |

### FastAPI (Python)

| File | Purpose |
|------|---------|
| [CLAUDE.md](boilerplates/fastapi/CLAUDE.md) | FastAPI project template with async patterns |
| [dot-claude/settings.json](boilerplates/fastapi/dot-claude/settings.json) | Ruff auto-format, migration guards, pytest permissions |
| [dot-claude/rules/api-routes.md](boilerplates/fastapi/dot-claude/rules/api-routes.md) | Route handler patterns, dependency injection, error handling |
| [dot-claude/rules/models-schemas.md](boilerplates/fastapi/dot-claude/rules/models-schemas.md) | SQLAlchemy 2.0 models + Pydantic v2 schema conventions |
| [dot-claude/rules/database.md](boilerplates/fastapi/dot-claude/rules/database.md) | Repository pattern, async queries, Alembic migrations |
| [dot-claude/rules/testing.md](boilerplates/fastapi/dot-claude/rules/testing.md) | Async pytest with httpx, fixtures, factory patterns |
| [dot-claude/agents/](boilerplates/fastapi/dot-claude/agents/) | Agents: api-designer, test-writer, researcher |
| [dot-gitignore-claude](boilerplates/fastapi/dot-gitignore-claude) | Python + Claude .gitignore |

### Next.js (TypeScript)

| File | Purpose |
|------|---------|
| [CLAUDE.md](boilerplates/nextjs/CLAUDE.md) | Next.js App Router template with RSC patterns |
| [dot-claude/settings.json](boilerplates/nextjs/dot-claude/settings.json) | Prettier + ESLint hooks, lock file guards, pnpm permissions |
| [dot-claude/rules/components.md](boilerplates/nextjs/dot-claude/rules/components.md) | Server vs Client components, props, composition patterns |
| [dot-claude/rules/api-routes.md](boilerplates/nextjs/dot-claude/rules/api-routes.md) | Route handlers, Server Actions, Zod validation |
| [dot-claude/rules/testing.md](boilerplates/nextjs/dot-claude/rules/testing.md) | Vitest + React Testing Library + Playwright patterns |
| [dot-claude/agents/](boilerplates/nextjs/dot-claude/agents/) | Agents: component-builder, reviewer, researcher |
| [dot-gitignore-claude](boilerplates/nextjs/dot-gitignore-claude) | Next.js + Claude .gitignore |

## How to Use

**New to Claude Code?** Read the playbook chapters 01-05 in order. They cover the fundamentals.

**Already comfortable?** Jump to chapters 06-07 (subagents and hooks) for advanced techniques.

**Setting up a new project?** Follow the Quick Start above, then customize the TODO markers.

**Need a cheat sheet?** Go straight to [Quick Reference](playbook/10-quick-reference.md).

## TL;DR — The 3 Biggest Wins

1. **Verify everything** — always include "run the tests" in your prompts
2. **Manage context** — `/clear` between tasks, use subagents for research
3. **Plan before you code** — use plan mode for anything non-trivial

---

Built with care by [MarsDevs](https://www.marsdevs.com) — We help teams ship great software with modern tools and best practices.
