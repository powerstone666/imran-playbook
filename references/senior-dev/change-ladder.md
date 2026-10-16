# Change Ladder

Prefer the most localized change. Picture the codebase as a ladder from the outer layer (what the user touches) down to the inner dependencies (what everything else relies on). Each step down the ladder is worth fewer points, because a change there reaches more callers, carries more risk, and needs more review.

Start at the top rung that can solve the problem correctly. Only step down when the rung above genuinely cannot do the job.

## The ladder

| Rung | Layer | Priority points | Examples |
| --- | --- | --- | --- |
| 1 | UI component, page, screen | 5 | Show/hide a button, change a label, pass a flag from a screen |
| 2 | UI helpers, client wrappers, per-feature config | 4 | A config entry, a client option, a UI utility |
| 3 | API route / request handler | 3 | Read a request field, add a route-level check, shape the response |
| 4 | Service, workflow, shared library | 2 | Business rules used by many routes and screens |
| 5 | Database, schema, migrations, stored data shape | 1 | New columns, constraints, data backfills |

Higher points mean higher priority. Inner rungs are not forbidden; they need a reason.

## How to choose

1. Find the outermost rung where the change fully solves the problem.
2. Check whether that rung is *correct*, not just *possible* (see the exceptions below). If it is, stop there.
3. If it is not, step down one rung at a time and repeat the check.
4. When a fix needs several rungs, keep the inner part as small as possible and put everything else at the outer rungs. A service may only need a data pass-through, while the decision stays in the screen or config.
5. Among options on the same rung, pick the shortest working diff that touches the fewest files: removing code beats adding it, and adding beats rewriting. Between options of equal size, pick the one that is correct on edge cases.

## Reuse ladder

The rungs above decide *where* the change goes. This ladder decides *what* to write there. Take the first option that fully works:

1. **Does it need to exist?** Skip what nobody asked for (see `workflow.md`).
2. **Already in this codebase?** Use the existing helper, component, service, or pattern the way the surrounding code does.
3. **Standard library or platform feature?** Use it, unless the project has its own. A house component beats a native widget.
4. **An installed dependency?** Use it. Adding a new one follows `../package-installation/npm.md`.
5. **One line a reader understands at a glance?** Write one line. A one-liner that needs decoding is not short.
6. **Otherwise:** the minimum code that works, keeping the codebase's existing layers, interfaces, and conventions.

## When stepping down is required

These are correctness rules, not point trade-offs. They override the ladder.

- **Security and authorization:** enforce permissions on the server (route or service). UI checks are user experience only; a hidden button never replaces a server check.
- **Data that users can tamper with:** anything sent from the browser must be validated or decided server-side if it controls stage, money, or access.
- **One source of truth:** if the same rule would otherwise be copied into several screens, put it once at the lowest rung they all share.
- **Data integrity:** rules that must hold no matter which code path writes the data belong in the service or the database.
- **Bug in shared code:** before editing, grep every caller of the function you touch, then fix the root cause once in the shared code instead of patching each caller.

## Examples

- **A button should appear for one record type (for example, one kind of order):** change the screen's render condition (rung 1). Don't add a new API field for it.
- **A per-action rule differs for one workflow:** add a field or override next to the existing action config (rung 2), not a hardcoded key check inside shared logic (rung 4).
- **A new record should start in a different workflow stage:** have the screen send the stage (rung 1/2) and rely on the existing route permission check (rung 3) instead of rewriting the service.
- **Spoofable flag from the client:** the screen sends a marker (rung 1), but the service only trusts it together with a server-verified condition (rung 4), because security forces the step down.
- **A participant must exist before actions are created:** this is a data-integrity rule, so call the existing sync method inside the service (rung 4) rather than patching each screen.

## Reporting

When proposing or summarizing a change, state the rung for each file you touch and why any inner-rung change was needed. If a reviewer suggests moving logic inward, weigh the points lost against the benefit (single source of truth, security) and say which wins.
