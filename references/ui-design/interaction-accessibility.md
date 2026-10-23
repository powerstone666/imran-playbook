# Material Design 3 Interaction And Accessibility

Use this for interaction behavior, states, motion, usability, and accessibility.

Official foundations reference: https://m3.material.io/foundations

## Interaction rules

- Every interactive element needs a visible state change.
- Use clear focus indicators for keyboard navigation.
- Keep primary actions easy to find.
- Avoid surprising navigation or hidden destructive actions.
- Show loading feedback for async actions. Buttons and pages must follow the button rules in `components.md`.
- Show errors in context and make recovery clear.

## Motion

- Use motion to explain relationships and state changes.
- Keep motion brief and purposeful.
- Avoid motion that blocks the task.
- Respect reduced-motion preferences when implementing animations.

Motion reference: https://m3.material.io/styles/motion/overview

## Animation with GSAP

Pick the lightest tool that does the job:

- Simple state changes (hover, press, open/close, fade): CSS transitions or Tailwind `transition-*` utilities. No library.
- Timelines, sequenced choreography, scroll-driven animation, pinning, Flip layout transitions, draggable, or SVG drawing: use GSAP.

When using GSAP, follow the official GreenSock skills: https://github.com/greensock/gsap-skills

| Task | Skill |
| --- | --- |
| Core tweens, easing, stagger, responsive or reduced-motion animation | `gsap-core` |
| React or Next.js (`useGSAP`, refs, cleanup on unmount) | `gsap-react` |
| Vue, Nuxt, Svelte, SvelteKit | `gsap-frameworks` |
| Sequencing and choreography | `gsap-timeline` |
| Scroll-linked animation, pinning, scrub, parallax | `gsap-scrolltrigger` |
| Flip, Draggable, SplitText, ScrollSmoother, SVG and other plugins | `gsap-plugins` |
| Jank, FPS, transforms vs layout | `gsap-performance` |
| `gsap.utils` helpers (clamp, mapRange, snap, toArray) | `gsap-utils` |

Install the skills once per machine with `npx skills add greensock/gsap-skills -g --all`. Install the packages following `../package-installation/npm.md`: `npm install gsap@latest`, plus `@gsap/react@latest` for React or Next.js.

GSAP motion still follows the Material motion rules above:

- Animate to explain a relationship or state change, never as decoration.
- Keep durations short and do not block the task.
- Respect `prefers-reduced-motion` through `gsap.matchMedia()`, with a no-motion or fade-only fallback.
- Animate transforms and opacity, not layout properties.
- In Next.js, GSAP runs only in client components (`"use client"`) and must clean up on unmount (`useGSAP` does this).

## Accessibility

- Ensure sufficient contrast for text, icons, and controls.
- Use semantic HTML when building web UI.
- Provide labels for form controls and icon-only buttons.
- Keep touch/click targets large enough for reliable interaction.
- Support keyboard navigation for interactive flows.
- Do not communicate meaning by color alone.

## Usability checklist

- Can the user identify the main task immediately?
- Can the user complete the task with keyboard only?
- Are loading, empty, error, and success states handled?
- Does the layout remain usable on mobile and desktop?
- Are destructive actions clearly labeled and reversible or confirmed when needed?
