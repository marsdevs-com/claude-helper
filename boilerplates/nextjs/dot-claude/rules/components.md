---
globs: ["**/components/**/*.tsx", "**/components/**/*.ts", "app/**/*.tsx"]
description: "React and Next.js component standards (Server vs Client, patterns, props)"
---

# Component Standards

## Server Components (Default)

Every component is a Server Component unless it needs interactivity. Do NOT add `"use client"` unless you need one of these:

- `useState`, `useEffect`, `useReducer`, `useContext`
- Event handlers: `onClick`, `onChange`, `onSubmit`
- Browser APIs: `window`, `document`, `localStorage`
- Hooks from client-only libraries

```tsx
// Server Component — no directive needed
// Can: fetch data, access DB, read cookies, use async/await
interface UserProfileProps {
  userId: string;
}

export async function UserProfile({ userId }: UserProfileProps) {
  const user = await db.user.findUnique({ where: { id: userId } });
  if (!user) notFound();

  return (
    <div>
      <h1>{user.name}</h1>
      <InteractiveSection user={user} /> {/* Client boundary pushed down */}
    </div>
  );
}
```

## Client Components

Push the `"use client"` boundary as low as possible:

```tsx
"use client";

// Only the interactive part is a Client Component
interface LikeButtonProps {
  postId: string;
  initialCount: number;
}

export function LikeButton({ postId, initialCount }: LikeButtonProps) {
  const [count, setCount] = useState(initialCount);
  // ...
}
```

## Component Structure

```tsx
// 1. Directive (only if needed)
"use client";

// 2. Imports
import { cn } from "@/lib/utils";

// 3. Props interface
interface ButtonProps extends React.ButtonHTMLAttributes<HTMLButtonElement> {
  variant?: "primary" | "secondary" | "ghost";
  size?: "sm" | "md" | "lg";
}

// 4. Component (named export)
export function Button({ variant = "primary", size = "md", className, children, ...props }: ButtonProps) {
  return (
    <button
      className={cn(
        "rounded font-medium transition-colors",
        variants[variant],
        sizes[size],
        className,
      )}
      {...props}
    >
      {children}
    </button>
  );
}
```

## Rules

- Named exports only (except `page.tsx`, `layout.tsx`, `loading.tsx`, `error.tsx` which use default)
- Props interface always named `{Component}Props`
- Use `cn()` utility for conditional Tailwind classes
- Compose small components — avoid 200+ line components
- Never fetch data in `useEffect` when a Server Component can do it
- Never pass serialized functions from Server to Client components
- Reuse `components/ui/` primitives — check what exists before creating new ones
- Use `@/` path alias — never `../../..` relative imports
