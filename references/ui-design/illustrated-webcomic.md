# Illustrated Webcomic Style

Use this only when the user picks the illustrated webcomic style in the design intake (`design-intake.md`), or asks for a character-led, storybook, or interactive-comic site. Where it applies, it is an allowed exception to the restraint rules in `material-3-web.md`. Accessibility, loading states (`components.md`), icons (`icons-and-labels.md`), and the happy path still apply.

Visual reference: the live site https://ponpon-mania.com/about. There is no bundled screenshot. Open the site with the browser skill and look at it first (see `viewing-reference-sites.md`). Copy the ideas, never the characters, art, or brand. Dismiss the cookie bar.

## Where to see it

- Live: https://ponpon-mania.com/about (also try the home page and the chapters page). Characters fall and tumble on a flat peach stage, so wait for the intro and move the pointer over the page. If the page content looks sparse, the art is the content.
- View it with the browser skill, as described in `viewing-reference-sites.md`.
- **Dynamic, GSAP and Framer motion (Imran's note):** these are dynamic, animated sites, built with GSAP and Framer, not static pages. Build the motion with GSAP (see "Animation with GSAP" in `interaction-accessibility.md`) or the project's motion library, and respect `prefers-reduced-motion`.

## What it is

The illustration is the whole design. One soft, flat background colour, a tiny navigation, and large hand-drawn characters filling the page. There are almost no boxes, cards, or decoration besides the art.

## Look

- **Background:** one flat warm pastel (a pale peach or cream in the reference), no gradients, no texture.
- **Art:** big characters drawn with thick dark outlines and flat fills in a small palette (tan, pink, orange, red, yellow accents). They overlap, tumble, and bleed off the page edges, and may animate (idle motion, reacting to scroll or pointer).
- **Navigation:** three items centred at the top: a text link, the logo in the middle, and an outlined pill link. Text is lowercase, bold, and plain. The logo is a chunky, slightly wonky lettermark.
- **Typography:** one heavy rounded display face for the logo and headings, and plain small body text. All lowercase headings give a casual voice.
- **Buttons:** outlined pills with a thin dark border and no fill (the "about" link), and a filled white or black pill for primary choices.
- **Footer or banners:** a solid near-black bar for system messages such as cookies, with small pill buttons.
- **Voice:** casual, short, with a wink ("Hey you").

## Build rules

1. **Art first.** The brief must say who the characters are before layout starts. Use art the user provides or approves. Never generate stand-in clip-art or hand-draw SVG characters. If there is no art yet, build the layout with clearly marked placeholders and say so.
2. **One palette from the art.** Take the background, ink, and 3 to 4 accent colours from the characters and define them as tokens (see `visual-system.md`). The UI chrome uses only the ink colour and the background.
3. **Motion carries the personality.** Animate the characters (spring or idle loops, scroll-linked reveals) using the project's animation approach (see `interaction-accessibility.md`). Keep the UI around them still. Respect `prefers-reduced-motion` by showing a still pose.
4. **Content on top of art stays readable.** Put text on the flat background area, or on a solid panel, never directly over busy art.
5. **Assets are heavy.** Use optimised image or video formats, set dimensions, lazy-load below the fold, and give every character image alt text, or an empty alt when it is decoration.
6. **Light mode first.** The pastel background is part of the identity. For a dark mode, redraw the background as a deep tone from the same hue and check that outlines and art still read; ask the user if there is no dark art.
7. **Both languages and tone.** If the site is bilingual (the reference has EN | FR), keep the toggle in the navigation and keep the voice in both.

## When not to use it

- Products where the interface or data is the point, such as dashboards and tools.
- Projects with no original illustration.
