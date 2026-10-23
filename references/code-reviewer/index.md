# Code Reviewer

Use this to review code changes without editing them. Collect the request details, inspect the diff against the correct base, run the most appropriate tests you can discover locally, and return a structured report that focuses on bugs, regressions, missing coverage, and risk.

This is the only code review reference. It has two modes:

- **Full review** of a diff, branch, or PR: follow the whole workflow below and return the report in `report-template.md`.
- **Self-review** of your own change before finishing: skip Required Inputs (do not ask questions) and the report; run the Maintainability Checklist and the validation step, then fix what you find.

## Maintainability Checklist

- Is the intent obvious without extra explanation?
- Are names domain-meaningful?
- Is control flow flat and easy to scan?
- Are dependencies injectable and test seams clear?
- Are literals named where meaning matters?
- Are functions cohesive and short?
- Is abstraction level appropriate, neither over-engineered nor under-engineered?
- Are comments rationale-focused and current?
- Did validation cover the touched behavior?
- Is each change at the right layer (see `../senior-dev/change-ladder.md`)?

## Required Inputs

This is a hard gate. Do not read the diff, run commands, or start the review until the inputs below are settled.

Needed inputs:

- Feature or bug description
- Source branch or PR reference
- Base branch
- Acceptance criteria
- Areas requiring special attention

Steps:

1. Check what the user's message and the repo (`git branch --show-current`, `git status`) already answer. Pre-fill what you can, such as the current branch as the source and `main` as the base.
2. Ask about everything still missing with the `AskUserQuestion` tool, in one call of up to 4 questions. Offer your pre-filled guess as the first option, marked "(Recommended)", and let the user pick "Other" to type their own answer. If the tool is not available, ask the same questions as a short numbered list and stop until the user replies.
3. Always ask for acceptance criteria and special-attention areas unless the user already gave them; the repo cannot answer these.
4. Only skip asking if the user says to review right away (for example "just review it"). Then state your assumptions in the report. If a PR reference is unavailable locally, ask for the source branch or a checked-out worktree instead of guessing.
5. If the user names no review target at all, ask which to review: uncommitted changes, the last commit, or a branch. Recommend uncommitted changes, or the last commit if there are none.

## Guardrails

- Do not modify code, tests, configs, or generated files.
- Do not fix issues during the review.
- Stay within the local workspace unless the user explicitly asks for a remote lookup and the necessary tools are available.
- Treat unverified assumptions as assumptions, not findings.
- If a command cannot run, record the blocker and continue with the rest of the review where possible.

## Review Workflow

### 1. Confirm Review Scope

- Restate the feature or bug description in one or two lines.
- Confirm the source branch or PR reference and the base branch.
- Restate the acceptance criteria and any special attention areas.
- Note the exact comparison you will review, such as `main...feature/add-cache`.

### 2. Gather Repository Context

- Check repository status and current branch.
- Identify the project’s test and build systems from local signals such as `package.json`, `pyproject.toml`, `Makefile`, CI config, or test directories.
- Skim any local docs that directly affect review expectations, such as contribution guides or test instructions, if they are easy to locate.
- Find the expected load (README, deploy config): one person running a script, or many users and processes at once. Judge scale against it and state the load you assumed.

### 3. Inspect the Diff

- Use `git diff --stat` and `git diff --name-only` first to size the change.
- Review the full patch for the requested comparison.
- Pay extra attention to files or paths the user flagged.
- Trace the real flow: where data comes in, what is stored, what goes out.
- A change can break code it does not touch. When a signature, return value, or behavior changes, grep every caller.
- Review these aspects explicitly (use the Maintainability Checklist above for maintainability): correctness, requirement compliance, security, performance, maintainability, error handling, edge cases, and test coverage.
- Look for regressions, missing validation, weak error handling, security concerns, backwards compatibility problems, and test gaps.
- Check edge cases explicitly: empty, zero, last item, rounding, time zones.
- Check scale against the expected load: check-then-write races, a query per item, lists or memory that only grow, O(n²) on big input, per-process state that must be shared.
- Flag code that should not exist: dead code, unused options, speculative features, or a helper the repo already has (name its path).
- Check whether the implementation appears to satisfy the stated acceptance criteria.

### 4. Run Validation

- Prefer targeted tests that match the changed area.
- Run broader relevant suites when the project layout or CI config suggests they are expected and the cost is reasonable.
- If linting, type checks, or build validation are standard for the repo and directly relevant to the changed code, run them too.
- Do not invent commands. Infer them from the repository.
- Capture which commands ran, which passed, which failed, and any environment blockers.
- If the code has not changed since the last run, do not rerun tests, linting, or type checks; reuse the earlier results.

### 5. Form Findings

Prioritize findings by severity:

- `High`: likely bug, regression, security issue, data loss, broken contract, or release blocker
- `Medium`: important correctness or maintainability risk that should likely block merge
- `Low`: smaller issue, clarity problem, or limited-scope risk

A finding should include:

- Number (count across all severities, so the user can say "fix 2 and 5")
- Severity
- Short title
- Why it matters
- Evidence from the diff or validation
- Smallest fix that works, preferring fixes that delete code
- File reference with line numbers when available

Before reporting a finding, confirm it:

- It needs a concrete case: "this input or situation leads to this wrong result". No case, no finding.
- Re-read the lines: the caller exists, the value can really be empty, the code really is unused.
- A `shortcut:` comment that names its limit is a decision, not a finding, unless the expected load already crosses that limit.

If there are no concrete findings, say so explicitly instead of padding the report.

### 6. Return the Report

Use the report structure in `report-template.md`.

Keep the report focused on review results:

- Findings first, ordered by severity
- Aspect-by-aspect review coverage for correctness, requirement compliance, security, performance, maintainability, error handling, edge cases, and test coverage
- Open questions or assumptions next
- Acceptance-criteria coverage
- Validation summary
- Overall quality score out of 10
- Deployment risk as `Low`, `Medium`, or `High`
- Final recommendation

Write in simple English: short sentences, everyday words, and explain a technical term the first time you use it.

## Review Heuristics

- Compare new behavior with likely existing caller expectations.
- Watch for missing updates across tests, docs, schemas, fixtures, or types when the code change suggests they should move together.
- Favor behavioral risks over style commentary. No style taste, no "consider", no vague worries.
- Be explicit about uncertainty when you cannot run a needed command or inspect a missing branch.
- If the change is large, summarize the architecture or change areas briefly before the findings.
