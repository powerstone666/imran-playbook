# Modern SaaS Design (Default Style)

This is the default *look* for web apps, dashboards, and product sites. The build rules come from `material-design-3.md` (mobile first, targets, type sizes, spacing, states, accessibility), which are required here as in every style. This file only decides the look: modern, spacious, calm, and current, never like a Google product and never like a template.

Read `material-design-3.md` first. This file adds to it and never relaxes it.

## What the look drops from Google

The MD3 rules all stay. Only the Google visual signature goes:
- The tonal-purple default palette, big pill buttons everywhere, floating action buttons, heavy tinted surfaces, and Roboto/Google Sans by default.
- Cloning any Material component pixel for pixel. Use the behaviour, then style it to the chosen palette and fonts.

## Breathing room

Generic output is cramped, so spacing is the first thing to fix.

- Spacing scale on a 4 px base: 4, 8, 12, 16, 24, 32, 48, 64, 96. Use only these.
- Section padding on marketing pages: 64 to 96 px vertical on desktop, 40 to 56 px on mobile.
- Card and panel padding: 24 px on desktop, 16 px on mobile. Gap between cards: 16 to 24 px.
- Form fields: 16 px between fields, 8 px between a label and its field, 40 to 48 px field height.
- Related items sit closer than unrelated ones; the gap between groups is at least double the gap inside a group.
- Body text line length 60 to 75 characters, line height 1.5 to 1.7. Headings tighter, 1.1 to 1.3.
- One focal point per viewport. If two things shout, one of them is wrong.
- Whitespace is not wasted space. Do not fill every gap with a card, badge, or icon.

## Anti-slop layout rules

- No three identical feature cards in a row with icon, heading, and two lines. Vary the layout: one large feature beside two small ones, a list with a real product screenshot, a split row, or a table.
- No centred hero over a gradient blob with two buttons as the only idea. Lead with the product, a real workflow, or a clear statement of value.
- Alternate section layouts; do not stack the same block six times.
- Use real or plausible product content, not "Lorem ipsum", "Feature One", or "John Doe".
- Limit to one accent colour used with purpose: the primary action, active state, and key data. Everything else is neutral.
- Borders and surface contrast first, shadow second. Use one subtle shadow level for floating layers only.
- One corner radius family: a small one for inputs and buttons, a larger one for cards and dialogs. Do not mix more.

## Shell width

The intake (`design-intake.md`) records which shell the user chose. Build exactly that, with one shared width token so the navbar and content cannot drift apart.

| Choice | Build |
| --- | --- |
| **Full-width app** | Sidebar or top bar and content use the full viewport. Right for dashboards, admin tools, and dense data. Cap long text blocks at a readable measure inside. |
| **Modern SaaS, about 70% width** | A centred container of about 70% of the viewport (`max-w` of roughly 1120 to 1280 px on large screens), navbar and content both inside it. Right for marketing sites, docs, and light apps. Falls back to full width with 16 to 24 px gutters on small screens. |
| **70% navbar, full-width app** | The navbar sits in the centred 70% container, while the app area below runs full width. Right for a marketing-style header over a data-heavy or canvas-style app. |

The floating cutout navbar in `layout.md` applies to the 70% shells; in the full-width shell it spans the full width unless the user says otherwise.

## Type and colour

- Choose a modern sans for UI and body (for example Inter, Geist, DM Sans, Plus Jakarta Sans, or the fonts from the user's chosen palette/site), and at most one display or serif face for headings if the brand needs it. Load fonts with `next/font` or the project's loader.
- A clear scale: for example 12, 14, 16, 20, 24, 32, 48, 64. Weight carries hierarchy; do not rely on size alone.
- Build the palette from the user's choice in the intake into semantic tokens (`visual-system.md`). Generate tints from one primary; keep neutrals slightly tinted toward the primary rather than pure grey.
- Check contrast in both modes when the user wanted light and dark.

## Components

- Buttons: one primary per view, secondary as outline or tonal, tertiary as text. Radius from the small family. Follow the loading rules in `components.md`.
- Navigation: sidebar for apps with more than four sections, top bar for sites. Show the active item clearly.
- Tables, filters, and empty states are designed, not defaults: sticky header, row hover, sensible column widths, and an empty state with a next action.
- Icons and labels follow `icons-and-labels.md`: one library, matching meaning, no default chips.
- Images, SVG, logos, and avatars follow `assets-and-brand.md`.
- Motion follows `interaction-accessibility.md`: GSAP is the default, scaled to the use case.

## Before calling it done

Open it in a browser at 1440, 1024, 768, and 390 px wide (and in both modes if both were chosen). Look for cramped groups, mismatched widths, repeated identical blocks, and anything that looks like a stock template, and fix it.
