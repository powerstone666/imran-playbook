---
name: imran-playbook
description: Use this skill for Imran's preferred engineering workflow, coding style, project memory process, JavaScript package installation rules, UI design with Google Material Design 3 or Pixel-style Tailwind web UI, Next.js app structure, LangChain/LangGraph implementation notes, code review, and senior clean-code maintainability rules. Trigger when working in Imran's projects, changing code, reviewing a diff or PR, designing UI, applying Material Design 3, avoiding generic AI-generated web UI, adding GSAP animation or Three.js 3D, installing JS/TS packages, building Next.js apps, adding AI agent/RAG workflows with LangChain or LangGraph, or when the user asks to follow Imran's playbook or approach.
metadata:
  short-description: Imran's engineering playbook and reference router
  version: "1.2.0"
  owner: imran
  reference-root: references/
---

# Imran Playbook

This skill is the entry point for Imran's preferred way of building software.
Use it as a router: read this file first, identify the task domain, then load only the smallest set of topic files that covers the task.

When a reference's trigger matches the task, it is a rule, not a suggestion. When this skill is active and another installed skill covers the same topic (for example general clean-code, code review, or frontend design skills), this skill's references win.

## Core Prompt

When this skill is active:

1. Inspect the task, repo context, and technology enough to identify the domain and existing conventions.
2. Select the smallest relevant set of topic files from the routing table below.
3. Read each selected file completely before implementing; do not skim it.
4. Follow the selected references as task rules, not as loose inspiration.
5. Preserve existing project conventions unless a selected reference explicitly says it overrides them.
6. Implement the smallest coherent change at the outermost layer that solves it correctly (`references/senior-dev/change-ladder.md`).
7. Validate with tests, type checks, builds, or focused manual checks whenever practical.
8. Report what changed and what was validated, then end with one or two lines: what you skipped or did not check, and any risk the user must know.

## Reference Routing Table

| Task signal | Read first | Also read when relevant | Use for |
| --- | --- | --- | --- |
| Any code change, refactor, bug fix, or feature | `references/senior-dev/workflow.md`, `references/senior-dev/change-ladder.md` | The matching file from `references/senior-dev/index.md` | Senior engineering workflow, scope mapping, layer choice, reuse before writing, maintainable implementation |
| Choosing OOP/classes vs functional style | `references/senior-dev/class-vs-function.md` | `references/senior-dev/functions.md`, `references/senior-dev/testing.md` | Classes for cohesive services, functions for stateless logic |
| Function design, parameters, return shape, nesting | `references/senior-dev/functions.md` | `references/senior-dev/testing.md` | Small functions, early returns, object parameters and returns |
| Naming, constants, magic values | `references/senior-dev/naming.md` | `references/senior-dev/maintainability.md` | Domain naming and readable constants |
| Commit message or commit context | `references/senior-dev/commits.md` | — | Specific commit summary, changed files, validation, risks |
| Code review: a diff, branch, or PR, or a self-review / final quality pass on your own change | `references/code-reviewer/index.md` | `references/code-reviewer/report-template.md` for full reviews | Full review with validation and a report, or a quick self-review checklist |
| Long, risky, multi-step, or resumed work, or a repo shared with other agents | `references/memory/index.md` | — | Shared `knowledge.md` for handoffs and cross-agent collaboration |
| JavaScript or TypeScript package installation | `references/package-installation/npm.md` | Relevant framework topic file | npm only, `@latest`, `--legacy-peer-deps` only after peer conflicts |
| Any UI design, visual polish, or component styling | `references/ui-design/material-design-3.md` | `components.md`, `layout.md`, `visual-system.md`, `interaction-accessibility.md` (motion and GSAP animation) in `references/ui-design/` | Material Design 3 principles, components, layout, visual system, accessibility |
| Web UI (HTML/Tailwind), including Pixel-inspired web UI or AI-slop prevention | `references/ui-design/material-design-3.md`, then `references/ui-design/material-3-web.md` | The matching UI topic file | Restrained Material 3 web UI, Tailwind tokens, root product showcase |
| 3D in web UI: Three.js, WebGL, model viewers, 3D scenes | `references/ui-design/threejs.md` | `references/ui-design/interaction-accessibility.md` for GSAP UI animation | When 3D belongs, Three.js skills, Next.js cleanup, performance, accessibility |
| Android app UI, Material You, Material 3 Expressive, or a web mockup of an Android screen | `references/ui-design/material-design-3.md`, then `references/ui-design/pixel-android.md` | `components.md`, `visual-system.md` | Pixel Android visual direction, rounded surfaces, pill controls |
| Next.js app or App Router work | `references/nextjs/version-check.md`, `references/nextjs/structure.md` | The matching file from `references/nextjs/index.md` | Version-sensitive Next.js coding and folder structure |
| LangChain setup, model calls, prompts, parsers, agents, RAG | `references/langchain/index.md` | The matching topic file from that index | LangChain topic routing |
| LangGraph graphs, state, reducers, routing, commands, subgraphs | `references/langgraph/index.md` | The matching topic file from that index | LangGraph topic routing |

## Selection Rules

- If the repo reveals a framework after inspection, load its matching topic file before making related edits.
- If the task spans multiple domains, load the small set that covers all of it. Example: a Next.js RAG route loads `nextjs/version-check.md`, `nextjs/structure.md`, `nextjs/api-routes.md`, `nextjs/prompts-config.md`, `langchain/rag-pinecone.md`, `senior-dev/workflow.md`, and `senior-dev/change-ladder.md`.
- Use memory files only when durable context is useful. Do not block small tasks on `knowledge.md` or session-file ceremony.
- If no domain reference matches, use `references/senior-dev/workflow.md` as the default engineering guide.

## Maintaining This Skill

The topic files are the source of truth for detailed guidance. Each rule lives in exactly one file; other files link to it instead of restating it. Keep examples and long-form rules in focused files under `references/<domain>/`, and keep `SKILL.md` focused on routing and operating behavior. Do not prune reference content unless the user asks, and do not create `full.md` archive files.
