---
globs: ["**/*"]
description: "Clean architecture and dependency rules for full-stack projects"
---

## Dependency Direction

handlers/controllers -> services -> repositories/data-access

Never reverse this. A repository must never call a service. A service must never call a handler.

## Layer Responsibilities

- **Handlers/Controllers**: Parse input, validate request shape, call service, format response. No business logic.
- **Services**: All business logic. Receive dependencies via injection. Return domain objects, not HTTP responses.
- **Repositories**: Database access only. Accept and return typed models. No business decisions.

## Boundaries

- Services do not call other services directly. If coordination is needed, create an orchestrator service or use events.
- Each layer has its own types: DTOs at the API boundary, domain models in services, entities at the data layer.
- Shared types between frontend and backend live in `shared/` — never duplicate types across layers.
- No circular dependencies between modules.
- One domain concept per module directory.

## When Adding New Code

- New endpoint? Create handler + service + repository + types + tests as a unit.
- New frontend feature? Create component + API call + types + tests as a unit.
- Reuse existing abstractions before creating new ones.
