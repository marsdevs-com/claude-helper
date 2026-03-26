---
globs: ["**/*"]
description: "Commit message standards for Next.js projects"
---

# Commit Standards

- Use conventional commit format: `type(scope): description`
- Types: `feat`, `fix`, `refactor`, `test`, `docs`, `chore`, `style`, `perf`
- Scopes: `ui`, `auth`, `api`, `db`, `forms`, `layout`, `config`, `deps`
- Keep the subject line under 72 characters
- Use imperative mood: "add component" not "added component"
- Do not mention AI tools or Claude in commit messages
- Reference ticket numbers: `feat(ui): add data table with sorting [PROJ-123]`
- Body should explain **why**, not what

## Examples

```
feat(ui): add user profile photo upload with cropping

Support JPEG/PNG up to 5MB with client-side crop preview.
Uses Server Action for upload to avoid client-side S3 credentials.

Refs: PROJ-456
```

```
fix(auth): redirect to login on expired session

Previously showed a blank page when the session cookie expired
mid-navigation. Now catches the auth error in middleware and
redirects to /login with a return URL.
```

```
refactor(forms): extract shared validation into Zod schemas

Moves email, password, and phone validation from inline to
lib/validations/. Reduces duplication across 4 form components.
```
