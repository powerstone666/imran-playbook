# Manga Comic Panels Style

Use this only when the user picks the manga comic panels style in the design intake (`design-intake.md`), or asks for an anime, manga, comic-panel, or illustrated pop portfolio look. It is an allowed exception to the restraint rules in `material-3-web.md`. Accessibility, loading states (`components.md`), icons (`icons-and-labels.md`), and the happy path still apply.

Visual reference: the live Framer template at https://peaceful-cantaloupe-258048.framer.app/ (an illustrator's portfolio). There is no bundled screenshot. Open the site with the browser skill and look at it first (see `viewing-reference-sites.md`). Copy the ideas, never the character, name, or copy. Ignore the Framer badge.

## Where to see it

- Live: https://peaceful-cantaloupe-258048.framer.app/ (a Framer template). Scroll slowly with real wheel events through: the angled hero panels with the mascot, the speech-bubble intro panel, "The work, in volumes." (fanned trading cards), "One project, three panels." (brief, chaos, ship), the services bars, the sketch, ink, and colour drag slider, and the outlined brand ticker.
- View it with the browser skill, as described in `viewing-reference-sites.md`.
- **Dynamic, GSAP and Framer motion (Imran's note):** these are dynamic, animated sites, built with GSAP and Framer, not static pages. Build the motion with GSAP (see "Animation with GSAP" in `interaction-accessibility.md`) or the project's motion library, and respect `prefers-reduced-motion`.

## What it is

The page is built from comic panels, and a mascot character leads it. Headlines are big, italic, and slanted, and every surface is drawn with thick outlines and offset shadows. The tone is energetic and fun, with game touches.

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
2. **Art is supplied.** The mascot and card art must come from the user or an approved source. Never hand-draw SVG characters or fake the art. Without art, build the panels with marked placeholders and say so.
3. **Panels are CSS.** Use `clip-path` or `transform: skew()` for angled panels, `repeating-conic-gradient` for speed lines, and `radial-gradient` for dots. Keep panel content readable by keeping text blocks un-skewed inside the skewed container.
4. **Offset shadows are solid** (zero blur), and shift on press for the bouncy press in `components.md`.
5. **Colour discipline:** each panel or card uses one accent family, and text on it is navy or white, whichever passes contrast.
6. **Motion:** cards fan and tilt on hover, panels reveal on scroll, and the slider is draggable with the keyboard as well. Use the project's animation approach (see `interaction-accessibility.md`) and respect `prefers-reduced-motion`.
7. **Accessibility:** speech bubbles and sound words are decoration or real text with proper alt or `aria-hidden`; the slider has a label and a keyboard control; headings stay real headings even when styled as art.
8. **Both modes:** the off-white page is part of the style. For a dark mode, use a deep navy page, keep the accents, and flip the outlines to light, then check each panel pattern.

## When not to use it

- Serious, data-heavy, or regulated products.
- Projects with no original illustration or mascot.
