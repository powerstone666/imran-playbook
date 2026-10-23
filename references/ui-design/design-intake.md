# Design Intake (Ask Before Designing)

Run this before any design work on a new UI, and again when the user asks to change the full design. It is a short round of user research. Do not pick the theme, style, or colours yourself and do not start building until the answers are in.

## When it applies

- **First implementation:** a new project, a new site or app, or the first UI in a repo that has no design system yet.
- **Full redesign:** the user asks to change the whole design, restyle everything, or switch design systems.

It does not apply to small UI edits in a project that already has a design system. Follow the existing tokens and style there. If the project already has an established design, say what you found in one line instead of asking again.

## Questions to ask

Use `AskUserQuestion`, in one call with up to 4 questions. Put your recommendation first, marked "(Recommended)", based on the product and the repo. Users can always pick "Other" and type their own.

1. **Theme mode:** light only, dark only, or both. Recommend both for products people use for a long time, and light for a simple marketing page.
2. **Design style:** the design system or look to follow. Offer what the playbook has, plus open options:
   - Material Design 3 (`material-design-3.md`, `material-3-web.md`).
   - WebOS, a desktop-style site (`webos.md`).
   - Pixel or Android style (`pixel-android.md`).
   - Illustrated webcomic: character-led, one pastel background (`illustrated-webcomic.md`).
   - Retro print comic: Ben-Day dots, sunbursts, comic magazine (`retro-print-comic.md`).
   - Manga comic panels: angled panels, mascot, bold pop colours (`manga-comic-panels.md`).
   - Something else: the user names a style or shares a reference site or screenshot. Read and describe it back before using it.
3. **Colour combination:** offer 2 to 3 palettes that fit the product, each with a primary colour, an accent, and a neutral base, plus "I have brand colours" (ask for the values) and "pick for me". If the project already has colour tokens, offer them as the first option.
4. **Anything else that decides the look**, only if still unknown: the product's purpose and audience, a reference site the user likes, or a hard constraint such as an existing brand.

If the user answers "pick for me" on any point, choose, say what you chose, and carry on.

## What each answer changes

- **Light and dark both:** design the full system in both modes from the start, not a dark mode added later.
  - Define every colour as a token with a light and a dark value (see `visual-system.md`), and use only tokens in components.
  - Check contrast, elevation, borders, shadows, graded images, and every state in both modes.
  - Follow `prefers-color-scheme` for the first visit, add a visible theme toggle, remember the choice, and avoid a flash of the wrong theme on load.
  - Review screenshots of both modes before calling the design done.
- **One mode only:** build and check that mode only. Do not add a toggle.
- **Style:** read the chosen style's reference files before writing UI, and follow them as rules. The rules every style keeps are in `material-design-3.md` (accessibility, hierarchy, states), `components.md` (buttons, loading), and `icons-and-labels.md`.
- **Colours:** turn the chosen palette into semantic tokens (primary, secondary, tertiary, surface, background, error, and their on-colours) once, in one place. Do not scatter hex values.

## Keep the answers

Write the decisions (mode, style, palette, icon source) in the project's `knowledge.md` if the project uses one (see `../memory/index.md`), or in the design tokens file header. Next time, read them instead of asking again, unless the user asks for a full change.
