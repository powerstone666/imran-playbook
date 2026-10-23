# Material 3 Web UI Rules

Use this when building or reviewing web UI that should follow Material Design 3 or a Pixel-inspired look with Tailwind CSS. Read `material-design-3.md` first. For a web page that mocks an Android phone screen, also read `pixel-android.md`.

Apply it to avoid generic AI-generated websites, overused gradients, glassmorphism, random cards, poor spacing, weak hierarchy, and inaccessible components.

## Core stack

- Use Tailwind CSS for styling.
- Use Radix UI, Ark UI, or native accessible components for behavior.
- Use a reputable icon library and the rules in `icons-and-labels.md`: matching icons, no text characters as icons, no default chips.
- Prefer semantic HTML.
- Use ARIA only when needed.

## Avoid AI-slop design

Do not use:

- Random purple/blue gradients.
- Glassmorphism.
- Excessive shadows.
- Generic SaaS hero sections.
- Floating blobs.
- Fake dashboards filled with made-up metrics that do not reflect the product.
- Oversized glowing buttons.
- Meaningless cards.
- Text characters (`->`, `+`, `✓`) or emoji as icons, one icon reused everywhere, and chips or pills on plain text.
- Inconsistent border radius.
- Low-contrast text.
- Cramped spacing (see density guidance in `layout.md`).
- "Modern and sleek" filler UI.

## Material 3 visual rules

Use:

- Soft but intentional rounded corners.
- Clear surface hierarchy.
- Restrained color.
- 4px/8px spacing rhythm.
- Readable typography.
- Large touch targets.
- Subtle state layers and the full state checklist in `components.md`.
- Accessible focus states.
- Purposeful motion only.

## Layout rules

Before coding, define:

1. Page purpose.
2. Primary user action.
3. Information hierarchy.
4. Navigation pattern.
5. Empty, loading, and error states.

## Tailwind style guidance

Prefer:

- `rounded-2xl`, `rounded-3xl`
- `p-4`, `p-6`, `gap-4`, `gap-6`
- `text-sm`, `text-base`, `text-lg`, `text-2xl`
- `bg-background`, `bg-surface`, `bg-primary`, `text-on-surface`

Avoid one-off arbitrary values unless required.

## First page rule

For new web UI projects, reserve the first page at `/` for the product showcase. In an existing project where `/` already has a purpose, keep it and ask before changing it. In Next.js this is `app/page.tsx` (see `nextjs/structure.md`).

When running locally, `localhost:3000` should open the showcase page. Use it to demonstrate the product, its primary workflow, and polished UI states.

The showcase page should:

- Make the product identity clear in the first viewport.
- Show the primary experience, not filler marketing.
- Include realistic previews of the actual product UI or workflow, using plausible data.
- Demonstrate empty, loading, error, and success states when relevant.
- Avoid generic hero copy and decorative sections that do not serve the product.

## Output behavior

When generating UI:

- Start with structure first.
- Build reusable components.
- Use design tokens.
- Explain only important design choices.
- Do not add decorative sections unless they serve the product.
