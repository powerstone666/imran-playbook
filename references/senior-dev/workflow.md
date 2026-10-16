# Senior Developer Workflow

Produce maintainable code that a new teammate can confidently modify.
Prioritize clarity, testability, and safe evolution over cleverness.

## Workflow

1. Clarify intent, constraints, and non-goals before editing.
2. Map the scope: read the code the task touches and list every place the change must reach (callers, tests, fixtures, config, exports). Check what it could break for users: data it could destroy or expose, callers that stop working. That is the scope; extra features are not.
3. Design the smallest complete change using the reuse ladder in `change-ladder.md`.
4. Implement for readability first, then optimize if required.
5. Validate behavior with tests or reproducible checks.
6. Leave the codebase easier to understand than before.

## Smallest complete change

- Write as little new code as possible, but finish every part the task needs, including the callers, tests, and fixtures the change breaks.
- Skip features, options, and flexibility nobody asked for, and name what you skipped in one line of the final report.
- A vague request ("build me X") gets the smallest version that does the core job.
- Code you move or merge keeps its error handling and validation.

## Never cut

Minimal code never removes or skips:

- Validation at trust boundaries.
- Error handling that prevents data loss.
- Security and authorization checks.
- Accessibility.
- Calibration or tuning that real hardware needs.
- Anything the user explicitly asked for.

## Operating principles

- Make assumptions explicit.
- Make intent obvious in names and structure.
- Reduce cognitive load in each function.
- Prefer straightforward code over terse shortcuts.
- Use obvious language/library primitives.
- Avoid obscure operators when a clear equivalent exists.
- Reject clever one-liners that hide intent.
- Choose the simplest design that satisfies current requirements.
- Add abstraction only when it removes recurring complexity.
- Reduce technical debt in touched areas.
- Improve onboarding by keeping flows discoverable.
- Favor changes that make future refactors safer.

## Default code style

This is the single home for general code style rules. Framework files add only framework-specific rules.

- Readable > fast: 100ms clean code beats 50ms clever code unless performance is a real requirement. Code is for humans first.
- Simple and minimal: no unnecessary abstractions, singletons, or over-engineering. No wrapper, type conversion, option, config, boilerplate, or "for later" code nobody asked for. Keep values in the form the platform already gives you.
- Sync vs async: no I/O means sync; I/O means async. Do not use blanket rules.
- Class vs function: class when grouping related methods with shared dependencies, function when standalone. Read `class-vs-function.md` when introducing services, clients, processors, or reusable modules.
- Return objects for multi-value results: `{ model, contextSize }`, not `[model, contextSize]` (see `functions.md`).
- No hardcoded values unless explicitly requested: use env vars for configuration and named constants for domain values (see `naming.md`).
- Comments are short and explain why, tradeoffs, or non-obvious constraints. Let code explain what it does (see `maintainability.md`).
