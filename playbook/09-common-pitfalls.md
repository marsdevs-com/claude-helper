# 09 — Common Pitfalls
> Part of the [Claude Code Team Playbook](../README.md) by [MarsDevs](https://www.marsdevs.com)

Patterns that waste time and how to fix them.

## 1. Over-Correcting

**Symptom**: Claude makes a mistake. You over-specify the correction. Claude over-compensates. You correct again. Spiral continues.

**Fix**: After 2 failed attempts, `/clear` and write a better prompt from scratch. It's faster than course-correcting in polluted context.

## 2. Infinite Exploration

**Symptom**: You ask Claude to "look at the codebase" without a specific question. It reads 30 files, burns through your context window, and gives a vague summary.

**Fix**: Always give a focused question or a specific starting file.

```
# Bad
"Explore the codebase and understand the architecture"

# Good
"Read @src/auth/middleware.ts and explain the token validation flow"
```

If you genuinely need broad exploration, delegate to a subagent so your main context stays clean.

## 3. Trust Without Verification

**Symptom**: You accept Claude's output, ship it, and it breaks in production because nobody ran the tests.

**Fix**: Always verify. Include it in your prompt:

```
"...and run the tests after making changes"
"...verify by calling the endpoint with curl"
"...check that the types compile with npm run typecheck"
```

Verification is the highest-leverage thing you can do. It catches 90% of mistakes before they matter.

## 4. Over-Specified CLAUDE.md

**Symptom**: Your CLAUDE.md is 400+ lines. Claude ignores half the rules or follows contradictory ones. New team members don't know which rules matter.

**Fix**:
- Keep CLAUDE.md under 200 lines
- Move file-specific rules to `.claude/rules/` with glob patterns
- Use `@imports` for external documentation
- Delete rules that duplicate your linter/formatter config

## 5. Kitchen-Sink Sessions

**Symptom**: You ask Claude to fix a bug, then refactor a module, then write docs, then update tests — all in one session. By the fourth task, Claude is referencing stale context from the first task.

**Fix**: One logical task per session. `/clear` between tasks.

## 6. Skipping Plan Mode for Big Changes

**Symptom**: Claude charges ahead implementing a large feature and makes architectural decisions you disagree with. Rework costs more than the original implementation.

**Fix**: Use plan mode first for any change touching more than 2-3 files. Review the plan. Push back. Then implement.

## 7. Ignoring the Diff

**Symptom**: You approve every file change without reading it. Claude introduces a subtle bug — wrong variable name, off-by-one error, or an accidental behavior change.

**Fix**: Read the diffs. Especially watch for:
- Changes to files you didn't ask Claude to touch
- Deleted code (was it intentional?)
- New dependencies or imports
- Changes to error handling or edge cases

## Quick Decision Tree

```
Claude made a mistake?
├── First attempt → correct and continue
├── Second attempt → be more specific about what's wrong
└── Third attempt → /clear and rewrite the prompt

Task is complex?
├── Yes → Plan mode first, then implement
└── No → Go straight to implementation

Need to understand code?
├── Focused question → ask directly
└── Broad exploration → use a subagent

Done implementing?
└── ALWAYS → run tests / verify output
```
