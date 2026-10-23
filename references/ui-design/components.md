# Material Design 3 Components

Use this when choosing or styling UI components.

Official component reference: https://m3.material.io/components

## Component selection

- Use the project's existing components first, then Material components, then custom ones. A house component beats a native widget.
- Use buttons for clear actions.
- Use icon buttons for compact tool actions. Icons and chips follow `icons-and-labels.md`.
- Use text fields for free-form input.
- Use menus for option sets.
- Use segmented buttons or tabs for switching modes/views.
- Use checkboxes, switches, or radio buttons for selection controls.
- Use cards for grouped repeated content, not as a default wrapper for every section.
- Use dialogs only when the user must make a focused decision.
- Use snackbars for brief, non-blocking feedback.

## Button guidance

- Primary action should be visually strongest.
- Secondary actions should be lower emphasis.
- Destructive actions need clear wording and state.
- Buttons need the interactive states in the checklist below.

## Button rules (always apply)

- **Loading is compulsory.** Any button that starts async work (submit, save, fetch, navigate to a slow page) shows a loading state: a spinner or progress indicator in the button, the label kept or changed ("Saving"), the button disabled and `aria-busy="true"`, and a guard so a second click cannot fire the action twice. Every page or route that loads data also has its own loading state (skeleton or progress, such as `loading.tsx` in Next.js), as well as empty and error states.
- **Pointer cursor.** Every clickable button and link-like control uses `cursor-pointer`; disabled buttons use `cursor-not-allowed`. Tailwind v4 resets buttons to the default cursor, so set it explicitly in the base button style.
- **Bouncy press, the Material 3 Expressive way.** On press, the button reacts with a quick spring: it scales down slightly and its shape morphs (for example corners tighten or round), then it springs back with a small overshoot. Put it in the shared button component, not in each button. Use a CSS transition with a spring-like easing (`cubic-bezier(0.34, 1.56, 0.64, 1)`, 150 to 250 ms) for plain cases, or the project's animation library for a true spring. Keep it small (scale about 0.95 to 0.98), and turn it off under `prefers-reduced-motion`.
- **Dual tone by default.** Every button has two tones: its normal colour and a different colour on hover, with a short colour transition (about 150 ms). Use the colour roles for both, for example primary changes to a deeper or lighter primary tone, and a tonal or outlined button fills with its container colour. Keep focus and pressed states visibly distinct from hover. Skip this only when the project already uses single-tone buttons or the user asks to avoid it.

## Form guidance

- Labels must remain clear.
- Validation errors should be close to the field.
- Helper text should reduce ambiguity.
- Do not hide required context inside placeholders only.

## State checklist

This is the single interactive-state checklist; other UI files refer to it. For each interactive component, consider:

- Default.
- Hover.
- Focus.
- Pressed.
- Selected.
- Disabled.
- Loading.
- Error, when applicable.
