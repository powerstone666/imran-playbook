# LangGraph Subgraphs

Use this when a workflow becomes too large for one graph or a domain should have its own internal flow.

## When to use

Use subgraphs when:

- A node would become a complex monolith.
- A domain has its own workflow, state, tools, or database.
- A main graph should route to a specialized workflow.

## Main graph

```ts
import { START, END, Annotation, StateGraph, MessagesAnnotation } from "@langchain/langgraph";
import { app } from "./subgraph.js";

const mainState = Annotation.Root({
  ...MessagesAnnotation.spec,
  question: Annotation<string>(),
  answer: Annotation<number>(),
});

const graph = new StateGraph(mainState)
  .addNode("calculation", app)
  .addEdge(START, "calculation")
  .addEdge("calculation", END);

const agent = graph.compile();
```

## Subgraph

```ts
import { START, END, Annotation, StateGraph, MessagesAnnotation } from "@langchain/langgraph";

const subgraphState = Annotation.Root({
  ...MessagesAnnotation.spec,
  question: Annotation<string>(),
  answer: Annotation<number>({
    reducer: (current, update) => current + update,
  }),
});

type State = typeof subgraphState.State;

async function addNode(state: State) {
  return { answer: 2 + 2 };
}

async function multiplyNode(state: State) {
  return { answer: state.answer * 2 };
}

const graph = new StateGraph(subgraphState)
  .addNode("addition", addNode)
  .addNode("multiply", multiplyNode)
  .addEdge(START, "addition")
  .addEdge("addition", "multiply")
  .addEdge("multiply", END);

export const app = graph.compile();
```

LangGraph automatically updates matching state keys between main graph and subgraph. If a subgraph returns state not defined in the main graph, the main graph ignores it.
