# Maintainability

Use this for clean-code principles, examples, and anti-patterns.

## Optimize for the next developer

Code is read far more than it is written. Write code your future self can understand months later without extra context.

- Reduce hidden assumptions.
- Make intent obvious.
- Minimize cognitive load.
- Prefer clarity over shortcuts.

## DRY with judgment

- Extract shared logic once duplication is real.
- Avoid premature abstraction for coincidental similarity.

Prefer:

```ts
function applyDiscount(price: number, rate: number) {
  return price - price * rate;
}
```

Avoid duplicated intent:

```ts
function priceAfterDiscountA(p: number) {
  return p - p * 0.1;
}

function priceAfterDiscountB(p: number) {
  return p - p * 0.1;
}
```

## Composition over inheritance

- Compose behaviors through interfaces and injected collaborators.
- Use inheritance only for true is-a relationships.

Prefer:

```ts
interface Notifier {
  notify(message: string): void;
}

class OrderService {
  constructor(private notifier: Notifier) {}

  placeOrder() {
    this.notifier.notify("Order placed");
  }
}
```

Avoid:

```ts
class EmailNotifier extends Order {}
```

## Comments

Code explains what. Comments should explain why.

Prefer:

```ts
// Retry once to handle transient network failures
retryOnce(request);
```

Avoid:

```ts
// Create a new user
const user = new User();
```

## Known shortcuts

A shortcut with a known limit gets a one-line comment in this form: `shortcut: <the limit>, <when to upgrade>`.

```ts
// shortcut: loads all rows in memory, switch to pagination past ~10k orders
const orders = await db.order.findMany();
```
