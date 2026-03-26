---
globs: ["app/api/**/*.ts", "app/api/**/*.tsx", "**/actions/**/*.ts", "**/actions.ts"]
description: "Next.js API route handlers and Server Actions standards"
---

# API Routes & Server Actions

## Route Handlers (`app/api/`)

Use for webhooks, external API endpoints, and non-form mutations:

```tsx
// app/api/webhooks/stripe/route.ts
import { NextRequest, NextResponse } from "next/server";

export async function POST(request: NextRequest) {
  const body = await request.json();

  // Validate webhook signature
  // Process webhook
  // Return response

  return NextResponse.json({ received: true }, { status: 200 });
}
```

## Server Actions (Preferred for UI Mutations)

Use for form submissions and UI-triggered mutations:

```tsx
// app/(dashboard)/settings/actions.ts
"use server";

import { z } from "zod";
import { revalidatePath } from "next/cache";
import { auth } from "@/lib/auth";

const updateProfileSchema = z.object({
  name: z.string().min(1).max(100),
  bio: z.string().max(500).optional(),
});

export async function updateProfile(formData: FormData) {
  const session = await auth();
  if (!session?.user) throw new Error("Unauthorized");

  const parsed = updateProfileSchema.safeParse({
    name: formData.get("name"),
    bio: formData.get("bio"),
  });

  if (!parsed.success) {
    return { error: parsed.error.flatten().fieldErrors };
  }

  await db.user.update({
    where: { id: session.user.id },
    data: parsed.data,
  });

  revalidatePath("/settings");
  return { success: true };
}
```

## Rules

- Prefer Server Actions over API routes for UI mutations
- Always validate input with Zod — never trust `formData` or `request.json()` directly
- Always check authentication in Server Actions — they are public endpoints
- Use `revalidatePath()` or `revalidateTag()` after mutations to refresh cached data
- Never import Server Actions in client components that don't need them
- API route files export named HTTP methods: `GET`, `POST`, `PUT`, `DELETE`, `PATCH`
- Return proper HTTP status codes: 200 (ok), 201 (created), 400 (bad input), 401 (unauth), 404 (not found)
- Handle errors gracefully — never let raw Error objects reach the client
- Keep Server Actions in co-located `actions.ts` files or a shared `lib/actions/` directory
