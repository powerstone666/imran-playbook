# Naming

Use this when naming variables, functions, files, constants, types, or abstractions.

## Rules

- Name by domain meaning, not implementation detail.
- Prefer descriptive nouns and verbs over abbreviations.
- Rename aggressively when behavior evolves.
- If a comment is required to explain a variable, improve the name.
- Replace unexplained literals with named constants.
- Keep domain constants close to their usage boundary.

## Examples

Readable boolean:

```ts
const isEligible = roles.includes("admin");
```

Avoid clever expressions:

```ts
const isEligible = !!~roles.indexOf("admin");
```

Meaningful variable:

```ts
let billingCycleDays: number;
```

Avoid:

```ts
let d: number;
```

Named constant:

```ts
const GST_RATE = 0.18;
const priceWithTax = price * (1 + GST_RATE);
```

Avoid:

```ts
const priceWithTax = price * 1.18;
```
