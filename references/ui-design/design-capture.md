# Design Capture: ui.md and design.md

Two capture routes turn something the user points at into a written spec the build can follow. Both use the browser, and both write a file into the project so the design survives across sessions.

| Route | Trigger | Output |
| --- | --- | --- |
| **Reference design** | The user picks a design style we do not bundle, or gives any other design (a site, an app, a screenshot, a named product look) | `ui.md` |
| **Colour and type from a website** | The user picks "give a website link" in the colour question | `design.md` |

Never copy brand assets, logos, art, copy, or code. Capture the system (layout, spacing, type, colour, motion), not the brand.

## Browser setup

Use Playwright (or the installed `agent-browser` skill; see `viewing-reference-sites.md` for the scroll and interaction method). Run it without a global install (`npx playwright`) and ask before installing anything globally. Use a 1440 x 900 viewport, wait 5 seconds for intro animations, dismiss cookie banners, and keep screenshots in the scratchpad folder, not in the repo.

## Route 1: reference design, written to ui.md

1. Take full-page and viewport screenshots at 1440, 768, and 390 px wide. Scroll with real wheel events in about 200 px steps so scroll-triggered content appears.
2. Hover and click the main buttons, cards, and navigation, and screenshot the states.
3. Look at every screenshot. Then write `ui.md` at the project root (or `docs/ui.md` if the repo has a `docs/` folder) with these sections:
   - **Source:** the URL or description, and the date captured.
   - **Layout:** shell type and width, grid, section order, navbar behaviour.
   - **Spacing:** the scale and typical section, card, and gap sizes.
   - **Typography:** families, scale, weights, line heights, letter spacing.
   - **Shape and elevation:** radii, borders, shadows.
   - **Components:** buttons, inputs, cards, nav, tables, and their states.
   - **Imagery and illustration:** style, treatment, and how it is used.
   - **Motion:** what animates, easing, and duration.
   - **Do and don't:** five short rules that keep the build faithful.
4. Describe it back to the user in a few lines and get a yes before building.
5. Build from `ui.md`, with the user's palette (colour question) applied on top if they chose one. The reference supplies the look only; layout, sizes, spacing, states, and accessibility follow `material-design-3.md`, so a copied look never inherits tiny text, small targets, or arbitrary placement.

If the browser cannot reach the source, say so and ask for screenshots or a recording.

## Route 2: colour and type from a website, written to design.md

1. Open the given link and take the viewport and full-page screenshots.
2. Read the page's real values from the live DOM and CSS, not by eye: computed `font-family`, sizes and weights for headings, body, and buttons; the CSS custom properties on `:root`; and computed colours for background, surface, text, primary action, links, borders, and accents. Check dark mode too if the site has one. Check the loaded fonts (network requests or `@font-face`) and note whether each is a Google font, a licensed font, or a system font.
3. Write `design.md` at the project root with:
   - **Source** and date.
   - **Colours:** a table of role, hex, and where it is used, for light and dark if both exist.
   - **Typography:** each family with its role, the weights used, the size scale, and the line heights.
   - **Fonts to use:** the exact font if it is freely available, otherwise the closest free match, and say which.
   - **Shape and spacing** notes if visible: radii, borders, shadows, and section spacing.
4. Turn the colours into semantic tokens (`visual-system.md`) and the fonts into the project's font setup. Show the user the palette and fonts, and wait for a yes before building.
5. Take the system, not the brand: do not use the site's logo, name, copy, or images.

## Keep it current

Write the path of `ui.md` or `design.md` into the project's `knowledge.md` if it has one (see `../memory/index.md`). Later sessions read these files instead of asking again, unless the user asks for a full redesign.
