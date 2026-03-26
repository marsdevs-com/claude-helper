# Project Name — Next.js

<!-- Template by MarsDevs (www.marsdevs.com) — customize the TODO sections below -->
<!-- TODO: Replace with your project description -->
Brief description of what this application does.

## Tech Stack

- **Framework**: Next.js 15 (App Router)
- **Language**: TypeScript 5.x (strict mode)
- **Styling**: Tailwind CSS v4
- **State**: React Server Components + Server Actions
- **Database**: Prisma ORM + PostgreSQL
- **Auth**: NextAuth.js v5
- **Testing**: Vitest + React Testing Library + Playwright
- **Linting**: ESLint + Prettier
- **Package Manager**: pnpm

<!-- TODO: Update with your actual stack -->

## Architecture

```
app/
├── layout.tsx               # Root layout (providers, global styles)
├── page.tsx                 # Home page
├── (auth)/                  # Auth route group (login, register)
│   ├── login/page.tsx
│   └── register/page.tsx
├── (dashboard)/             # Dashboard route group (authenticated)
│   ├── layout.tsx           # Dashboard layout with sidebar
│   └── settings/page.tsx
├── api/                     # API route handlers
│   └── webhooks/route.ts
└── globals.css              # Global styles and Tailwind imports
components/
├── ui/                      # Reusable UI primitives (Button, Input, Card)
├── forms/                   # Form components with validation
└── layouts/                 # Layout components (Header, Sidebar, Footer)
lib/
├── db.ts                    # Prisma client singleton
├── auth.ts                  # NextAuth config
├── utils.ts                 # Shared utility functions
└── validations/             # Zod schemas for form/API validation
hooks/                       # Custom React hooks
types/                       # Shared TypeScript type definitions
public/                      # Static assets
prisma/
├── schema.prisma            # Database schema
└── migrations/              # Migration history
```

<!-- TODO: Adjust to match your actual layout -->

## Key Files

- @app/layout.tsx — Root layout, providers, metadata
- @lib/db.ts — Prisma client (singleton for hot reload)
- @lib/auth.ts — Auth configuration and session helpers
- @lib/utils.ts — Shared utilities (cn(), formatDate(), etc.)
- @components/ui/ — Base UI components used everywhere
- @prisma/schema.prisma — Database schema (source of truth)

<!-- TODO: Add your project's key files -->

## Conventions

### Components
- Server Components by default — only add `"use client"` when you need interactivity
- Co-locate component, styles, and tests: `Button.tsx`, `Button.test.tsx`
- Use named exports, not default exports (except for pages)
- Props interface named `{Component}Props` and defined above the component
- Composition over configuration — small components composed together

### Server Components vs Client Components
- **Server**: data fetching, database access, reading cookies/headers, heavy dependencies
- **Client**: interactivity (onClick, onChange), browser APIs, useState/useEffect, animations
- Keep the `"use client"` boundary as low as possible in the component tree
- Never import server-only code in client components
- Pass server data to client components via props, not by making them server components

### Data Fetching
- Fetch data in Server Components, not in useEffect
- Use Server Actions for mutations (forms, button actions)
- Validate all inputs with Zod schemas in `lib/validations/`
- Use `revalidatePath()` or `revalidateTag()` after mutations

### Routing (App Router)
- Use route groups `(groupName)` for shared layouts without URL segments
- Use `loading.tsx` for streaming/suspense per route
- Use `error.tsx` for route-level error boundaries
- Use `not-found.tsx` for custom 404 pages
- Parallel routes `@slot` for modals and conditional layouts

### TypeScript
- Strict mode always enabled
- No `any` — use `unknown` and narrow, or define proper types
- Shared types in `types/` directory
- Use Zod for runtime validation, TypeScript for compile-time
- Infer types from Zod schemas: `type User = z.infer<typeof userSchema>`

### Styling
- Tailwind CSS utility classes for all styling
- Use `cn()` utility (clsx + twMerge) for conditional classes
- No inline styles, no CSS-in-JS
- Responsive: mobile-first (`sm:`, `md:`, `lg:` breakpoints)
- Dark mode via Tailwind `dark:` variant

## Rules

- Never use `"use client"` unless the component needs interactivity or browser APIs
- Never fetch data in useEffect when a Server Component can do it
- Never use `any` type — define proper types or use `unknown`
- Never import from `@prisma/client` directly — use `@/lib/db`
- Never commit .env files or secrets
- Never modify migration files after they've been applied
- Do not mention AI tools in commit messages
- Run `pnpm test` before considering any task complete
- Run `pnpm lint` and `pnpm typecheck` before committing

## Common Commands

```bash
# Development
pnpm dev

# Build
pnpm build

# Start production
pnpm start

# Type check
pnpm typecheck    # or: npx tsc --noEmit

# Lint and format
pnpm lint
pnpm format       # or: npx prettier --write .

# Test
pnpm test                        # Unit tests (Vitest)
pnpm test:e2e                    # E2E tests (Playwright)
pnpm test -- --run path/to/test  # Single test file

# Database
npx prisma generate              # Regenerate client after schema change
npx prisma db push               # Push schema changes (dev only)
npx prisma migrate dev           # Create and apply migration
npx prisma studio                # Visual database browser

# Storybook (if configured)
pnpm storybook
```

## Claude Best Practices for This Project

- Always read existing components in `components/ui/` before creating new ones — reuse first
- When creating a new page, also create its `loading.tsx` and `error.tsx`
- When adding a form, create the Zod schema in `lib/validations/` first, then the Server Action, then the form component
- When fixing a bug, write a failing test first, then fix
- Use `@/` path aliases — never use relative paths like `../../../`
- Check if a component can be a Server Component before adding `"use client"`
- After any Prisma schema change, always run `npx prisma generate` and create a migration
