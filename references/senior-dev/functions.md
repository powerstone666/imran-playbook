# Functions

Use this when writing, splitting, or refactoring functions.

## Function shape

- Keep functions small and focused.
- Make each function do one clear job.
- Split functions that need "and then" in their description.
- Prefer early returns to deep nesting.
- Guard invalid states up front.
- Keep the happy path linear and short.

## Parameters and return values

- Avoid long parameter lists.
- Group related inputs into typed objects.
- Let function signatures communicate cohesive abstractions.
- Use objects for multi-value returns: `{ model, contextSize }`, not `[model, contextSize]`.

Example:

```ts
interface RegisterUserRequest {
  name: string;
  email: string;
  country: string;
  marketingOptIn: boolean;
}

function registerUser(request: RegisterUserRequest) {}
```

## Control flow example

Prefer:

```ts
if (!user) return;
if (!user.isActive) return;
if (!hasAccess(user)) return;

process(user);
```

Avoid:

```ts
if (user) {
  if (user.isActive) {
    if (hasAccess(user)) {
      process(user);
    }
  }
}
```
