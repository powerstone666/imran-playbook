# LangChain Prompts

Use this when creating or refactoring prompts.

## Prompt options

LangChain prompts can be handled in three common ways:

1. Direct prompt inside `agent.invoke`.
2. `ChatPromptTemplate` from `@langchain/core/prompts`.
3. Structured message classes from `@langchain/core/messages`.

## ChatPromptTemplate

- Use `fromTemplate` for a single prompt.
- Use `fromMessages` for an array of prompt messages.
- Prefer prompt formatting with `prompt.invoke(variables)`.

## Message classes

For better segregation:

```ts
import { SystemMessage, HumanMessage, AIMessage } from "@langchain/core/messages";
```

Use clear message categories:

```ts
[
  new SystemMessage(""),
  new HumanMessage(""),
  new AIMessage("history message")
]
```
