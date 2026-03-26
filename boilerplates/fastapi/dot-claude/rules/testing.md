---
globs: ["**/test_*.py", "**/*_test.py", "**/tests/**/*.py", "**/conftest.py"]
description: "FastAPI testing standards with pytest and httpx"
---

# FastAPI Testing Standards

## Test Structure

```
tests/
├── conftest.py              # Shared fixtures: async client, test db, auth helpers
├── test_routers/            # Integration tests — test the full HTTP request cycle
│   ├── test_users.py
│   └── test_auth.py
├── test_services/           # Unit tests — test business logic in isolation
│   └── test_user_service.py
└── factories/               # Test data factories
    └── user_factory.py
```

## Async Test Pattern

Always use async tests with httpx:

```python
import pytest
from httpx import AsyncClient

@pytest.mark.anyio
async def test_create_user(client: AsyncClient, db_session: AsyncSession):
    response = await client.post("/api/users", json={
        "email": "test@example.com",
        "password": "securepass123"
    })
    assert response.status_code == 201
    data = response.json()
    assert data["email"] == "test@example.com"
    assert "password" not in data  # Never leak passwords in responses
```

## Fixture Pattern

```python
# conftest.py
@pytest.fixture
async def client(app: FastAPI) -> AsyncGenerator[AsyncClient, None]:
    async with AsyncClient(app=app, base_url="http://test") as ac:
        yield ac

@pytest.fixture
async def authenticated_client(client: AsyncClient, test_user: User) -> AsyncClient:
    token = create_access_token(test_user.id)
    client.headers["Authorization"] = f"Bearer {token}"
    return client
```

## Rules

- Use `@pytest.mark.anyio` for all async tests (not `@pytest.mark.asyncio`)
- Use `httpx.AsyncClient` — never use the sync `TestClient` in async projects
- Test the HTTP layer (status codes, response shapes, headers), not internal functions
- Each test should create its own data — never depend on test ordering
- Use factories for test data, not raw dicts repeated across tests
- Test error cases: 400 (validation), 401 (unauth), 403 (forbidden), 404 (not found)
- Always assert on response status code first, then body
- Use `db_session.rollback()` or transaction-scoped fixtures to isolate tests
- Name tests: `test_<action>_<scenario>_<expected>` (e.g., `test_create_user_duplicate_email_returns_409`)
- After writing tests, run `pytest -v` to confirm they pass
