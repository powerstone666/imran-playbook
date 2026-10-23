# Viewing Reference Sites

Some style files point to live sites instead of bundled screenshots, because these sites are animated and screenshots go stale and bloat the repo. Before building in one of those styles, open the site yourself and look at it.

## Steps

1. **Use the browser skill.** Invoke the `agent-browser` skill (or `playwright` if that is what is installed), and follow its own usage guide. If the CLI is not installed, you can run it with `npx agent-browser` without a global install; ask the user before installing anything globally.
2. **Use your own session**, a 1440 x 900 viewport, and wait 5 seconds after opening so intro animations can finish.
3. **Dismiss banners** (cookie bars, template pop-ups) so they do not cover the design.
4. **Scroll with real wheel events**, not by jumping: `mouse move` to the centre, then `mouse wheel` in steps of about 200 px with a 2 second wait between steps. GSAP and Framer reveal content on scroll and on wheel, so a fast jump captures blank sections. Take a screenshot after every step.
5. **Interact.** Hover buttons and cards, click the main button, drag any slider, and move the pointer over the hero. Much of the style is in the motion.
6. **Look at the screenshots** and describe what you see back to the user in a few lines (palette, type, shapes, motion) before you start building.
7. **Do not copy the files** into the project or the repo. Keep screenshots in a scratch folder. Copy the ideas, never the brand, art, copy, or code.

## If the browser cannot reach the site

Say so, and ask the user for screenshots or a screen recording of the site, or build from the written description in the style file.
