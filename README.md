# imran-playbook

An agent skill that teaches AI coding agents (Claude Code, Codex, and others) how I build software: a senior engineering workflow, code review, shared project memory, npm rules, Material Design 3 UI, Next.js structure, and LangChain/LangGraph patterns.

The agent reads one small router file, then loads only the topic files the current task needs, so it stays cheap on tokens.

## Install

```bash
npx skills add powerstone666/imran-playbook -g --all
```

- `-g` installs for your user account, so every project gets it.
- `--all` installs for every supported agent without prompting. To choose agents, use `-a <agent-names> -y` instead (see `npx skills add --help`).

## Update

```bash
npx skills update -g
```

## What's inside

| Area | Folder | Covers |
| --- | --- | --- |
| Engineering workflow | [`references/senior-dev/`](references/senior-dev/) | Scope mapping, smallest complete change, change ladder (which layer to touch), reuse before writing, functions, naming, testing, commits |
| Code review | [`references/code-reviewer/`](references/code-reviewer/) | Full review of a diff, branch, or PR with a numbered report, plus a quick self-review checklist |
| Project memory | [`references/memory/`](references/memory/) | A shared `knowledge.md` so different agents can hand off work and avoid editing the same files |
| Package installation | [`references/package-installation/`](references/package-installation/) | npm only, `@latest`, no new dependency for a few lines of code |
| UI design | [`references/ui-design/`](references/ui-design/) | Material Design 3, restrained Tailwind web UI without AI-slop, Pixel-style Android UI, accessibility, GSAP animation, Three.js 3D |
| Next.js | [`references/nextjs/`](references/nextjs/) | Version check, `app/` folder structure, API routes, UI-to-backend client boundary, prompts in `.txt` files |
| LangChain | [`references/langchain/`](references/langchain/) | Setup, prompts, parsers and Zod, agents, RAG with Pinecone, retriever tools |
| LangGraph | [`references/langgraph/`](references/langgraph/) | Graphs, state and reducers, routing and commands, subgraphs |

## How it works

```text
SKILL.md                     router: maps task signals to topic files
references/<area>/index.md   per-area routing table
references/<area>/<topic>.md the actual rules and examples
```

1. The agent loads [`SKILL.md`](SKILL.md) when a task matches its description.
2. It picks the smallest set of topic files from the routing table, for example `senior-dev/workflow.md` and `senior-dev/change-ladder.md` for any code change.
3. It follows those files as rules, then reports what changed, what it validated, and what it skipped.

Each rule lives in exactly one file; other files link to it instead of repeating it.

## Project memory across agents

For longer work, agents keep a `knowledge.md` at the project root:

- **Active**: who is working on what, and which files they are changing.
- **Facts**: one-line project gotchas every task should know.
- **Log**: one line per finished or paused task, linking to an optional session file.

Small tasks skip memory entirely. See [`references/memory/index.md`](references/memory/index.md).

## Customizing

Fork the repo and edit the topic files. Keep `SKILL.md` focused on routing, and add new topics as `references/<area>/<topic>.md` plus a row in that area's `index.md` and in the `SKILL.md` routing table.
