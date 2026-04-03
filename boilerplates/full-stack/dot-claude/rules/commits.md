---
globs: ["**/*"]
description: "Conventional commit message standards for full-stack projects"
---

## Format

```
<type>(<scope>): <description>

[optional body — explain WHY, not what]

[optional footer — ticket references]
```

## Types

- `feat` — new feature
- `fix` — bug fix
- `refactor` — code restructuring, no behavior change
- `test` — adding or updating tests
- `docs` — documentation only
- `chore` — maintenance, dependencies, tooling
- `style` — formatting, whitespace, no code change
- `perf` — performance improvement
- `ci` — CI/CD changes
- `infra` — infrastructure, Docker, K8s, Terraform

## Scopes

`api`, `ui`, `auth`, `db`, `infra`, `ci`, `config`, `shared`, `tests`, `docs`

<!-- TODO: Add project-specific scopes -->

## Rules

- Imperative mood: "add feature" not "added feature"
- Under 72 characters for the subject line
- Body explains WHY the change was made, not what changed (the diff shows that)
- Reference ticket numbers in the footer: `Closes #123`
