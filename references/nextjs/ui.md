# Next.js UI

Use this when building or editing frontend components. Folder placement is defined in `structure.md`.

## UI to backend boundary

This is the single home for the frontend/backend boundary rule.

- Frontend components call backend endpoints through typed API client functions in `app/(ui)/lib/api-client.ts`.
- Never import or call backend services directly from UI components.

Prefer:

```text
UI component -> app/(ui)/lib/api-client.ts -> app/api/<route>/route.ts -> backend service
```

Avoid:

```text
UI component -> backend service
```

Example client function:

```ts
// app/(ui)/lib/api-client.ts
export async function askQuestion(question: string) {
  const response = await fetch("/api/query", {
    method: "POST",
    headers: { "Content-Type": "application/json" },
    body: JSON.stringify({ question }),
  });

  if (!response.ok) {
    throw new Error("Failed to ask question");
  }

  return response.json();
}
```

Example usage:

```ts
import { askQuestion } from "@/app/(ui)/lib/api-client";

export async function submitQuestion(question: string) {
  return askQuestion(question);
}
```

## Interaction rule

- All interactive elements must have `cursor-pointer`.
- Buttons, clickable cards, dropdowns, and expandable rows are interactive.
- Non-interactive elements should not use `cursor-pointer`.
