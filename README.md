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

### Full-Stack (Framework-Agnostic)

```bash
cp boilerplates/full-stack/CLAUDE.md your-project/CLAUDE.md
cp -r boilerplates/full-stack/dot-claude your-project/.claude
cat boilerplates/full-stack/dot-gitignore-claude >> your-project/.gitignore
```

Includes: 17 specialized agents (architect, reviewer, devops, test engineer, refactorer, security auditor, product thinker, doc writer, troubleshooter, database architect, performance profiler, dependency manager, PR writer, E2E designer, regression analyzer, accessibility auditor, fixture builder), architecture rules, security rules, secrets-blocking hooks, multi-language formatter hooks.

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

### Full-Stack (Framework-Agnostic)

| File | Purpose |
|------|---------|
| [CLAUDE.md](boilerplates/full-stack/CLAUDE.md) | Full-stack project template with layered architecture and agent workflow |
| [dot-claude/settings.json](boilerplates/full-stack/dot-claude/settings.json) | Multi-language hooks, secrets blocking, broad permissions |
| [dot-claude/rules/architecture.md](boilerplates/full-stack/dot-claude/rules/architecture.md) | Clean architecture, dependency direction, layer boundaries |
| [dot-claude/rules/security.md](boilerplates/full-stack/dot-claude/rules/security.md) | Security hygiene: no secrets, validate input, parameterize queries |
| [dot-claude/rules/code-review.md](boilerplates/full-stack/dot-claude/rules/code-review.md) | Review checklist with architecture and security checks |
| [dot-claude/rules/testing.md](boilerplates/full-stack/dot-claude/rules/testing.md) | Framework-agnostic testing standards |
| [dot-claude/rules/commits.md](boilerplates/full-stack/dot-claude/rules/commits.md) | Conventional commits with full-stack scopes |
| [dot-claude/agents/](boilerplates/full-stack/dot-claude/agents/) | 17 agents: system-architect, code-reviewer, devops, test-engineer, refactorer, security-auditor, product-thinker, doc-writer, troubleshooter, database-architect, performance-profiler, dependency-manager, pr-writer, e2e-designer, regression-analyzer, accessibility-auditor, fixture-builder |
| [dot-gitignore-claude](boilerplates/full-stack/dot-gitignore-claude) | Full-stack .gitignore (JS + Python + infra + Claude) |

## Using Agents

After copying a boilerplate into your project, invoke any agent with `/agent:<name>`:

```bash
# Think before building
/agent:product-thinker "Should we add a notifications system or can we solve this with email?"

# Design the architecture
/agent:system-architect "Design the architecture for a real-time notifications system with trade-offs"

# Design the database schema
/agent:database-architect "Design schema for notifications — user preferences, delivery channels, read status"

# Write the code, then get it reviewed
/agent:code-reviewer "Review the changes in the last commit"

# Debug a failing feature
/agent:troubleshooter "NotificationService.send() throws 'channel not found' — here's the stack trace: ..."

# Security check before launch
/agent:security-auditor "Audit the notifications module — especially the webhook endpoint"

# Find performance issues
/agent:performance-profiler "The notifications list endpoint is slow with 1000+ notifications"

# Write tests
/agent:test-engineer "Write tests for NotificationService covering all delivery channels"

# Design E2E scenarios (for QA)
/agent:e2e-designer "Design E2E test scenarios for the notification preferences page"

# Check what could break
/agent:regression-analyzer "We changed the notification delivery logic — what else could be affected?"

# Audit accessibility
/agent:accessibility-auditor "Audit the notification bell dropdown and preferences form"

# Create test fixtures
/agent:fixture-builder "Create test data for users with various notification preferences and histories"

# Set up CI/CD
/agent:devops "Add a GitHub Actions workflow for lint, test, build, and deploy"

# Audit dependencies
/agent:dependency-manager "Audit our dependencies for outdated packages and CVEs"

# Write PR description
/agent:pr-writer "Write PR description for this branch"

# Clean up messy code
/agent:refactorer "Simplify the notification routing logic in src/services/notifications/"

# Write docs
/agent:doc-writer "Document the notifications module — API endpoints and webhook integration"
```

You can also spawn multiple agents in parallel for independent tasks. See [Chapter 06 — Subagents](playbook/06-subagents.md) for details.

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
