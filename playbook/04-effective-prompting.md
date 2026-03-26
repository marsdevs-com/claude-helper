# 04 — Effective Prompting
> Part of the [Claude Code Team Playbook](../README.md) by [MarsDevs](https://www.marsdevs.com)

Small changes in how you phrase requests make a large difference in output quality.

## Use @file References

Point Claude at specific files instead of describing them.

```
# Bad
"Fix the authentication bug in the middleware"

# Good
"Fix the token expiry check in @src/auth/middleware.ts — it's not
accounting for clock skew"
```

`@file` tells Claude exactly where to look. No guessing, no reading 20 files to find the right one.

You can also reference directories (`@src/auth/`) and URLs.

## Include Verification Criteria

Tell Claude what success looks like.

```
# Bad
"Add input validation to the signup form"

# Good
"Add input validation to the signup form. Email must be valid format,
password must be 8+ chars with one number. Run the tests after and
make sure the existing tests still pass."
```

Without criteria, Claude decides when it's "done." With criteria, you decide.

## Point to Example Patterns

When your codebase has established patterns, reference them.

```
"Create a new API route for /orders following the same pattern
as @src/routes/users.ts — same error handling, same response format,
same test structure."
```

This produces more consistent code than describing the pattern from scratch.

## Describe Symptoms, Not Assumptions

```
# Bad (assumption)
"The database connection pool is exhausted"

# Good (symptom)
"The API returns 500 errors after ~100 concurrent requests.
Here's the error log: [paste]"
```

Your assumption might be wrong. Give Claude the symptoms and let it diagnose.

## Paste Screenshots

Claude Code can read images. For UI bugs or visual issues:

```
"The login button overlaps the footer on mobile. See this screenshot:"
[paste screenshot]
"Fix the CSS in @src/components/Login.module.css"
```

## Scope Your Requests

```
# Too broad
"Refactor the auth module"

# Scoped
"Extract the token validation logic from @src/auth/middleware.ts
into a separate @src/auth/validate-token.ts file. Only move the
validation — don't change any other behavior."
```

## State Constraints Upfront

```
"Add Redis caching to the user lookup. Constraints:
- Do not add any new npm dependencies (use the existing ioredis client)
- Cache TTL should be configurable via environment variable
- Existing tests must still pass"
```

Constraints prevent Claude from making unwanted architectural decisions.

## Quick Reference

| Instead of | Try |
|-----------|-----|
| "Fix the bug" | "Fix the null pointer in @src/api/handler.ts:42" |
| "Make it faster" | "The query in @src/db/users.ts:15 takes 3s — add an index or optimize" |
| "Add tests" | "Add tests for @src/auth/login.ts covering: valid login, wrong password, locked account" |
| "Clean up the code" | "Extract the repeated validation in @src/routes/*.ts into a shared middleware" |
