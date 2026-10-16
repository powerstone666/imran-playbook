# LangGraph State And Reducers

Use this for state, annotations, message state, and reducers.

## Reducers

Normal state updates override existing values.

For arrays, multi-agent responses, or accumulated outputs, use reducers to stack updates.

```ts
answer: Annotation<string[], string | string[]>({
  default: () => [],
  // concat accepts a single item or an array, so updates never nest
  reducer: (current, update) => current.concat(update),
});
```

## MessagesAnnotation

Use `MessagesAnnotation` when storing message history.

It includes AI, system, and human messages.

Use spread syntax when adding custom variables:

```ts
const graphState = Annotation.Root({
  ...MessagesAnnotation.spec,
  question: Annotation<string>(),
});
```

Or use it directly:

```ts
const workflow = new StateGraph(MessagesAnnotation);
```
