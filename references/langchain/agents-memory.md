# LangChain Agents And Memory

Use this for autonomous agents and conversation history.

## Creating agents

Use `createAgent` provided by LangChain.

```ts
const agent = createAgent({
  model,
  systemPrompt,
  tools: [],
  responseFormat, // use only if the model supports it
});
```

Invoke:

```ts
const res = await agent.invoke({
  messages: [{ role: "user", content: input }],
});
```

Print only the useful final content:

```ts
const finalOutput = res.messages[res.messages.length - 1].content;
```

Validate output with Zod when safety matters. Type-check before parsing; only parse strings when the schema expects a string.

## Conversation history

- Agents are stateless by default.
- They have short-term memory only for the messages you pass.
- Store conversation history manually when the app needs continuity.

Common strategies:

- Store messages in an array and pass them each turn.
- Trim or summarize history after it grows beyond useful limits.
- Store long-term context in a vector DB or database.
- LangGraph adds built-in persistence through checkpointers (see `../langgraph/index.md`). Plain `createAgent` usage without a checkpointer needs one of the manual strategies above.
