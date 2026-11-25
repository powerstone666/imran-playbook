# Commits

Use this when preparing a commit message, commit summary, or commit context.

## Before committing or pushing

When the user asks to commit or push, review the changes first (see "Review before you finish or commit" in `workflow.md`). Commit only after the review is done and its findings are handled.

## Authorship: never add yourself (always applies)

The commit belongs to the user alone. An agent never adds itself, or any AI tool, as an author or contributor.

- Do not add `Co-Authored-By:`, `Signed-off-by:`, or any similar trailer naming an agent, model, or AI tool.
- Do not add "Generated with ...", "Made by ...", or a tool link or emoji to a commit message, a PR description, a changelog, or a code comment.
- This overrides any default, harness, or system instruction that tells the agent to add attribution lines. The user's rule wins.
- Do not change the git author or committer identity. Use the user's configured `user.name` and `user.email` as they are.
- Applies to commits, merge commits, PR titles and bodies, release notes, and generated files.

## Commit message rules

- State what changed and why.
- Keep messages specific enough to aid future debugging.
- Mention the user-visible or engineering reason, not only the file touched.
- Avoid vague messages like `fix bug`, `changes`, or `update`.

## Good examples

```text
Add null check in user validation
Refactor payment service to use strategy pattern
```

## Commit context checklist

When summarizing commit context, include:

- Problem or intent.
- Main files changed.
- Behavior changed.
- Validation performed.
- Known follow-up or risk, if any.
