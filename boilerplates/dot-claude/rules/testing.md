---
globs: ["**/*.test.*", "**/*.spec.*", "**/test_*.py", "**/*_test.py", "**/*_test.go", "**/tests/**"]
description: "Standards for writing and modifying tests"
---

# Testing Standards

When writing or modifying tests:

<!-- TODO: Customize these rules for your project -->

- Follow the Arrange-Act-Assert pattern
- Each test should test exactly one behavior
- Use descriptive test names: `test_<what>_<when>_<expected>`
- Never use `any` types in test assertions
- Mock external dependencies (APIs, databases), not internal modules
- Include both happy-path and error cases
- Do not skip or disable existing tests without explanation
- After writing tests, run the full test suite to confirm they pass
- Keep test files next to the code they test (or in a mirrored `tests/` directory)
- Prefer real assertions over snapshot tests for logic
