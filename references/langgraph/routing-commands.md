# LangGraph Routing And Commands

Use this for conditional nodes, routing, loops, review flows, and command-based transitions.

## Conditional nodes

Use conditional edges when a graph needs to route by state.

```ts
async function conditionalRoute(state: State) {
  if (state.question.includes("refund")) {
    return { route: "refund" };
  }

  return { route: "orders" };
}

const graph = new StateGraph(GraphState)
  .addNode("router", conditionalRoute)
  .addNode("refund", refundNode)
  .addNode("orders", ordersNode)
  .addEdge(START, "router")
  .addConditionalEdges("router", (state) => state.route, {
    refund: "refund",
    orders: "orders",
  })
  .addEdge("refund", END)
  .addEdge("orders", END);
```

## Commands

Use commands when routing and state updates should happen together, especially loop-back flows. Import `Command` from `@langchain/langgraph`.

Example: a review agent sends work back to research until quality passes.

```ts
async function researcherNodeWithFeedback(state: State) {
  const result = await model.invoke([
    [
      "system",
      `Do research once again based on existing research: ${state.researcher} feedback: ${state.qualityReviewer}`,
    ],
    ["user", state.question],
  ]);

  return new Command({
    update: { researcher: result.content as string },
    goto: "reviewer",
  });
}
```

When a node uses possible destinations, declare `ends`:

```ts
.addNode("reviewer", qualityReviewerNode, {
  ends: ["researcherWithFeedback", "writer"],
})
.addNode("researcherWithFeedback", researcherNodeWithFeedback, {
  ends: ["reviewer"],
});
```
