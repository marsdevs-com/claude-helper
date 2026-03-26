---
globs: ["**/models/**/*.py", "**/schemas/**/*.py", "**/models.py", "**/schemas.py"]
description: "SQLAlchemy model and Pydantic schema conventions for FastAPI"
---

# Models & Schemas Standards

## SQLAlchemy Models (`models/`)

```python
from sqlalchemy import Column, String, DateTime, ForeignKey
from sqlalchemy.dialects.postgresql import UUID
from sqlalchemy.orm import Mapped, mapped_column, relationship
import uuid
from datetime import datetime, UTC

class User(Base):
    __tablename__ = "users"

    id: Mapped[uuid.UUID] = mapped_column(UUID(as_uuid=True), primary_key=True, default=uuid.uuid4)
    email: Mapped[str] = mapped_column(String(255), unique=True, index=True, nullable=False)
    created_at: Mapped[datetime] = mapped_column(DateTime(timezone=True), default=lambda: datetime.now(UTC))
    updated_at: Mapped[datetime] = mapped_column(DateTime(timezone=True), onupdate=lambda: datetime.now(UTC))

    # Relationships
    items: Mapped[list["Item"]] = relationship(back_populates="owner", lazy="selectin")
```

## Pydantic Schemas (`schemas/`)

Split into purpose-specific schemas:

```python
from pydantic import BaseModel, ConfigDict, EmailStr
from uuid import UUID
from datetime import datetime

# Input: what the client sends
class UserCreate(BaseModel):
    email: EmailStr
    password: str  # min_length validated via Field()

# Input: partial updates
class UserUpdate(BaseModel):
    email: EmailStr | None = None
    display_name: str | None = None

# Output: what the API returns
class UserResponse(BaseModel):
    model_config = ConfigDict(from_attributes=True)

    id: UUID
    email: str
    created_at: datetime
    # Never include: password, password_hash, internal flags
```

## Rules

- Never expose ORM models in API responses — always use a response schema
- Never include sensitive fields (password_hash, internal_notes, is_admin) in response schemas
- All IDs should be `UUID`, not `int`
- All timestamps should be timezone-aware `datetime` (UTC)
- Use `Mapped[]` type annotations in SQLAlchemy 2.0 models
- Use `ConfigDict(from_attributes=True)` on response schemas for ORM compatibility
- Use `EmailStr` for email validation, not bare `str`
- Every model needs `created_at` and `updated_at` timestamps
- Use `Field()` for validation constraints: `Field(min_length=8, max_length=100)`
- Index columns used in WHERE clauses and foreign keys
- Name schemas clearly: `{Entity}Create`, `{Entity}Update`, `{Entity}Response`
