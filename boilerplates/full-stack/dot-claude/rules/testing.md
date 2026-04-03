---
globs: ["**/*.test.*", "**/*.spec.*", "**/test_*.py", "**/*_test.py", "**/*_test.go", "**/tests/**", "**/__tests__/**"]
description: "Framework-agnostic testing standards for full-stack projects"
---

## Structure

- Follow Arrange-Act-Assert (Given-When-Then) pattern
- One behavior per test — if the test name has "and", split it
- Each test is independent — no shared mutable state, no ordering dependencies

## Naming

- Test names describe the scenario and expected outcome
- Pattern: `test_<what>_<when>_<expected>` or `it("should <expected> when <condition>")`
- Bad: `test_create_user` — Good: `test_create_user_returns_201_with_valid_input`

## Mocking

- Mock external services (APIs, databases, file system), not internal modules
- Use factories for test data, not hardcoded literals repeated across tests
- Assert on specific values, not truthiness

## Coverage

- Every new code path needs tests: happy path + error cases + edge cases
- Do not test framework internals or trivial getters/setters
- No snapshot tests for logic — use them only for rendering if the project already does
- No `test.skip` or `xtest` — either the test works or delete it

## Execution

- Run the full test suite after writing tests
- If tests fail, fix them before reporting completion
- No flaky conditions (timeouts, race conditions in tests)
