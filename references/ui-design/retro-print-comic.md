# Retro Print Comic Style

Use this only when the user picks the retro print comic style in the design intake (`design-intake.md`), or asks for a Ben-Day dots, pop-art, old comic book, or comic magazine look. It is an allowed exception to the restraint rules in `material-3-web.md`. Accessibility, loading states (`components.md`), icons (`icons-and-labels.md`), and the happy path still apply.

Visual reference: the live Framer template "Benday" at https://studio-comico.framer.website/. There is no bundled screenshot. Open the site with the browser skill and look at it first (see `viewing-reference-sites.md`). Copy the ideas, never the name, logo, or copy. Close the template pop-ups.

## Where to see it

- Live: https://studio-comico.framer.website/ (a Framer template). Open the hero with the red "Don't press" button, press it, then scroll through "Recent work" (a paged project viewer with Back and Next tabs) and "How Benday began" (comic panels with a speech bubble and a "60!" burst).
- View it with the browser skill, as described in `viewing-reference-sites.md`.
- **Dynamic, GSAP and Framer motion (Imran's note):** these are dynamic, animated sites, built with GSAP and Framer, not static pages. Build the motion with GSAP (see "Animation with GSAP" in `interaction-accessibility.md`) or the project's motion library, and respect `prefers-reduced-motion`.

## What it is

The site is a printed comic magazine. Sections are pages and panels, headings are comic titles, and captions narrate the story. Everything looks printed: dots, halftones, thick ink outlines, and hard shadows.

## Look

- **Palette:** a tight set of warm printing colours: sunburst yellow, ink red, cream paper, a pink or salmon page, a blue panel, and near-black ink. Define them as tokens. Flat fills only.
- **Print texture:** Ben-Day dot patterns on backgrounds and inside titles, sunburst ray backgrounds (radiating stripes), halftone gradients that fade dots in a corner, and a faint hatched paper edge around the page.
- **Outlines and shadows:** every box, button, and panel has a thick near-black border and a hard offset shadow (a solid dark block shifted down and right, no blur). Panels and the page frame sit at slight angles, never perfectly square.
- **Typography:** a chunky comic title face with an outline and a drop shadow for headings, with the dot pattern clipped inside the letters. A hand-lettered all-caps face for captions and body text. Keep body copy short.
- **Comic devices as UI:**
  - **Caption boxes:** small yellow or cream rectangles with a border, used as labels and section intros ("Meanwhile, back at the studio...").
  - **Speech and thought bubbles** for quotes and short statements.
  - **Action bursts:** a starburst shape holding a key number ("60!").
  - **Page ribbon:** a small red tag for counts ("1 of 9").
  - **Side tabs** with rotated text for back and next.
- **Buttons:** rectangular, thick border, hard offset shadow, bold caps label. A primary button is yellow, a secondary is cream, a menu button is red with cream text. On hover the shadow shrinks and the button shifts into it, like pressing a key. This is the bouncy press from `components.md`.
- **Photos:** product or portrait photos sit inside a bordered frame with the same shadow. Portraits may be halftone-dotted to match the print look (see "Images" in `visual-system.md`).
- **Layout:** a page frame inset from the screen edge, with sections as stacked "pages". Content aligns inside the frame (see "Cutout navbar and content width" in `layout.md`).

## Build rules

1. **Tokens for the print system:** ink, paper, and 4 to 5 accent colours, one border width, one hard-shadow offset, and one dot pattern. Components use only these.
2. **Patterns in CSS.** Make dots with `radial-gradient` on a repeating background size, rays with `repeating-conic-gradient`, and halftone fades with a mask. Do not ship large pattern images.
3. **Shadows are solid.** Use `box-shadow` with zero blur, or a pseudo-element, so the offset block is crisp and keeps its colour in dark areas.
4. **Tilt sparingly.** Rotate only a few elements by 0.5 to 2 degrees, and keep text, forms, and buttons straight when they are used for input.
5. **One story, one voice.** Write captions and titles in the comic voice, and keep them short. Navigation labels stay plain and clear.
6. **Readability:** all-caps hand-lettered text is only for short lines. Long text uses a readable weight and size, and every colour pair passes contrast.
7. **Both modes:** the paper is part of the style. For a dark mode, use a dark ink page with the same accent colours and keep the outlines light, and check the dot patterns still read.

## When not to use it

- Long-form reading, data tools, or serious or regulated products.
- Brands that are not playful.
