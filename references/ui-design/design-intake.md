# Design Intake (Ask Before Designing)

Run this before any design work on a new UI, and again when the user asks to change the full design. It is a short round of user research. Do not pick the theme, shell, style, colours, or art source yourself and do not start building until the answers are in.

## When it applies

- **First implementation:** a new project, a new site or app, or the first UI in a repo that has no design system yet.
- **Full redesign:** the user asks to change the whole design, restyle everything, or switch design systems.

Whatever the user picks, the MD3 construction rules in `material-design-3.md` apply to it. The intake chooses the look; MD3 is never an option to drop.

It does not apply to small UI edits in a project that already has a design system. Follow the existing tokens and style there. If the project already has an established design (tokens, `design.md`, `ui.md`, or notes in `knowledge.md`), say what you found in one line instead of asking again.

## How to ask

Use `AskUserQuestion`, at most 4 questions per call, so the intake runs in three rounds. Put your recommendation first, marked "(Recommended)". Users can always pick "Other" and type their own. If the user answers "pick for me" on any point, choose, say what you chose, and carry on.

### Round 1: theme, style, shell

1. **Theme mode:** light only, dark only, or both. Recommend both for products people use for a long time, and light for a simple marketing page.
2. **Design style:**
   - **Modern SaaS (Recommended):** a clean, spacious, current look. `modern-saas.md`.
   - **Other styles we have:** WebOS desktop-style (`webos.md`), Pixel or Android (`pixel-android.md`), illustrated webcomic (`illustrated-webcomic.md`), retro print comic (`retro-print-comic.md`), manga comic panels (`manga-comic-panels.md`). Offer only the ones that fit the product; put the rest under "Other". They do not use the Modern SaaS look, but every one of them still follows the MD3 construction rules.
   - **Any other design:** the user names a style or gives a site, app, or screenshot. Follow Route 1 in `design-capture.md`: take screenshots with Playwright and write `ui.md` before building.
3. **Shell width** (ask when the style is Modern SaaS or a custom design, skip for WebOS, Android, and comic styles):
   - **Modern SaaS, about 70% width:** navbar and content in a centred container. Recommend for marketing sites, docs, and light apps.
   - **Full-width app:** navbar and content use the whole viewport. Recommend for dashboards and dense tools.
   - **70% navbar, full-width app:** a centred navbar over a full-width app area.

### Round 2: colour combination

Ask one question with these options in this order. `AskUserQuestion` takes 4 options plus "Other", so the fifth option is "Other".

1. **Palette from a big company, option A.**
2. **Palette from a big company, option B.**
3. **Palette from a big company, option C.** Suggest three well-known, award-winning company palettes that fit the product and give the primary, accent, and neutral base of each, for example Stripe's indigo, Spotify's green on near-black, Airbnb's coral, Linear's violet, Notion's warm neutrals, or Vercel's black and white. Pick ones that suit the product's mood. Take the colours only, never the brand.
4. **A website link.** The user gives a URL. Follow Route 2 in `design-capture.md`: read the real colours and fonts from the live site and write `design.md`.
5. **Describe it (the "Other" option).** The user describes the colours in their own words or gives brand hex values. Turn the description into a palette, show it, and get a yes. Label the "Other" field clearly in the question text ("or type your own colours or brand values").

If the project already has colour tokens, offer them as the first option instead of one of the company palettes.

### Round 3: art, motion, extras

1. **Images:** user provides, AI generates, or mix (recommended). See `assets-and-brand.md`.
2. **SVG:** user provides, AI creates, or mix (recommended). See `assets-and-brand.md`.
3. **Animation level:** GSAP is the default for every site, even a small one. Ask only how much, and recommend a level from the use case (see "Animation with GSAP" in `interaction-accessibility.md`): *subtle* for tools, dashboards, and docs; *moderate* for marketing and product sites; *expressive* for portfolios, launches, and illustrated styles.
4. **Anything else that decides the look**, only if still unknown: the product's purpose and audience, or a hard constraint such as an existing brand.

## What each answer changes

- **Light and dark both:** design the full system in both modes from the start, not a dark mode added later.
  - Define every colour as a token with a light and a dark value (see `visual-system.md`), and use only tokens in components.
  - Check contrast, elevation, borders, shadows, graded images, and every state in both modes.
  - Follow `prefers-color-scheme` for the first visit, add a visible theme toggle, remember the choice, and avoid a flash of the wrong theme on load.
  - Review screenshots of both modes before calling the design done.
- **One mode only:** build and check that mode only. Do not add a toggle.
- **Style:** read the chosen style's reference files before writing UI, and follow them as rules. The rules every style keeps are in `material-design-3.md` (accessibility, hierarchy, states), `components.md` (buttons, loading), `icons-and-labels.md`, and `assets-and-brand.md`.
- **Shell:** one shared width token for the navbar and the content (`modern-saas.md`).
- **Colours:** turn the chosen palette into semantic tokens (primary, secondary, tertiary, surface, background, error, and their on-colours) once, in one place. Do not scatter hex values.
- **Art source and animation level:** follow `assets-and-brand.md` and `interaction-accessibility.md`.

## Keep the answers

Write the decisions (mode, style, shell, palette, art source, animation level, icon source, and the path to `ui.md` or `design.md`) in the project's `knowledge.md` if the project uses one (see `../memory/index.md`), or in the design tokens file header. Next time, read them instead of asking again, unless the user asks for a full change.
