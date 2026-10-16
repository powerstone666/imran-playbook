# Google Material Design 3

Use this when designing or implementing UI with Google Material Design 3 principles. Read it first for any UI work.

## Official references

- Material Design 3 home: https://m3.material.io/
- Foundations: https://m3.material.io/foundations
- Styles: https://m3.material.io/styles
- Components: https://m3.material.io/components

If a task needs exact component specs, states, tokens, or platform details, consult the official Material Design 3 website first. Topic files link to the specific style pages.

## Core approach

- Build with a clear hierarchy: important actions and content should be visually obvious.
- Use familiar Material components instead of inventing custom controls.
- Prefer consistent spacing, shape, color roles, typography roles, and interaction states.
- Use design tokens where the project supports them.
- Keep UI practical and readable before making it decorative.
- Make every interactive state explicit (full checklist in `components.md`).

## Material 3 priorities

- Use color roles, not random colors.
- Use typography roles, not one-off font sizes.
- Use shape consistently across related surfaces.
- Use elevation to communicate surface hierarchy, not decoration.
- Use motion to explain state changes, not to distract.
- Support responsive layouts (see `layout.md`).

## Implementation habit

Before creating a custom UI element, ask:

- Is there a Material component for this?
- What state variants does it need?
- What is the primary action?
- What content must remain scannable?
- Does the layout work on mobile and desktop?
