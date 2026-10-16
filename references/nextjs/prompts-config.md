# Next.js Prompts And Config

Use this when adding prompts, LLM instructions, JSON config, PDFs, or static configuration.

## Prompt rule

All LLM prompts must be in separate `.txt` files.

Never hardcode prompts in TypeScript or JavaScript code.

Prompt files belong under:

```text
app/api/(prompts)/
```

## Config rule

Config files such as JSON, PDFs, and other static configuration files belong under:

```text
app/(config)/
```
