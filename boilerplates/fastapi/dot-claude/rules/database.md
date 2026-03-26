---
globs: ["**/repositories/**/*.py", "**/db/**/*.py", "**/models/**/*.py", "alembic/**/*.py"]
description: "Database and repository patterns for async SQLAlchemy with FastAPI"
---

# Database Standards

## Repository Pattern

```python
from sqlalchemy import select
from sqlalchemy.ext.asyncio import AsyncSession

class UserRepository:
    def __init__(self, session: AsyncSession):
        self.session = session

    async def get_by_id(self, user_id: UUID) -> User | None:
        result = await self.session.execute(
            select(User).where(User.id == user_id)
        )
        return result.scalar_one_or_none()

    async def get_by_email(self, email: str) -> User | None:
        result = await self.session.execute(
            select(User).where(User.email == email)
        )
        return result.scalar_one_or_none()

    async def create(self, user: User) -> User:
        self.session.add(user)
        await self.session.flush()
        return user
```

## Rules

- All DB operations must be async (`AsyncSession`, `await`)
- Use the repository pattern — never write raw queries in route handlers
- Use `select()` from SQLAlchemy 2.0, not legacy `session.query()`
- Use `.scalar_one_or_none()` for single results, `.scalars().all()` for lists
- Always use `.flush()` instead of `.commit()` in repositories — let the route/service control the transaction
- Use `selectin` or `joinedload` for relationships to avoid N+1 queries
- Add database indexes on all foreign keys and frequently-queried columns
- Never use `session.execute(text("raw SQL"))` unless absolutely necessary

## Migrations (Alembic)

- Always auto-generate: `alembic revision --autogenerate -m "description"`
- Review the generated migration before applying — autogenerate can miss things
- Never edit a migration that has been applied to shared environments
- Migration messages should be descriptive: "add_user_email_index" not "update"
- Always test migrations: `alembic upgrade head` then `alembic downgrade -1` then `alembic upgrade head`
- Keep migrations small — one logical change per migration
