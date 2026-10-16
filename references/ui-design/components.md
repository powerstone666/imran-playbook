# Material Design 3 Components

Use this when choosing or styling UI components.

Official component reference: https://m3.material.io/components

## Component selection

- Use the project's existing components first, then Material components, then custom ones. A house component beats a native widget.
- Use buttons for clear actions.
- Use icon buttons for compact tool actions.
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
