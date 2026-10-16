# Project Memory

Shared memory any agent (Claude, Codex, opencode, ...) can read and write, so work survives the chat and agents can hand off to each other. Keep it cheap: one small file read at start, a few lines written at the end.

## When to use

Use for multi-step or risky work, work that continues a previous session, or repos where several agents work. Skip for small edits, quick questions, and anything the final reply already covers. Never block a task because memory is missing or stale.

## Files

Both live at the project root, unless the project already keeps them elsewhere.

- `knowledge.md`: the only file every agent reads. Keep it under ~100 lines.
- `sessions/YYYY-MM-DD-<agent>-<task>.md`: optional detail for one multi-step task. `<agent>` is the lowercase agent name (`claude`, `codex`, `opencode`).

## `knowledge.md` format

```md
# Project Knowledge

## Active
- 2026-10-16 claude | auth refactor | area: app/api/(services)/auth/ | sessions/2026-10-16-claude-auth-refactor.md

## Facts
- Pinecone index uses 1536-dim embeddings; match the embedding model.

## Log
- 2026-10-15 codex | upload route | done | added size limit, tests in app/api/upload/ | sessions/2026-10-15-codex-upload-route.md
```

- **Active**: who is working on what right now, and which files or folders they are changing.
- **Facts**: durable project knowledge and gotchas that any task benefits from. One line each; delete facts that become wrong.
- **Log**: one line per finished or paused task, newest first. Older than ~30 lines: delete the oldest; their session files keep the detail.

## Session file format

Only for work that spans many steps or may be resumed by another agent:

```md
# <task> (<agent>, YYYY-MM-DD)

Status: in progress | paused | done
Goal:
Decisions:
Files touched:
Next steps:
```

Record decisions, gotchas, and next steps only. Do not log commands run, files read, or anything visible in git.

## Flow

1. **Start:** read `knowledge.md`. Open a session file only if a Log or Active line is clearly relevant.
2. **Check for overlap:** if another agent's Active line covers files you need, do not edit them; tell the user and ask how to proceed.
3. **Claim:** for multi-step work, add your Active line (and session file, if useful).
4. **Finish or pause:** remove your Active line, add a Log line, add any new Facts. If unfinished, set `Status: paused` and fill `Next steps` so any agent can resume.

## Collaboration rules

- Edit only your own Active line, Log lines, and session files. Add Facts freely; fix a wrong Fact only when you verified it.
- Write `knowledge.md` in small edits, never a full rewrite, so concurrent agents don't overwrite each other.
- To resume another agent's paused task, read its session file, then continue in it and note your agent name in `Decisions`.
- An Active line older than a day with no recent session update is probably stale; ask the user before taking over its files.
