# Next.js Routing

Use this when adding or changing pages, layouts, route groups, or URL structure. Folder placement is defined in `structure.md`.

## Route groups

Folders wrapped in parentheses are excluded from the URL path. That is why the non-route folders in `structure.md` (`(services)`, `(prompts)`, `(db)`, `(common-lib)`, `(ui)`, `(config)`) use them.

A route group still routes any `page.tsx` or `route.ts` placed inside it, so keep those files out of non-route groups.

## Pages and layouts

Place `page.tsx` and `layout.tsx` at the folder matching their URL:

```text
app/page.tsx               -> /
app/settings/page.tsx      -> /settings
app/settings/layout.tsx    -> layout for /settings/*
```

## API routes

Each API endpoint gets its own folder with a `route.ts` file:

```text
app/api/upload/route.ts
app/api/parse/route.ts
app/api/query/route.ts
```

Route handler boundaries are in `api-routes.md`.
