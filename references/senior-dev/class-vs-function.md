# Class vs Function

Use this when deciding between object-oriented code and function-based code.

## Default rule

Choose the simplest shape that matches the problem.

- Use functions for stateless logic, small wrappers, data transforms, validators, mappers, and one-off utilities.
- Use classes for stateful services, grouped behavior with shared dependencies, complex workflows, lifecycle management, or implementations that benefit from an interface.
- Do not force OOP everywhere.
- Do not force functional style when the module is clearly a service with dependencies and multiple related operations.

## Use functions when

- The behavior is standalone.
- There is no internal state.
- The function has a clear input and output.
- The logic is easy to test directly.
- The module is a small wrapper around one endpoint or utility.

Example:

```ts
type FormatPriceInput = {
  amount: number;
  currency: string;
};

export function formatPrice({ amount, currency }: FormatPriceInput) {
  return new Intl.NumberFormat("en-US", {
    style: "currency",
    currency,
  }).format(amount);
}
```

Simple API wrapper:

```ts
type CreateUserRequest = {
  name: string;
  email: string;
};

export async function createUser(request: CreateUserRequest) {
  const response = await fetch("/api/users", {
    method: "POST",
    headers: { "Content-Type": "application/json" },
    body: JSON.stringify(request),
  });

  if (!response.ok) {
    throw new Error("Failed to create user");
  }

  return response.json();
}
```

## Use classes when

- Multiple methods share the same dependencies.
- The service needs configuration, injected clients, cache, state, or lifecycle.
- The behavior belongs to one cohesive domain concept.
- The implementation needs an interface for tests or replacement.
- The workflow has multiple related steps that should not be scattered across unrelated functions.

Example:

```ts
interface PaymentGateway {
  charge(input: { customerId: string; amount: number }): Promise<void>;
}

interface ReceiptSender {
  send(input: { customerId: string; amount: number }): Promise<void>;
}

export class BillingService {
  constructor(
    private readonly paymentGateway: PaymentGateway,
    private readonly receiptSender: ReceiptSender
  ) {}

  async chargeCustomer(input: { customerId: string; amount: number }) {
    await this.paymentGateway.charge(input);
    await this.receiptSender.send(input);
  }
}
```

## Frontend/backend boundary

In Next.js projects, UI components call backend routes through a typed API client, never backend services directly. See `references/nextjs/ui.md`.

## Decision checklist

- If it only transforms data, use a function.
- If it coordinates dependencies, consider a class.
- If it has multiple related public operations, consider a class.
- If there is no shared dependency or state, prefer functions.
- If tests need to swap implementation behind an interface, classes or injected objects are often clearer.
- If a module starts as functions and grows into a cohesive service, refactor into a class.
