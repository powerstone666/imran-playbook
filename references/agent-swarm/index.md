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

## Cross-agent bridge (only when it earns its place)

If the `crossagentbridge` MCP tools are present in this session, other agents (other models or tools, running outside this session) can join a swarm as workers. The bridge is an escape hatch for swarm work, not the default way to run one.

**Use it only when one of these is true:**

- The user asked for it, or named another agent.
- The task is too heavy for the in-session swarm: the work needs more parallel hands than the session's own models give, or it is something this session's models cannot do or reason about well and another agent is better at.
- Your own context is running low and the remaining reading or editing can be handed off.

**Do not use it** on every swarm, for small swarms, or because the tools happen to exist. The ordinary swarm above is the first choice. If the MCP tools are absent, skip this section and carry on without it.

**Treat bridged agents as ordinary workers.** A bridged agent is a worker like a Haiku explorer: it gets a named role, a full brief, an exclusive file list if it edits, and its report is a lead to verify, not a fact. No special trust, no special ceremony, no extra approval steps because it came over the bridge. Use the bridge's room, task, and file-claim tools only as far as needed to hand out the work and stop two workers touching the same file.

**Bridged agents can run their own swarms.** They are often specialised frontier models with their own sub-agents. When work is handed to one (because the user asked, or the task is too heavy for this session), do not make it do the whole piece alone in one thread. In the brief, tell it to:

- Split its piece into independent angles and spawn its own sub-agents to work them in parallel, as evenly as the work allows, using the cheapest model it has that can do each role.
- Load and follow the imran-playbook skill, and pass the same instruction to every sub-agent it spawns. Every agent in the swarm, here or across the bridge, has the playbook, so they all work to the same rules (this file, `../senior-dev/workflow.md`, the UI and package rules).
- Keep its sub-agents inside the piece and the exclusive file list it was given; no two agents touch the same file.
- Return conclusions with `file_path:line` references, not dumps, with facts separated from guesses.

**How to handle other frontier models.** They are peers in capability, not subordinates, but in this swarm they are still workers. Give them the goal, the boundaries, and the shape of the answer, then let them choose how to do it inside those. Do not micromanage their method or re-explain what the playbook already says; point to it. Expect different habits and strengths from different models, so do not assume one agent's report matches another's format. Fix that by stating the answer shape in the brief, and verify the cited lines yourself before relying on anything. Disagreement between two strong agents is a debate to resolve with evidence, not something to settle by deferring to either.

**Hand off side requests so you stay on task.** If you are mid-task and the user asks for something on the side (review this diff, run the tests, check a second question), do not drop your work and do not spend your context on it. When the bridge is present, hand it to a bridged agent with a full brief (the goal, the files, the answer shape) and carry on. Good fits are reviews, test and build runs, and read-only checks. Keep the main thread on the main task, and fold the result in when it arrives. If the side request changes the plan itself, that is yours to decide, not the worker's.

**Do the handshake first.** The bridge has setup steps before an agent can take work: check which agents are online (`list_agents`), set up or join a room, invite the agent, and read the room onboarding and setup the bridge returns. Before inviting, check whether the agent is already available: already a member of the room (`list_room_members`) or already online and ready. If it is, do not invite it again; use it as it is. Invite only agents that are missing. Let the steps finish and follow what the bridge asks for. Do not skip them or send work to an agent that has not joined. Handing off before the handshake completes means the work goes nowhere. While it completes, keep working on your own part.

**Use the agents that are there, efficiently.** Up to three bridged agents may be available. Match them to the work instead of defaulting to a count:

- **Look first.** See who is online and what each is good at before assigning anything.
- **One agent** is right when there is a single separable piece, such as one review or one test run. Do not leave capable agents idle when the work clearly splits.
- **Two or three agents** are right only when the work has that many independent pieces with different roles (for example reviewer, tester, mapper), each with its own files or question.
- **Never bombard.** Do not send the same task to all of them, split a small task three ways, or give agents overlapping scope. More agents means more reports to verify and more seams to integrate, so each one must own a distinct piece.
- **Match strength to role.** Give each agent the piece it is best at. If two are equally suited, give the larger or riskier piece to the stronger one, and keep the others on lighter pieces.

**Never block on it.** After handing work over, continue your own part of the task. Do not sit waiting for a bridged worker; collect its report when it arrives and fold it in. If a worker is slow or silent, finish without it or take that piece yourself, and say so.

## Rules

- Research workers are read-only; only editing workers in step 8 write files, and only inside the files they were given.
- Workers are cheap but wrong sometimes. Treat reports as leads, not facts, until the lines are verified.
- Do not ask workers to return whole files or long dumps; ask for conclusions with references, so the main context stays small.
- Do not re-run in the main context the searches a worker already did.
- Say in one line in your reply that you used a swarm, and what each worker covered.
