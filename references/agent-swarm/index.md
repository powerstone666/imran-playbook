# Agent Swarm

The main (big) model should think with code context in hand, not spend its context collecting that context. When a task needs more reading than a few targeted lookups, launch a swarm of small, cheap models to explore in parallel, then reason over their results. When the change itself is large and splits cleanly, the same swarm can edit in parallel after the main model has set the plan.

## When a swarm is required

The swarm is not optional when any of these is true. Do not judge by how big the repo feels; judge by how much you would have to read.

- The request is to read, summarise, map, or audit **more than 8 files or about 1,000 lines**, or it says "every file", "whole repo", "the repo", or "the codebase".
- You would run **many repeated reads, greps, or diffs** to answer one question.
- It is **research** across several areas (how does X work, where is Y used, what are the options for Z).
- It is a **large change or refactor** touching many files or layers, or a **feature request** where the design is not obvious.

A small documentation repo still counts. File count and lines read decide it, not the kind of repo.

Skip the swarm only when the task is truly small: a one-file fix, a rename, a small edit in files you already know, or a question that one or two lookups answer.

## Swarm check (do this before the first read)

Before you read anything for a task like this, write one line: `Swarm: yes, because <reason>` or `Swarm: no, because <reason>`. Count the files and lines first if you are unsure. Say it every time, so the choice is never made silently.

If you are unsure, use the swarm. A swarm that was not needed costs a little; reading everything yourself costs your whole context.

## How to run it

1. **Split the question** into 2 to 5 independent angles (for example: data flow, existing helpers to reuse, tests and callers, risks, alternative designs). Each angle is one worker with its own role (see Give every worker a role). Fewer angles beat many overlapping ones.
2. **Pick the worker model from what is available.** Do not assume a model name. Look at the models this session offers (the `model` options on the `Agent` tool, or any the user names) and choose the smallest, cheapest one that can read code and follow a brief (in plain terms, the cheapest model that can still read files and report back). Prefer a smaller model over a larger one whenever the angle is only reading and reporting. If only one model is available, use it.
3. **Launch workers in parallel** in a single message with the `Agent` tool, passing the chosen model. Use the read-only `Explore` agent type for pure reading; use `general-purpose` when the worker needs skills or must run commands. In the research phase workers never edit files.
4. **Brief each worker fully**, because it sees nothing else: the goal, the one angle it owns, the files or areas to start from, what you already know or ruled out, and the exact shape of the answer (short, with `file_path:line` references, facts separated from guesses).
5. **Give workers the skills.** Name the skills they should invoke for their angle (for example the matching framework or `imran-playbook` topic skills) so their findings follow the same rules you will code with. Tell them to read the relevant reference files, not to skim.
6. **Let them debate when the design is open.** For a decision, give two workers opposing positions (for example "argue for extending the existing helper" vs "argue for a new module"), or run a second round where a worker critiques the first round's answers. Keep it to one round of debate; stop when the options and trade-offs are clear.
7. **Gather, then think.** Read the workers' reports, check any claim that your change depends on by opening the cited lines yourself, resolve disagreements, and pick the design. The main model makes the decision and owns the plan.
8. **Implement.** The main model writes the plan first: the design, the shared interfaces and types, and which files each piece touches. Then choose:
   - **Small or tightly coupled change:** the main model edits it itself, using `../senior-dev/workflow.md`.
   - **Large change that splits into independent pieces:** launch parallel editing workers in a single message, one per piece, each with `general-purpose`. Give each worker the plan, its exclusive list of files, the interfaces it must match, the skills and reference files to follow, and the happy path it must not break. No two workers may touch the same file; if pieces overlap, merge them into one worker or do that part yourself. Pick the editing model by risk: a mid-size model is fine for mechanical, well-specified edits; keep subtle or cross-cutting logic with the main model.
9. **Integrate and verify.** After editing workers finish, the main model reads every diff, fixes mismatches at the seams between pieces, then runs the type check, tests, or build and confirms the happy path still works. Do not report done on a worker's word.

## Give every worker a role

A worker is never "an agent". Each one gets a named role that sets its angle, its skills, and what its report must contain. Pick roles from the task; examples:

- **Expert coder** for one language or layer: writes or plans the code for its piece.
- **Framework expert** (for example Next.js, LangGraph, Postgres): checks the design against that framework's rules and loads its skills.
- **Tester**: finds existing tests, edge cases, and how to prove the happy path still works.
- **Senior reviewer**: attacks a plan or diff for bugs, regressions, and scale problems.
- **Document reviewer**: reads docs, specs, and READMEs and reports what the code must satisfy.
- **Explorer / mapper**: finds callers, helpers to reuse, and the files a change must reach.
- **Devil's advocate**: argues the opposite design in a debate.

Put the role, in one line, at the top of the worker's brief, and match the skills you name to the role. Use the smallest model that can do that role (see step 2); a senior reviewer or expert coder may justify a larger one than an explorer.

## Ask the user when the shape is unclear

Do not guess the swarm. Use the `AskUserQuestion` tool, in one call, when any of these is true:

- The work is huge (many modules, many files, or several features at once).
- You cannot tell how many workers are needed.
- You cannot tell which roles or which models fit.

Offer your proposed team as the first option marked "(Recommended)" (for example "4 workers: mapper, Next.js expert, tester, senior reviewer, on the smallest model, editors on a mid-size model"), plus a smaller and a larger alternative. Skip asking when the task is clear and the swarm is small (2 to 3 read-only workers).

## Visualise it when the user should see it

For a decision, a debate, or any run where the user benefits from watching or comparing the workers, publish an HTML page with the `Artifact` tool and give the user the link.

- Load the `artifact-design` skill first (and `artifact-capabilities` if the page needs more than static content), then write the page and publish it.
- Show one lane or card per worker: its role, model, status (waiting, running, done), and its short result. For a debate, show the opposing positions side by side with the trade-offs and the final choice.
- Publish it as soon as the workers launch, with every worker marked running. Republish the same file path as reports arrive so the same link updates, and make the last version show the decision and why.
- If you are unsure whether the user wants this, ask with `AskUserQuestion` ("Do you want a visual page of the swarm running?") before launching. Do not publish unasked for a plain research swarm.

## Rules

- Research workers are read-only; only editing workers in step 8 write files, and only inside the files they were given.
- Workers are cheap but wrong sometimes. Treat reports as leads, not facts, until the lines are verified.
- Do not ask workers to return whole files or long dumps; ask for conclusions with references, so the main context stays small.
- Do not re-run in the main context the searches a worker already did.
- Say in one line in your reply that you used a swarm, and what each worker covered.
