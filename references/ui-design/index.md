# UI Design Reference Index

Use this folder for UI design decisions, Material Design 3 guidance, visual hierarchy, component selection, accessibility, and interaction behavior.

## Route by task

For a new UI or a full redesign, run `design-intake.md` first: ask the user about theme mode, design style, shell width, colours, art source, and animation level before designing. Always read `material-design-3.md`: it holds the required construction rules (mobile first, targets, type sizes, spacing, states, accessibility) that every style follows. The style decides the look, MD3 decides how it is built. Then add the chosen style's file and any topic files the task needs. Modern SaaS is the default style.

| Task signal | Read |
| --- | --- |
| Starting a new UI, or the user asks to change the full design | `design-intake.md` |
| Web app or site in the default Modern SaaS style: spacing, shell width, anti-slop layout | `modern-saas.md` |
| A design we do not bundle, or colours and fonts from a website link (writes `ui.md` or `design.md`) | `design-capture.md` |
| Images, SVG, backgrounds, logos, profiles, avatars (any style) | `assets-and-brand.md` |
| Any web UI: the Tailwind implementation of the MD3 rules and the AI-slop list. Pixel look and Android mockups add `pixel-android.md` | `material-3-web.md` |
| Android app UI, Material You, Material 3 Expressive, or a web mockup of an Android screen | `pixel-android.md` |
| Choosing or styling UI components, interactive state checklist | `components.md` |
| Icons, symbols, status labels, tags, chips, or badges | `icons-and-labels.md` |
| Layout, spacing, density, and responsive structure | `layout.md` |
| Color, typography, shape, and elevation | `visual-system.md` |
| Interaction behavior, motion, GSAP animation, usability, accessibility | `interaction-accessibility.md` |
| WebOS, desktop-style, or playful "site as an operating system" design (asked for explicitly) | `webos.md` |
| Illustrated, character-led webcomic site (asked for or chosen in the intake) | `illustrated-webcomic.md` |
| Retro print comic, Ben-Day dots, pop-art comic magazine look | `retro-print-comic.md` |
| Manga or anime comic panels, mascot-led illustrator or portfolio look | `manga-comic-panels.md` |
| A style file points to a live reference site to look at first | `viewing-reference-sites.md` |
| 3D scenes, model viewers, WebGL, Three.js | `threejs.md` |

Every web UI gets `material-design-3.md` and `material-3-web.md`, plus a look: `modern-saas.md` by default, or the chosen style's file. An Android app gets `material-design-3.md` and `pixel-android.md`. A web page meant to look like an Android phone screen gets all of these.
