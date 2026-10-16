# LangChain Basics

Use this for simple model calls and basic LangChain usage.

## Core imports and calls

- Import `ChatOpenAI` from `@langchain/openai` to configure a chat model.
- Read the model name, API key, and `baseURL` from env so OpenAI-compatible endpoints work:

```ts
const model = new ChatOpenAI({
  model: process.env.LLM_MODEL,
  apiKey: process.env.LLM_API_KEY,
  configuration: { baseURL: process.env.LLM_BASE_URL },
});
```

- Use `invoke` for model calling.
- Use tools to define custom functions.
- For stdin/stdout CLIs, use `node:process` with `createInterface` from `node:readline`.

## Manual vs autonomous

Manual LangChain usage includes direct model invocation, prompts, pipelines, parsers, and custom formatting.

Autonomous agents use `createAgent` and tool-aware message flows.
