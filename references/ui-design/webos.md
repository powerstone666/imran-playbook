# WebOS Desktop-Style Websites

Use this only when the user asks for a webOS, desktop-style, or playful "website as an operating system" design. It is a deliberate exception to the restraint rules in `material-3-web.md`: where the user asked for this style, its playful surfaces, textures, and metaphors are allowed. Accessibility, the happy path, and the cutout alignment idea (see `layout.md`) still apply.

Visual reference: the live site https://posthog.com. There is no bundled screenshot. Open the site with the browser skill and look at it first (see `viewing-reference-sites.md`). Copy the ideas, never their brand, copy, illustrations, or logos.

## Where to see it

- Live: https://posthog.com (the desktop with icons down both sides, the menu bar, and the content window). Open a few icons to see the windows work.
- View it with the browser skill, as described in `viewing-reference-sites.md`.
- **Dynamic, GSAP and Framer motion (Imran's note):** these are dynamic, animated sites, built with GSAP and Framer, not static pages. Build the motion with GSAP (see "Animation with GSAP" in `interaction-accessibility.md`) or the project's motion library, and respect `prefers-reduced-motion`.

## What it is

The whole site is a fake desktop. Navigation becomes "opening apps", and pages open as windows on top of a wallpaper.

## Parts of the reference

- **Menu bar** across the top: logo, main links, then search, help, and account on the right. It is the real navigation and floats inset from the screen edges.
- **Desktop icons** down the left and right edges: an icon above a short label (Home, Docs, Pricing, Careers, Trash). Each one opens a page or window.
- **Window** in the middle with maximise and close controls. Page content lives inside it, scrolls inside it, and has its own inner panels.
- **Wallpaper**: an illustrated, handmade-looking scene (paper-cut grass and low-poly objects), not a stock photo.
- **Frosted window surface** over the wallpaper, with a soft dotted-grid panel for the hero inside.
- **Hero as a nostalgic object**: here a retro software box and CD. Pick one object that tells the brand's joke or story.
- **Highlighter emphasis**: one phrase in the headline sits on a marker-style colour block.
- **Chunky buttons** with a visible bottom edge, in one warm accent colour.
- **Plain-spoken, funny copy.** The brand voice is part of the design.

## Build rules

1. **Shell first.** Build the shell as its own component: menu bar, desktop icon grid, wallpaper layer, window layer. Pages render inside a `Window` component and know nothing about the shell.
2. **Window state in one store** (open windows, order, focused, minimised, maximised). Use a small store such as Zustand, or React context for a few windows. Clicking a window raises it by changing its order, not by hand-set z-index values.
3. **Real URLs.** Opening a window updates the route, and loading a route opens its window. Back and forward, deep links, and sharing must work. In Next.js this means one route per page, with the shell in the layout.
4. **Dragging and resizing** only where it earns its place. Start with one main window that maximises and closes; add dragging with a small library or pointer events only if asked.
5. **Make it accessible.** Desktop icons are real links or buttons with visible focus. Windows are dialogs or regions with a label, Escape closes the top one, focus moves into a window on open and returns to its icon on close, and all of it works from the keyboard. Respect `prefers-reduced-motion` for open and close animation.
6. **Phones get a simple version.** Under tablet width, drop the drag behavior and show the desktop icons as an app-style grid, and open pages full screen. Do not shrink a desktop to a phone.
7. **Keep the wallpaper light.** Use a compressed image (WebP or AVIF) with set dimensions, load it with the framework's image component, and keep text on top of it readable with a solid or frosted surface.
8. **Content stays real.** The playful frame must not hide the pricing, docs, or main action. The primary action is visible without opening anything.

## Tokens

- One warm accent for buttons and one highlighter colour for the headline phrase, defined as design tokens like the rest of the UI.
- Two radius values: window and panel corners, and control corners.
- Text on frosted or illustrated surfaces must keep accessible contrast (see `interaction-accessibility.md`).

## When not to use it

- Serious, data-heavy, or accessibility-critical tools.
- Projects with no brand personality.
- A hackathon with little time, unless the metaphor is the whole pitch. The illustrations, window behavior, and icons take real time.
