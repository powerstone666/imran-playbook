# Senior Developer Reference Index

Use this folder for writing code, code quality, maintainability, refactoring, review, and commit guidance.

## Route by task

| Task signal | Read |
| --- | --- |
| Starting any code change | `workflow.md` |
| Deciding which layer to change, or whether to reuse existing code instead of writing new code | `change-ladder.md` |
| Choosing class/OOP vs function/functional style | `class-vs-function.md` |
| Writing or refactoring functions | `functions.md` |
| Naming variables, functions, files, or abstractions | `naming.md` |
| Improving testability or side-effect boundaries | `testing.md` |
| Clean-code examples and anti-patterns | `maintainability.md` |
| Preparing commit message or commit context | `commits.md` |
| Code review or self-review / final quality pass | `../code-reviewer/index.md` |

Default for code changes: read `workflow.md` and `change-ladder.md`, then the most specific topic file. If the implementation introduces services, clients, processors, or reusable modules, also read `class-vs-function.md`.
