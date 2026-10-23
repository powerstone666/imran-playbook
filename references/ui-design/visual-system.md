# Material Design 3 Visual System

Use this for color, typography, shape, elevation, and visual hierarchy.

Official style reference: https://m3.material.io/styles

## Color

- Use semantic color roles: primary, secondary, tertiary, surface, background, error, and their container/on-color variants.
- Do not choose random colors per component.
- Ensure text and icon contrast is accessible.
- Reserve error colors for actual errors or destructive meaning.

Color reference: https://m3.material.io/styles/color/overview

## Typography

- Use typography roles consistently: display, headline, title, body, and label.
- Use larger type only where hierarchy requires it.
- Avoid viewport-scaled font sizes.
- Keep letter spacing normal unless the design system says otherwise.

Typography reference: https://m3.material.io/styles/typography/overview

## Shape

- Use shape to define component personality and hierarchy.
- Keep shape consistent across related surfaces and controls.
- Avoid randomly mixing radius values.

Shape reference: https://m3.material.io/styles/shape/overview

## Images

Images that are not a background get colour grading so they feel part of the design, not pasted in. Background images follow the normal background rules and are not graded this way.

- Grade photos and illustrations to the palette: a tint or duotone from the primary or tertiary tokens, adjusted contrast and saturation, and a subtle gradient overlay where text or controls sit on the image.
- Do it in CSS, not by editing each file: `filter` (`saturate`, `contrast`, `brightness`, `grayscale`), a `mix-blend-mode` overlay layer in a token colour (`multiply`, `soft-light`, or `color`), or an SVG `feColorMatrix` for a true duotone. Keep the grade in one shared image component or class so every image gets the same treatment.
- **The grade reacts on hover.** At rest the image sits in its grade; on hover (and keyboard focus) the grade intensifies, like on a flip card. Pick one hover style per project, to match the chosen design style, and use it for every image:
  - **Colour reveal:** graded, muted, or tinted at rest, then full colour on hover.
  - **Tint in:** full colour at rest, then the background or brand tint comes in on hover.
  - **Light and shadow:** a shadow layer at rest (a bottom gradient), and a light layer (a soft highlight or glow) on hover, or the reverse.
  - **Contrast shift:** contrast and saturation go up or down a step on hover.
  Do the change with a CSS transition (about 200 to 300 ms) on `filter` or on the overlay layer's opacity, not by swapping files. Under `prefers-reduced-motion`, keep the end state but drop the transition. Touch screens have no hover, so show a state that already reads well at rest, and do not hide information behind hover.
- One grade across the whole UI. Do not give each image its own look.
- Keep the subject readable: no heavy tints that hide detail, skin tones, or product colours. Check text contrast over any graded image.
- Do not grade logos, product screenshots, charts, maps, or images where accurate colour matters (for example product photos for sale). Leave user avatars and uploads ungraded unless asked.
- Always set `alt` text (or empty `alt` for decorative), explicit width and height, and use the framework's image component.

## Elevation

- Use elevation to communicate surface layering and interaction.
- Do not use shadows as decoration everywhere.
- Keep elevation subtle and consistent.
- Prefer tonal surface color to separate layers; add shadow only where layering needs it.

Elevation reference: https://m3.material.io/styles/elevation/overview
