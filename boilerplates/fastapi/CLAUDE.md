# Project Name — FastAPI

<!-- Template by MarsDevs (www.marsdevs.com) — customize the TODO sections below -->
<!-- TODO: Replace with your project description -->
Brief description of what this API does.

## Tech Stack

- **Runtime**: Python 3.11+
- **Framework**: FastAPI
- **ORM**: SQLAlchemy 2.0 (async)
- **Migrations**: Alembic
- **Validation**: Pydantic v2
- **Database**: PostgreSQL
- **Testing**: pytest + httpx (async TestClient)
- **Linting**: ruff
- **Type checking**: mypy / pyright

<!-- TODO: Update with your actual stack -->

## Architecture

```
app/
├── main.py              # FastAPI app factory, lifespan, middleware
├── config.py            # Settings via pydantic-settings (env-based)
├── dependencies.py      # Shared FastAPI dependencies (get_db, get_current_user)
├── models/              # SQLAlchemy ORM models
├── schemas/             # Pydantic request/response schemas
├── routers/             # Route handlers grouped by domain
│   ├── users.py
│   ├── auth.py
│   └── ...
├── services/            # Business logic (called by routers, not by each other)
├── repositories/        # Database queries (one per model)
├── middleware/           # Custom middleware
└── utils/               # Shared utilities
tests/
├── conftest.py          # Fixtures: async client, test db, factory functions
├── test_routers/        # Integration tests per router
├── test_services/       # Unit tests per service
└── factories/           # Test data factories
alembic/
├── versions/            # Migration files (never edit by hand after merge)
└── env.py
```

<!-- TODO: Adjust to match your actual layout -->

## Key Files

- @app/main.py — App factory, startup/shutdown, middleware registration
- @app/config.py — All environment variables and settings
- @app/dependencies.py — get_db session, auth dependencies
- @tests/conftest.py — Test fixtures, async client setup
- @alembic/env.py — Migration environment config

<!-- TODO: Add your project's key files -->

## Conventions

### Routing
- One router file per domain (users, auth, orders)
- Use APIRouter with prefix and tags
- Always declare response_model on endpoints
- Use Depends() for all shared logic (auth, db, pagination)
- Return Pydantic schemas, never raw ORM models

### Models & Schemas
- ORM models in `models/`, Pydantic schemas in `schemas/`
- Schemas are split: `UserCreate`, `UserUpdate`, `UserResponse`
- Use `model_config = ConfigDict(from_attributes=True)` on response schemas
- All IDs are UUID, all timestamps are UTC datetime

### Services
- Business logic lives in `services/`, not in route handlers
- Services receive repository instances via DI, not raw sessions
- Services raise domain exceptions, routers catch and return HTTP errors

### Error Handling
- Use custom exception classes in `app/exceptions.py`
- Register exception handlers in main.py, not in individual routes
- Return consistent error shape: `{"detail": "message", "code": "ERROR_CODE"}`

### Async
- All database operations are async (use `AsyncSession`)
- Use `async for` for streaming queries
- Never use `time.sleep()` — use `asyncio.sleep()` if needed

## Rules

- Never import from `routers/` into `services/` (dependency flows one way)
- Never return ORM model instances from route handlers
- Never modify migration files after they've been merged to main
- Never commit .env files or secrets
- Never add `# type: ignore` without an explanation comment
- Do not mention AI tools in commit messages
- Run `pytest` before considering any task complete
- Run `ruff check` and `ruff format` before committing

## Common Commands

```bash
# Development server
uvicorn app.main:app --reload --port 8000

# Run all tests
pytest -v

# Run specific test file
pytest tests/test_routers/test_users.py -v

# Run with coverage
pytest --cov=app --cov-report=term-missing

# Lint and format
ruff check .
ruff format .

# Type check
mypy app/

# Create migration
alembic revision --autogenerate -m "description"

# Apply migrations
alembic upgrade head

# Rollback one migration
alembic downgrade -1
```

## API Documentation

- Swagger UI: http://localhost:8000/docs
- ReDoc: http://localhost:8000/redoc
- OpenAPI JSON: http://localhost:8000/openapi.json

## Claude Best Practices for This Project

- Always read existing router/service/schema before creating new ones — follow the same patterns
- Use @app/dependencies.py for any new shared dependency
- When adding an endpoint, also add the Pydantic schemas and tests in the same task
- When fixing a bug, reproduce it with a test first, then fix
- Use `httpx.AsyncClient` in tests, not the sync `TestClient`
- After any model change, always create an Alembic migration
