# Material Design 3: The Construction Rules (Required for Every Style)

MD3 is the design-pattern layer, the way SOLID is for code. The chosen style (Modern SaaS, a Netflix-like reference, a comic look, anything) decides how the UI *looks*. MD3 decides how it is *built*: how components are sized, spaced, placed, and behave. Without it, "make it like Netflix" gives a vague clone with arbitrary buttons and card placement. With it, the result is consistent, accessible, and mobile-first whatever the look.

Every UI follows the rules below in every style. A style file may change colour, type face, shape, imagery, and mood. It may not break these rules, except where a style file names the exception.

## Required rules

**Mobile first**
- Design and build the smallest screen (360 to 390 px) first, then enhance at 600, 840, 1200, and 1600 px (compact, medium, expanded, large, extra-large window classes). Base styles are the mobile styles; wider breakpoints add.
- No horizontal page scroll. Navigation fits the size: bottom bar or drawer on compact, rail or sidebar on medium and up.

**Touch and click targets**
- Every interactive control is at least 48 x 48 px of hit area (the visible shape can be smaller, such as a 40 px button with padding). At least 8 px between adjacent targets.

**Type sizes (readable minimums)**
- Body text 16 px (never below 14 px), labels and buttons 14 px with weight 500, captions 12 px at the very smallest and only for secondary text. Headlines step up from the MD3 roles (display, headline, title, body, label) rather than one-off sizes.
- Line height 1.4 to 1.6 for body. Keep lines to 45 to 75 characters. Use the roles in `visual-system.md`.
- Text and background contrast: 4.5:1 for body, 3:1 for large text and for icons and control borders.

**Spacing**
- Use the 4 px / 8 px rhythm: 4, 8, 12, 16, 24, 32, 48, 64. Page gutters 16 px on compact, 24 px on medium, 24 to 32 px on expanded. Card and panel padding 16 to 24 px. Related items sit closer than unrelated groups.
- No cramped UI. When in doubt, add space, not another border.

**Components and placement**
- Use the standard component for the job (`components.md`) and put it where users expect it: the primary action in a consistent, prominent spot; navigation in one predictable place; search at the top; forms in a single column on compact; destructive actions apart from the primary one.
- One primary action per view. Visual weight follows importance: filled, then tonal, then outlined, then text.
- Lists and card grids use a consistent grid and equal gaps. Do not place cards by eye.

**States and cursor**
- Every interactive element has the full state checklist in `components.md`: default, hover, focus, pressed, selected, disabled, loading, error.
- Clickable things show `cursor: pointer`; disabled ones `cursor: not-allowed`. Hover changes are visible; focus rings are always visible for keyboard users and never removed.
- Loading, empty, and error states exist for every view that loads data.

**Accessibility**
- Semantic HTML first, ARIA only when needed. All controls reachable and operable by keyboard in a logical order. Labels for every form field and icon-only button. Meaning is never carried by colour alone. Respect `prefers-reduced-motion` and `prefers-color-scheme`.

**Tokens**
- Colour, type, shape, spacing, and elevation come from named tokens (roles), defined once. No stray hex values or one-off pixel sizes in components.

## How styles sit on top of this

1. The intake picks a style or reference (`design-intake.md`).
2. The style supplies the look: palette, fonts, shape language, imagery, motion mood, layout character.
3. These rules govern every component and layout the style produces. If a reference design (for example from `ui.md`) has smaller text or a tiny target, keep its look but meet the minimums here.
4. When a style and these rules conflict, the rules win, unless the style file lists an exception.

Do not copy Google's visual design. Take the patterns, not the Google look.

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
- Use motion to explain state changes, not to distract. For animation tooling (CSS vs GSAP and the official GSAP skills), see `interaction-accessibility.md`.
- Support responsive layouts (see `layout.md`).

## Implementation habit

Before creating a custom UI element, ask:

- Is there a Material component for this?
- What state variants does it need?
- What is the primary action?
- What content must remain scannable?
- Does the layout work on mobile and desktop?
