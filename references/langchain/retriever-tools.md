# LangChain Retriever Tools

Use this when exposing vector retrieval as an agent tool.

## Retriever tool

Use the retriever interface so agents can search knowledge directly.

```ts
import { createRetrieverTool } from "langchain/tools/retriever";

const knowledgeBaseTool = createRetrieverTool(retriever, {
  name: "knowledge_base",
  description: "Search company policies, documents and FAQs",
});
```

Use a clear tool name and description so the agent knows when to call it.
