# Material Design 3 Interaction And Accessibility

Use this for interaction behavior, states, motion, usability, and accessibility.

Official foundations reference: https://m3.material.io/foundations

## Interaction rules

- Every interactive element needs a visible state change.
- Use clear focus indicators for keyboard navigation.
- Keep primary actions easy to find.
- Avoid surprising navigation or hidden destructive actions.
- Show loading feedback for async actions.
- Show errors in context and make recovery clear.

## Motion

- Use motion to explain relationships and state changes.
- Keep motion brief and purposeful.
- Avoid motion that blocks the task.
- Respect reduced-motion preferences when implementing animations.

Motion reference: https://m3.material.io/styles/motion/overview

## Accessibility

- Ensure sufficient contrast for text, icons, and controls.
- Use semantic HTML when building web UI.
- Provide labels for form controls and icon-only buttons.
- Keep touch/click targets large enough for reliable interaction.
- Support keyboard navigation for interactive flows.
- Do not communicate meaning by color alone.

## Usability checklist

- Can the user identify the main task immediately?
- Can the user complete the task with keyboard only?
- Are loading, empty, error, and success states handled?
- Does the layout remain usable on mobile and desktop?
- Are destructive actions clearly labeled and reversible or confirmed when needed?
