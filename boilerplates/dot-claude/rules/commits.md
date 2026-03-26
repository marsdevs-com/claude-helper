---
globs: ["**/*"]
description: "Commit message standards and conventions"
---

# Commit Standards

<!-- TODO: Customize for your team -->

- Use conventional commit format: `type(scope): description`
- Types: `feat`, `fix`, `refactor`, `test`, `docs`, `chore`, `style`, `perf`
- Keep the subject line under 72 characters
- Use imperative mood: "add feature" not "added feature"
- Do not mention AI tools or Claude in commit messages
- Reference ticket numbers when applicable: `feat(auth): add SSO login [PROJ-123]`
- Separate subject from body with a blank line
- Body should explain **why**, not what (the diff shows what)

## Examples

```
feat(auth): add JWT refresh token rotation

Tokens were previously single-use with no rotation, leaving a window
for replay attacks after expiry. Rotation closes that gap.

Refs: PROJ-456
```

```
fix(api): handle empty response from payment provider

The provider returns 200 with an empty body when the merchant account
is suspended. Previously this threw an unhandled JSON parse error.
```
