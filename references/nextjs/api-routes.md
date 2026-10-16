# Next.js API Routes

Use this when creating or changing backend API endpoints. Folder placement is defined in `structure.md`.

## Boundary rules

- Keep route handlers thin: parse and validate the request, call a service, shape the response.
- Put reusable backend logic in `app/api/(services)/`, never directly in route handlers.
- Shared types used by both UI and backend belong under `app/(common-lib)/types`.
- Read configuration from env vars; do not hardcode keys, URLs, or model names.
- LLM clients must support OpenAI-compatible endpoints by reading `baseURL` from env.
- Load LLM prompts from `.txt` files (see `prompts-config.md`).
