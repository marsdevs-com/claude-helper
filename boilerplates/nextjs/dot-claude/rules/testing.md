---
globs: ["**/*.test.ts", "**/*.test.tsx", "**/*.spec.ts", "**/*.spec.tsx", "**/tests/**", "**/__tests__/**"]
description: "Next.js testing standards with Vitest, React Testing Library, and Playwright"
---

# Next.js Testing Standards

## Test Types

| Type | Tool | What to test | Where |
|------|------|-------------|-------|
| Unit | Vitest | Utilities, hooks, validation schemas | `*.test.ts` next to source |
| Component | Vitest + RTL | Rendering, interactions, accessibility | `*.test.tsx` next to component |
| Integration | Vitest | Server Actions, API routes | `*.test.ts` next to source |
| E2E | Playwright | Full user flows | `tests/e2e/*.spec.ts` |

## Component Test Pattern

```tsx
import { render, screen } from "@testing-library/react";
import userEvent from "@testing-library/user-event";
import { describe, it, expect } from "vitest";
import { LoginForm } from "./LoginForm";

describe("LoginForm", () => {
  it("submits with valid credentials", async () => {
    const user = userEvent.setup();
    render(<LoginForm />);

    await user.type(screen.getByLabelText(/email/i), "test@example.com");
    await user.type(screen.getByLabelText(/password/i), "password123");
    await user.click(screen.getByRole("button", { name: /sign in/i }));

    expect(screen.queryByText(/invalid/i)).not.toBeInTheDocument();
  });

  it("shows validation error for empty email", async () => {
    const user = userEvent.setup();
    render(<LoginForm />);

    await user.click(screen.getByRole("button", { name: /sign in/i }));

    expect(screen.getByText(/email is required/i)).toBeInTheDocument();
  });
});
```

## Server Action Test Pattern

```tsx
import { describe, it, expect, vi } from "vitest";
import { updateProfile } from "./actions";

describe("updateProfile", () => {
  it("updates user profile with valid data", async () => {
    const formData = new FormData();
    formData.set("name", "New Name");

    const result = await updateProfile(formData);
    expect(result.success).toBe(true);
  });

  it("returns errors for invalid data", async () => {
    const formData = new FormData();
    formData.set("name", ""); // Empty name

    const result = await updateProfile(formData);
    expect(result.error).toBeDefined();
  });
});
```

## Rules

- Use `screen.getByRole()` and `getByLabelText()` over `getByTestId()` — test like a user
- Use `userEvent` over `fireEvent` — it simulates real browser behavior
- Test behavior, not implementation — don't test internal state or method calls
- Each test should be independent — no shared mutable state
- Mock external services (APIs, databases), not internal modules
- Every form component needs: happy path, validation errors, submission states
- After writing tests, run `pnpm test -- --run` to verify they pass
- Name tests descriptively: what component, what scenario, what expected outcome
- Accessible components are testable components — if you can't query by role, the component needs accessibility fixes
