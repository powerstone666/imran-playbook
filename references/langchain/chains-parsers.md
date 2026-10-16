# LangChain Chains, Parsers, And Zod

Use this when chaining model calls or enforcing structured output.

## Pipelines

Pipelines are useful when chaining multiple functions together.

Example pattern:

```ts
const chain = prompt.pipe(model).pipe(parser);
```

This avoids writing a separate parsing function after model invocation.

## Parsers

- `JsonOutputParser` returns JSON-like output.
- `StringOutputParser` returns a string.
- `CommaSeparatedListOutputParser` converts comma-separated values into a list.
- `withStructuredOutput(zodSchema)` uses a custom Zod schema.

## Zod

Zod enforces strict model output.

```ts
const ProductSchema = z.object({
  id: z.number().describe("Product ID, if known").nullable().optional(),
  title: z.string(),
  price: z.number(),
  review: z.array(z.string()),
});
```

Note: OpenAI-compatible models such as DeepSeek may not support every OpenAI-specific structured output feature. Use native endpoints or compatible model features when needed.
