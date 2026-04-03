# <!-- TODO: Project Name -->

<!-- Full-stack project template by MarsDevs (www.marsdevs.com) -->

## Tech Stack

<!-- TODO: Fill in your actual stack -->

- **Frontend**: <!-- e.g., React, Vue, Svelte, Angular -->
- **Backend**: <!-- e.g., Node/Express, FastAPI, Go, Rails -->
- **Database**: <!-- e.g., PostgreSQL, MongoDB, MySQL -->
- **Cache**: <!-- e.g., Redis, Memcached -->
- **Queue**: <!-- e.g., RabbitMQ, SQS, BullMQ -->
- **Infrastructure**: <!-- e.g., AWS, GCP, Azure, Docker, K8s -->
- **CI/CD**: <!-- e.g., GitHub Actions, GitLab CI, CircleCI -->
- **Monitoring**: <!-- e.g., Datadog, Grafana, Sentry -->

## Architecture

```
frontend/           # Client application
backend/            # API server
  api/              # Route handlers / controllers
  services/         # Business logic
  repositories/     # Data access layer
  models/           # Domain models / schemas
  middleware/        # Request middleware
  config/           # Configuration
shared/             # Shared types, utilities, constants
infra/              # Docker, K8s, Terraform, CI/CD configs
scripts/            # Build, deploy, seed, migration scripts
tests/              # Test suites (unit, integration, e2e)
docs/               # Documentation
```

<!-- TODO: Adjust the directory structure above to match your actual project layout -->

## Key Files

<!-- TODO: Add @file references to your most important files -->

- `@README.md` — project overview and setup instructions
- <!-- @backend/config/settings.py or similar -->
- <!-- @frontend/src/App.tsx or similar -->
- <!-- @infra/docker-compose.yml -->
- <!-- @shared/types/index.ts -->

## Conventions

### API Layer
- Thin handlers: validate input, call service, return response
- Validate at the boundary — never trust incoming data
- Return typed, consistent response shapes
- Consistent error format across all endpoints

### Service Layer
- All business logic lives here, not in handlers or repositories
- Services receive dependencies via injection (not global imports)
- Services do not call other services directly — use an orchestrator or events if coordination is needed

### Data Layer
- Repository pattern: all database access through typed abstractions
- No raw queries in services or handlers
- Migrations are append-only — never edit an applied migration

### Frontend
- Component composition over inheritance
- State management is intentional — document why each piece of state lives where it does
- API client abstraction: one place to change if the API contract changes

### Shared
- Types and constants shared between frontend and backend live in `shared/`
- Never duplicate types across layers — import from the shared source

## Rules

- Never commit `.env`, credentials, or secrets
- Never modify generated files, lock files, or applied migrations
- All new code requires tests
- Dependency direction: handlers -> services -> repositories (never reverse)
- Run tests before considering any task complete
- Run linter and type checker before committing

## Common Commands

<!-- TODO: Fill in your actual commands -->

```bash
# Development
# npm run dev / python manage.py runserver / make dev

# Testing
# npm test / pytest / make test

# Linting
# npm run lint / ruff check . / make lint

# Type checking
# npx tsc --noEmit / mypy . / make typecheck

# Database
# npm run migrate / alembic upgrade head / make migrate

# Build
# npm run build / docker build . / make build

# Deploy
# npm run deploy / make deploy
```

## Agent Workflow

This project includes 17 specialized agents. Use them at the right time:

| Phase | Agent | Command |
|-------|-------|---------|
| **Think** | product-thinker | `/agent:product-thinker "Should we build X?"` |
| **Design** | system-architect | `/agent:system-architect "Design architecture for X"` |
| **Schema** | database-architect | `/agent:database-architect "Design schema for X"` |
| **Build** | devops | `/agent:devops "Set up CI/CD for this project"` |
| **Code** | refactorer | `/agent:refactorer "Clean up module X"` |
| **Debug** | troubleshooter | `/agent:troubleshooter "Why is X failing?"` |
| **Review** | code-reviewer | `/agent:code-reviewer "Review changes in last commit"` |
| **Secure** | security-auditor | `/agent:security-auditor "Audit auth module"` |
| **Perf** | performance-profiler | `/agent:performance-profiler "Why is X slow?"` |
| **Test** | test-engineer | `/agent:test-engineer "Write tests for X"` |
| **E2E** | e2e-designer | `/agent:e2e-designer "Design test scenarios for X"` |
| **Regress** | regression-analyzer | `/agent:regression-analyzer "What could break from these changes?"` |
| **A11y** | accessibility-auditor | `/agent:accessibility-auditor "Audit component X"` |
| **Fixtures** | fixture-builder | `/agent:fixture-builder "Create test data for X"` |
| **Deps** | dependency-manager | `/agent:dependency-manager "Audit our dependencies"` |
| **PR** | pr-writer | `/agent:pr-writer "Write PR description for this branch"` |
| **Docs** | doc-writer | `/agent:doc-writer "Document module X"` |
