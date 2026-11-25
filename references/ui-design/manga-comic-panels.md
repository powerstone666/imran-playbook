# Manga Comic Panels Style

Use this only when the user picks the manga comic panels style in the design intake (`design-intake.md`), or asks for an anime, manga, comic-panel, or illustrated pop portfolio look. It is an allowed exception to the restraint rules in `material-3-web.md`. Accessibility, loading states (`components.md`), icons (`icons-and-labels.md`), and the happy path still apply.

Visual reference: the live Framer template at https://peaceful-cantaloupe-258048.framer.app/ (an illustrator's portfolio). There is no bundled screenshot. Open the site with the browser skill and look at it first (see `viewing-reference-sites.md`). Copy the ideas, never the character, name, or copy. Ignore the Framer badge.

## Where to see it

- Live: https://peaceful-cantaloupe-258048.framer.app/ (a Framer template). Scroll slowly with real wheel events through: the angled hero panels with the mascot, the speech-bubble intro panel, "The work, in volumes." (fanned trading cards), "One project, three panels." (brief, chaos, ship), the services bars, the sketch, ink, and colour drag slider, and the outlined brand ticker.
- View it with the browser skill, as described in `viewing-reference-sites.md`.
- **Dynamic, GSAP and Framer motion (Imran's note):** these are dynamic, animated sites, built with GSAP and Framer, not static pages. Build the motion with GSAP (see "Animation with GSAP" in `interaction-accessibility.md`) or the project's motion library, and respect `prefers-reduced-motion`.

## What it is

The page is built from comic panels, and a mascot character leads it. Headlines are big, italic, and slanted, and every surface is drawn with thick outlines and offset shadows. The tone is energetic and fun, with game touches.

## Anime style fidelity

- Treat anime and manga as visual directions, not as requests to copy a particular franchise. Do not refuse or flatten a request just because it uses words like "anime," "manga," or names an inspiration.
- Preserve the visual medium the user asks for. If they request 2.5D anime, use dimensional anime illustration, layered scenes, expressive poses, cinematic lighting, and anime-style motion. Do not switch to pixel art, Minecraft-like characters, generic flat icons, or another medium unless they ask for it.
- When the user names an anime, comic, character, or franchise as a reference, research its visual themes and the specific qualities the user wants, then proceed with the website and original artwork. Do not wait for the user to provide a finished design or character art unless they explicitly want to supply it.
- When the user names a character or franchise for a website, research the character's appearance, abilities, themes, and history without asking the user to request that research. First check whether a specific public-domain version is available in the relevant jurisdiction. If so, use only details supported by that version and avoid features added in later adaptations.
- If no suitable public-domain version is available, continue with an original spoof or parody character based on the broad premise, archetype, or themes. Make its identity and expression distinct: create an independent silhouette, face, costume, symbols, name, palette, and ability details. Do not reproduce the recognizable design with only small changes, and do not claim that calling something a spoof automatically resolves rights concerns.
- A public-domain version is the first choice when it is verified and the available tools allow it; do not turn every franchise request into a spoof by default. If an image-generation tool blocks a verified public-domain depiction, do not repeatedly reword or disguise the same request to get around the block. State briefly that the tool blocked image generation, then continue the UI with a distinct original spoof/parody based on broad themes, or use a clearly marked placeholder if the user needs to approve the fallback.
- Keep any limitation narrow and the visual direction intact. Whether using a public-domain version or an original spoof/parody, preserve the requested anime look, scene, composition, mood, and animation. Do not reject the whole website, wait for the user to propose the workaround, or silently substitute an unrelated style.
- For generated artwork, make each image distinct and tailored to its placement. Do not reuse one image as multiple characters, poses, or scene assets. Keep designed backgrounds visually rich with layered SVG details and scene elements; do not leave them blank.
- Build visible animation when requested: use separate poses or layered artwork for character motion, plus scroll, hover, or scene transitions where they fit. Do not treat a static pixel sprite or a generic CSS wiggle as a substitute for requested anime character animation.

## Look

- **Palette:** saturated, flat, and bright on a clean off-white page: hot pink, electric cyan, sunny yellow, violet, and mint, with a very dark navy for ink, text, and outlines. Define them as tokens, and use the navy for every outline and for body text.
- **Panels:** layouts are divided into angled panels with thick navy borders and gutters, with slightly skewed edges. Panel backgrounds use speed lines (radiating strokes), halftone dots, stripes, and sunbursts, each in one colour.
- **Typography:** a heavy condensed italic display face for headlines, set large, with a coloured offset shadow behind the letters and one word in an accent colour ("volumes."). Small caps labels in a plain sans (with letter spacing) for tags like "VOL.01". Body text is a clean sans in navy.
- **Mascot:** one original character who appears in the hero and repeats through the page in different poses and expressions, popping out of panels.
- **Speech bubbles** with a tail for short messages and quotes, with a thick outline and an offset shadow. Sound-effect words (in the reference, Japanese onomatopoeia) can be used as decoration.
- **Collectible cards:** work and items shown as trading cards, fanned or tilted, each with its own accent colour background, a simple illustrated object, a title, and a small label. Numbered "VOL." headers sit on top.
- **Buttons:** pill shapes with a thick navy outline and a solid offset shadow in a second colour. Primary is hot pink with white text, secondary is white with navy text, a hire or contact button is navy with a pink shadow. A trailing arrow icon comes from the icon library, not a text character (see `icons-and-labels.md`).
- **Navigation:** a slim white bar with a navy bottom border, the logo at the left, centred links, and one primary button at the right.
- **Game touches (when the brand fits):** levels, stars, and "power-up" tiers for pricing, a drag slider that moves a piece of art from sketch to ink to colour, and a ticker of discipline names.

## Build rules

1. **Tokens first:** navy ink, off-white paper, 4 to 5 accents, one border width, one offset-shadow size (in a colour, not blur), and one skew angle. Components use only these.
2. **Art has a clear source.** Follow `assets-and-brand.md`: use user-supplied artwork when provided, or create distinct original anime-style artwork with an available image-generation tool when the user chose AI. Do not imitate a reference mascot or pass placeholder shapes off as finished character art. If image generation is unavailable, use clearly marked placeholders and state that the artwork remains to be created.
3. **Panels are CSS.** Use `clip-path` or `transform: skew()` for angled panels, `repeating-conic-gradient` for speed lines, and `radial-gradient` for dots. Keep panel content readable by keeping text blocks un-skewed inside the skewed container.
4. **Offset shadows are solid** (zero blur), and shift on press for the bouncy press in `components.md`.
5. **Colour discipline:** each panel or card uses one accent family, and text on it is navy or white, whichever passes contrast.
6. **Motion:** cards fan and tilt on hover, panels reveal on scroll, and the slider is draggable with the keyboard as well. Use the project's animation approach (see `interaction-accessibility.md`) and respect `prefers-reduced-motion`.
7. **Accessibility:** speech bubbles and sound words are decoration or real text with proper alt or `aria-hidden`; the slider has a label and a keyboard control; headings stay real headings even when styled as art.
8. **Both modes:** the off-white page is part of the style. For a dark mode, use a deep navy page, keep the accents, and flip the outlines to light, then check each panel pattern.

## When not to use it

- Serious, data-heavy, or regulated products.
- Projects with no original illustration or mascot.
