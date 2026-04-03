---
globs: ["**/*"]
description: "Code review checklist and standards for full-stack projects"
---

## Review Checklist

### Correctness
- Does the code do what the description claims?
- Are all code paths reachable and tested?
- Edge cases: null, empty, zero, negative, boundary values handled?
- Error handling: errors caught, logged, and surfaced meaningfully?

### Architecture
- Does the change respect layer boundaries (handler -> service -> repo)?
- Is business logic in the service layer, not in handlers or UI?
- Are new dependencies justified? Could an existing abstraction be reused?

### Security
- No hardcoded secrets or credentials
- Input validated at system boundaries
- Auth checked on state-changing endpoints
- Sensitive data excluded from logs and responses

### Performance
- No N+1 queries or unbounded loops
- No unnecessary re-renders or recomputation
- Large payloads use pagination or streaming

### Readability
- Clear naming — intent obvious without reading the implementation
- Reasonable function length (under 40 lines)
- Nesting depth under 3 levels

### Tests
- New code paths covered by tests
- Edge cases and error paths tested
- Tests are independent — no ordering dependency

## Severity Levels

- **[CRITICAL]** — Must fix before merge. Bugs, security holes, data loss risk.
- **[WARNING]** — Should fix. Design issues, performance concerns, missing coverage.
- **[NIT]** — Optional. Style, naming, minor improvements.
