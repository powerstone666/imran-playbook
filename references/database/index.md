# Database

Use this whenever a task creates, changes, or chooses a database.

## Ask first

Never pick the database setup silently. Ask these together in one message and wait for the answers. Recommend a default for each, but let the user choose.

1. **ORM or raw queries?** ORM (for example Drizzle or Prisma): typed models, more abstraction. Raw SQL (for example `better-sqlite3`, `pg`): full control, the `.sql` files are the single source of truth.
2. **Local or cloud?** Local: a file or local server on the user's machine. Cloud: a hosted database (for example Turso, Neon, Supabase); ask which provider.
3. **Which engine?** Default to SQLite when the user has no preference. Offer Postgres for relational data at scale or a hosted multi-user setup.

- Ask even if the repo suggests an answer; confirm it instead of assuming. If the repo already has a database, follow its choice and say so.
- Record the answers in `plan.md` or `knowledge.md` when those exist, so later agents do not ask again.
- Install any driver or ORM per `references/package-installation/npm.md`.

## Schema files

`db/` holds schema only: one `.sql` file per table, so the user can open a file and see exactly what a table looks like and run it themselves. Do not put every table in one `schema.sql`, and do not describe the schema only in chat or hide it inside application code.

```text
db/
  user.sql      CREATE TABLE user, its indexes and constraints
  message.sql   CREATE TABLE message, its indexes and constraints
```

- One file per table (or per tightly coupled group, such as a table and its join table). Name the file after the entity, in the singular, matching the table name.
- Each file is runnable on its own with the database's CLI, for example `sqlite3 app.db < db/user.sql`. When foreign keys require an order, use numeric prefixes (`01_user.sql`, `02_message.sql`).
- Comment each table and non-obvious column in the SQL file so the schema documents itself.
- Do not create a `db/README.md`, or `migrations/`, `seeds/`, `queries/` folders by default. Add migrations or seeds only when the user asks.
- Queries do not live in `db/`. Put them in the service that owns the entity (for example `user.service.ts` holds the user queries).
- With an ORM, still keep the `.sql` files as the readable schema, or generate them into `db/`, and tell the user which one is authoritative. Do not leave the schema only inside ORM models.
- In the final report, list the files under `db/` and the one command that creates the database, so the user can run it outside the app.
