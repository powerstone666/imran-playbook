# Next.js Project Structure

This is the single source of truth for Next.js folder placement. Other Next.js files link here instead of restating it.

Apply it to new Next.js projects and to new code in projects that already follow it. In an existing project with a different established layout, follow the existing layout and mention the difference instead of moving files.

```text
app/
  page.tsx               # "/" route: the product showcase (see ui-design/material-3-web.md)
  <segment>/page.tsx     # Other pages and layouts live at their URL path
  api/
    (services)/          # Backend code: models, agents, processors, tools, utils
      processors/        # Sub-agents and data processors
      tools/             # LangChain tools
      utils/             # Utility functions
    (db)/                # Database services, if applicable
    (prompts)/           # LLM prompt .txt files
    <route>/route.ts     # API route handlers, e.g. upload/, parse/, query/
  (common-lib)/          # Shared code used by UI and backend
    types/               # TypeScript interfaces and types
  (ui)/                  # Non-route UI code: components, hooks
    lib/api-client.ts    # Typed client functions for backend routes
  (config)/              # JSON, PDFs, and static config files
```

## Rules

- All application code belongs under `app/`. Framework-required root files (`next.config.*`, `middleware.ts`, `package.json`, etc.) stay at the root.
- Route files (`page.tsx`, `layout.tsx`, `loading.tsx`, `error.tsx`) live at their URL path under `app/`. Keep them thin: they compose components imported from `app/(ui)/`.
- Do not put `page.tsx` inside `app/(ui)/`; it would become a real route (for example `app/(ui)/page.tsx` serves `/`).
- Backend code goes under `app/api/(services)/`.
- API routes go under `app/api/<route>/` with a `route.ts` file.
- Database services go under `app/api/(db)/`.
- Prompts go under `app/api/(prompts)/`.
- Shared code goes under `app/(common-lib)/`.
- Config files go under `app/(config)/`.
