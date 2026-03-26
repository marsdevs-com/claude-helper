---
globs: ["**/routers/**/*.py", "**/routes/**/*.py", "**/endpoints/**/*.py", "**/api/**/*.py"]
description: "FastAPI route handler standards and patterns"
---

# FastAPI Route Standards

## Route Handler Pattern

Every route handler should follow this structure:

```python
@router.post("/", response_model=ItemResponse, status_code=status.HTTP_201_CREATED)
async def create_item(
    payload: ItemCreate,
    db: AsyncSession = Depends(get_db),
    current_user: User = Depends(get_current_user),
) -> ItemResponse:
    """Create a new item."""
    service = ItemService(db)
    item = await service.create(payload, owner_id=current_user.id)
    return ItemResponse.model_validate(item)
```

## Rules

- Always declare `response_model` on the decorator
- Always use `status` codes from `starlette.status`
- Route handlers should be thin — delegate to services
- Use `Depends()` for auth, db sessions, pagination, and all shared logic
- Never put business logic in route handlers
- Never catch generic `Exception` in routes — let the exception handler middleware handle it
- Group related routes in one router file with a shared prefix and tag
- Use path parameters for resource identifiers: `/users/{user_id}`
- Use query parameters for filtering/pagination: `?page=1&limit=20`
- Return Pydantic schemas, never raw dicts or ORM objects

## Dependency Injection

```python
# Good: Use Depends for shared logic
async def get_current_user(token: str = Depends(oauth2_scheme)) -> User: ...
async def get_db() -> AsyncGenerator[AsyncSession, None]: ...
async def get_pagination(page: int = 1, limit: int = Query(20, le=100)) -> Pagination: ...

# Use them in routes
@router.get("/items", response_model=PaginatedResponse[ItemResponse])
async def list_items(
    db: AsyncSession = Depends(get_db),
    current_user: User = Depends(get_current_user),
    pagination: Pagination = Depends(get_pagination),
): ...
```

## Error Responses

```python
# Raise domain exceptions — they get caught by exception handlers in main.py
from app.exceptions import NotFoundError, ForbiddenError

if not item:
    raise NotFoundError("Item", item_id)
if item.owner_id != current_user.id:
    raise ForbiddenError("You do not own this item")
```
