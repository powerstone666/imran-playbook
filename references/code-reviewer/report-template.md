# Code Review Report Template

Use this structure for the final response.

## Review Summary

- Feature or bug: `...`
- Reviewed comparison: `base...source`
- Assumed load: `...`
- Special attention: `...`
- Overall quality score: `x/10`
- Deployment risk: `Low`, `Medium`, or `High`
- Merge recommendation: `Approve`, `Approve with comments`, `Request changes`, or `Unable to complete`

## Findings

List findings first, numbered across all severities. For each finding, use this format:

`1. [Severity] Title`  
Why it matters: `...`  
Evidence: `...`  
Fix: `...`  
Reference: `path/to/file.ext:123`

If there are no findings, write `No concrete review findings.` and move on.

## Review Coverage

- `Correctness`: `...`
- `Requirement compliance`: `...`
- `Security`: `...`
- `Performance`: `...`
- `Maintainability`: `...`
- `Error handling`: `...`
- `Edge cases`: `...`
- `Test coverage`: `...`

## Open Questions And Assumptions

- `...`

## Acceptance Criteria Coverage

- `Criterion`: met, partially met, or not met
- `Notes`: `...`

## Validation Run

- `Command`: result
- `Command`: result
- Blockers: `...`

## Recommendation

- One short paragraph with the merge recommendation and the most important rationale, naming which findings to fix first (for example, "fix 1 and 3 first").
