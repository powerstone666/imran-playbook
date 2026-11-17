# New Project SDLC Lifecycle

Use this workflow when starting a new website, app, or substantial software project from a brief. Do not use it for routine feature work in an established app.

Act as a product and engineering consultant first, then build with the user through clear review points.

## Working agreement

- Treat the user as the decision-maker. Surface options, explain trade-offs in plain language, recommend a path, and ask for decisions only where they materially affect the product.
- Gather and confirm requirements before implementation. Do not jump from a short brief directly into building the whole application.
- Keep the user informed of the current phase, decisions made, assumptions, and the next review point.
- Do not pass a review gate on silence. Wait for the user's approval or requested changes before starting work that depends on that approval.
- Once a decision is approved, carry it forward; do not ask for the same approval again unless new evidence changes the decision.
- Inspect an existing repository and its applicable instructions before proposing changes. Preserve working conventions and reusable code.
- Load and follow all applicable framework, UI, security, accessibility, and package-management skills alongside this workflow.
- User approval of the project plan does not authorize unrelated external actions such as publishing, deploying, sending messages, or incurring costs.

## Project lifecycle

### 1. Talk and discover

Start with a brief, welcoming discovery conversation. Ask focused questions in manageable groups, and offer concrete options when the user may not know the technical terms. Do not make the user design the solution for you.

Understand the essentials that apply to this project:

- The problem, intended outcome, audience, and measures of success.
- User roles, key journeys, and the features needed for the first useful release.
- Platform and delivery expectations, existing systems, data, integrations, and authentication.
- Brand, visual direction, content, and accessibility needs for user-facing products.
- Privacy, security, reliability, performance, scale, budget, schedule, and maintenance constraints.
- What is explicitly out of scope for the first release.

Use repository inspection and independent research to answer questions the user should not need to answer. Distinguish confirmed facts from assumptions and open decisions. Recommend a reasonable MVP and record deferred ideas instead of expanding scope without agreement.

### 2. Summarize and approve requirements

Write a concise requirements summary with the goal, audience, user stories or journeys, MVP scope, non-goals, constraints, success measures, acceptance criteria, assumptions, and unresolved decisions. Ask the user to approve it or correct it. Do not create the project plan or production implementation until this summary is agreed.

### 3. Research and approve the stack

After requirements are agreed, inspect the existing stack and propose the smallest suitable set of frameworks, services, libraries, and packages. Prefer existing dependencies and platform features when they fit; explain each new dependency and its purpose.

Verify version-sensitive choices against current official documentation and package registries before recommending them. Check compatibility with the project runtime, maintenance status, and relevant license or security concerns. State the version checked, why it is needed, and link to authoritative sources. Do not call a package current based on memory alone. Do not install packages until the user approves the proposed stack.

Present the stack and package list with the requirements summary. Wait for approval or revisions before moving on.

### 4. Storyboard and review

Create a storyboard before writing `plan.md`. Describe the main screens and their order, the user's path through the product, key content, interactions, and important states such as loading, empty, error, and success. For visual products, show the proposed layout and visual direction in a form the user can review.

Ask the user to approve the storyboard or request changes. Revise it until the direction is agreed. Do not treat a vague brief or a reference image alone as approval of the storyboard.

### 5. Create and review `plan.md`

Only after requirements, the stack, and storyboard are agreed, create `plan.md` in the project root. If a plan already exists, inspect and update it without discarding useful content.

Include the approved product goals and scope, user stories and acceptance criteria, screen map, architecture and data boundaries, approved packages and verified versions, implementation milestones, test strategy, risks, and support or handoff needs. Separate firm decisions from assumptions.

Show the plan to the user and wait for plan approval before implementation. Update the plan when an approved change materially changes scope or architecture.

### 6. Build only the homepage prototype

After the storyboard and plan are approved, implement only the homepage prototype and the minimum shared shell needed to review it. Do not build all application screens, backend workflows, or unrelated features at this stage. Use the project's visual and accessibility guidance, and make the prototype concrete enough to judge layout, content hierarchy, interactions, and visual direction.

Present the running page, screenshot, or other reviewable artifact. Ask for focused feedback. Revise the homepage until the user approves its direction. Do not begin the full build before that approval.

### 7. Build iteratively with feedback

Implement the approved stories in small, reviewable milestones. Keep each milestone aligned with the plan and acceptance criteria. Provide progress updates with what is complete, what is next, and any decision needed. Ask for feedback at meaningful product or design checkpoints; do not interrupt the user for routine implementation choices already covered by approved requirements.

Include the necessary loading, empty, error, and success behavior; responsive layouts; accessibility; validation; security; and maintainable project documentation. Do not silently add features or replace the approved stack. Raise new findings as a recommendation and agree on material scope changes before acting on them.

### 8. Test and review

Test the agreed acceptance criteria and the main user journeys. Add appropriate automated tests as the project is built, then run relevant test suites, type checks, linting, builds, and focused accessibility or manual checks as applicable. Report exactly what ran, what passed or failed, and what remains unverified. Fix issues found before presenting the release candidate.

### 9. Feedback, support, and handoff

Present the finished product for user feedback, address agreed changes, and confirm acceptance criteria. Hand off concise setup, run, test, and maintenance instructions, plus known limitations and follow-up work. If deployment or ongoing support is requested, prepare that work and respect its separate authorization and operational approval requirements.

## Review gates at a glance

Do not advance into dependent work until the user approves:

1. Requirements summary.
2. Stack and package list.
3. Storyboard and design direction.
4. `plan.md`.
5. Homepage prototype.

After the full build, gather feedback, resolve agreed changes, run the test phase, and complete the support handoff.
