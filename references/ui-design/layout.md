# Material Design 3 Layout

Use this for layout, spacing, density, and responsive structure.

Official foundations reference: https://m3.material.io/foundations

## Layout principles

- Use clear visual hierarchy.
- Group related controls and content.
- Keep scanning paths predictable.
- Align content to a consistent grid or spacing system.
- Avoid overcrowding dense screens; use spacing to separate meaning.
- Avoid oversized decorative layouts for operational tools.

## Cutout navbar and content width

The default navbar is the cutout navbar: inset from the screen edges (floating, with side margins and rounded corners), not a bar that touches the edges.

- The page body aligns to the cutout: same left and right edges, same max width. Put the navbar and the content in one shared container, or one shared width token, so they cannot drift apart.
- Use a full-width navbar only when the user explicitly asks for it.
- Content may go edge to edge only in rare cases, where matching the cutout width would make the UI look strange or not fit (for example a full-bleed hero image, a map, a wide data table, or a canvas). Keep text and controls inside the cutout width even then, and let only the one wide element break out.
- Do not let some sections match the cutout and others use a different width without a reason like the one above.

## Responsive guidance

- Design for compact, medium, and expanded widths.
- On compact screens, prioritize the main task and collapse secondary controls.
- On wider screens, use available space to improve comparison and scanning.
- Keep fixed-format elements stable with explicit dimensions, aspect ratios, or grid tracks.

## Spacing guidance

- Use consistent spacing increments.
- Keep related items closer than unrelated items.
- Do not rely on arbitrary one-off margins.
- Ensure text and controls do not overlap at narrow widths.

## Density guidance

- Density is a deliberate choice, not an accident. Cramped spacing (touching controls, no grouping, inconsistent gaps) is always wrong.
- Productivity tools can be denser, but must remain readable and keep the spacing rhythm.
- Marketing or editorial pages can use more open space, but the first viewport should still communicate the subject clearly.
