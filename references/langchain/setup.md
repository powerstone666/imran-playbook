# LangChain Setup

Use this for a TypeScript LangChain starter setup. Install commands follow `../package-installation/npm.md`.

## TypeScript core

```bash
cd <project-dir>
npm init -y
npm install -D typescript@latest @types/node@latest tsx@latest
npx tsc --init
```

Add a dev script:

```json
{
  "scripts": {
    "dev": "tsx watch src/index.ts"
  },
  "type": "module"
}
```

## LangChain starter dependencies

```bash
npm install langchain@latest @langchain/core@latest @langchain/openai@latest zod@latest
```
