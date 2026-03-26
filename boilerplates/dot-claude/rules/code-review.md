---
globs: ["**/*"]
description: "Checklist for code review tasks"
---

# Code Review Checklist

When reviewing code, check for:

<!-- TODO: Customize for your team's standards -->

**Correctness**
- Does the code do what it claims?
- Are edge cases handled (nulls, empty arrays, boundary conditions)?

**Security**
- No hardcoded secrets or API keys
- No SQL injection, XSS, or command injection vectors
- Input is validated at system boundaries

**Performance**
- No N+1 queries or unbounded loops
- No unnecessary re-renders or recomputation
- Large data sets are paginated or streamed

**Readability**
- Clear naming — no abbreviations unless universally understood
- Reasonable function length (under 50 lines)
- No deep nesting (max 3 levels)

**Tests**
- Are changes covered by tests?
- Are edge cases and error paths tested?

**Types**
- Are types accurate and specific (not `any` or `object`)?

## Output Format

Structure your review as:
1. **Summary** — one sentence describing what the change does
2. **Issues** — each tagged `[CRITICAL]`, `[WARNING]`, or `[NIT]` with `file:line`
3. **Suggestions** — optional improvements, not blockers
