# NPM Package Installation

Use this whenever working in the JavaScript or TypeScript ecosystem.

## Before installing

- Check whether an installed dependency, the platform, or the codebase already does the job (see the reuse ladder in `../senior-dev/change-ladder.md`).
- Never add a dependency for something a few lines of code can do.

## Rules

- Always use `npm`.
- Do not use `yarn`, `pnpm`, or `bun` for package installation.
- Always install packages with `@latest`.
- Do not hardcode package versions in install commands.
- Do not manually pin package versions unless the user explicitly asks for a specific version.
- Let `npm` update `package.json` and lockfiles.

## Install command pattern

Use:

```bash
npm install <package>@latest
```

For multiple packages:

```bash
npm install <package-a>@latest <package-b>@latest
```

For dev dependencies:

```bash
npm install -D <package>@latest
```

## Peer dependency failures

If the install fails because of peer dependency conflicts, retry with:

```bash
npm install <package>@latest --legacy-peer-deps
```

For dev dependencies:

```bash
npm install -D <package>@latest --legacy-peer-deps
```

Use `--legacy-peer-deps` only after a dependency resolution failure or when the existing project already requires it.

## Avoid

Do not write:

```bash
npm install package@1.2.3
```

Do not switch package managers to work around dependency issues.
