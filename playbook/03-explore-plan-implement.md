# 03 — Explore, Plan, Implement, Verify
> Part of the [Claude Code Team Playbook](../README.md) by [MarsDevs](https://www.marsdevs.com)

For any non-trivial change, follow this four-phase workflow. It prevents the most common failure mode: Claude charging ahead with the wrong approach.

## The Four Phases

```
┌──────────┐    ┌──────────┐    ┌─────────────┐    ┌──────────┐
│ Explore  │ →  │   Plan   │ →  │ Implement   │ →  │  Verify  │
│ (read)   │    │ (design) │    │ (write)     │    │ (test)   │
└──────────┘    └──────────┘    └─────────────┘    └──────────┘
```

### Phase 1: Explore

**Goal**: Understand the code before changing it.

Switch to plan mode (Shift+Tab) so Claude can only read, not write.

```
> Look at @src/auth/middleware.ts and explain how token validation works.
> What other files call this middleware?
> Show me the test coverage for auth.
```

Ask Claude to read files, trace code paths, and explain what exists. This prevents it from reinventing something that already exists or breaking something it didn't know about.

### Phase 2: Plan

**Goal**: Agree on an approach before writing code.

```
> Based on what you've seen, how should we add refresh token rotation?
> What files need to change? What's the risk?
```

Review Claude's plan. Push back if something seems off. This is the cheapest place to catch mistakes — changing a plan costs nothing; changing code costs time.

Use Ctrl+G to open and edit the plan directly if needed.

### Phase 3: Implement

**Goal**: Execute the agreed plan.

Switch back to normal mode. Let Claude write code.

```
> Go ahead and implement the plan. Start with the token rotation logic.
```

For trusted changes, use `acceptEdits` mode. For well-scoped, low-risk work with tests, use `auto` mode.

### Phase 4: Verify

**Goal**: Confirm the change works. This is the highest-leverage phase.

```
> Run the tests.
> Try calling the /auth/refresh endpoint with an expired token.
> Check if the old token is invalidated after rotation.
```

**Always verify.** Include verification in your prompt: "...and run the tests after making changes."

## When to Skip Phases

| Change | Skip to |
|--------|---------|
| Typo fix | Implement |
| One-liner bug fix | Implement + Verify |
| New feature | All four phases |
| Large refactor | All four phases (with extra exploration) |

## Example Session

```
You: [Plan mode] Look at @src/payments/stripe.ts — I need to add
     support for subscription pauses. What's the current flow?

Claude: [reads files, explains current implementation]

You: How would you add pause/resume support? Keep it minimal.

Claude: [proposes plan: 2 new functions, 1 modified webhook handler, tests]

You: Looks good, but also handle the case where a paused sub expires.
     Go ahead and implement.

[Switch to normal mode]

Claude: [implements changes]

You: Run the tests and also test with a paused+expired subscription.

Claude: [runs tests, all pass, shows edge case handling]
```
