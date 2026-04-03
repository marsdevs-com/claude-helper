---
globs: ["**/*"]
description: "Security hygiene rules applied to all code changes"
---

## Secrets

- No hardcoded secrets, API keys, tokens, passwords, or connection strings in code
- Secrets come from environment variables or secret managers, never config files
- Never log secrets, tokens, or passwords — even at debug level

## Input Validation

- Validate all input at system boundaries: API handlers, form processors, CLI args
- Never trust data from the client — re-validate on the server
- Parameterize all database queries — no string interpolation or concatenation

## Output

- Escape user content before rendering (prevent XSS)
- Sensitive data (passwords, tokens, PII) excluded from API responses and logs
- Error messages are generic in production — no stack traces, SQL, or file paths exposed

## Authentication & Authorization

- Auth required on all state-changing endpoints by default
- Check authorization (not just authentication) — can this user access this resource?
- Use established libraries for auth — never roll your own encryption or token generation

## Dependencies

- Pin dependency versions — no floating ranges in production
- Commit lockfiles and use them in CI
