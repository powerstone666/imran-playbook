# Testability

Use this when code needs tests, dependency boundaries, side-effect control, or safer validation.

## Rules

- Write testable code.
- Inject dependencies instead of constructing them inside business logic.
- Isolate side effects.
- Keep pure computation separate from I/O.
- Validate behavior with tests or reproducible checks.

## Dependency injection example

Prefer:

```ts
interface PaymentGateway {
  charge(input: { customerId: string; amount: number }): Promise<void>;
}

async function processPayment(
  input: { customerId: string; amount: number },
  gateway: PaymentGateway
) {
  await gateway.charge(input);
}
```

Avoid:

```ts
async function processPayment(input: { customerId: string; amount: number }) {
  const gateway = new StripePaymentGateway();
  await gateway.charge(input);
}
```

## Validation guidance

- For narrow code changes, run focused tests or type checks.
- For user-facing workflows, validate the actual workflow.
- For refactors, verify behavior did not change unless the task requires it.
- New non-trivial logic (a branch, a loop, a parser, money or security code, or a whole new script or app) leaves at least one small test or assert-based self-check. Code without its check is unfinished. Trivial changes need none.
