---
globs: ["**/*"]
description: "Commit message standards for FastAPI projects"
---

# Commit Standards

- Use conventional commit format: `type(scope): description`
- Types: `feat`, `fix`, `refactor`, `test`, `docs`, `chore`, `style`, `perf`
- Scopes: `api`, `auth`, `db`, `models`, `schemas`, `tests`, `config`, `deps`
- Keep the subject line under 72 characters
- Use imperative mood: "add endpoint" not "added endpoint"
- Do not mention AI tools or Claude in commit messages
- Reference ticket numbers: `feat(api): add order export endpoint [PROJ-123]`
- Body should explain **why**, not what

## Examples

```
feat(api): add user profile photo upload

Support JPEG/PNG up to 5MB, stored in S3 with CloudFront CDN.
Existing avatar URLs remain valid during migration.

Refs: PROJ-456
```

```
fix(auth): handle expired refresh tokens gracefully

Previously returned 500 when refresh token was expired. Now returns
401 with clear error code so the client can redirect to login.
```

```
refactor(db): switch user queries to repository pattern

Moves raw SQLAlchemy queries out of route handlers into
UserRepository. No behavior change — existing tests pass.
```
