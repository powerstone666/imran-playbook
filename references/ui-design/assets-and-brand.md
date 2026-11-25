# Images, SVG, Logos and Avatars (All Styles)

This rule applies to every UI, not only anime or illustrated sites. A page with no art and a blank background looks generic, and a page with fake art looks worse, so the source of the art is a decision for the user.

## Ask first: who provides the visuals

Ask once per project, in the design intake (`design-intake.md`), with `AskUserQuestion`:

1. **Images:** I will provide them / AI generates them / mix.
2. **SVG (backgrounds, patterns, illustrations, shapes):** I will provide them / AI creates them / mix.

Recommend "mix" for most products: the user supplies real photos, product shots, and logos, and the AI fills the rest. Record the answer in `knowledge.md` or the tokens file header.

| Answer | What to do |
| --- | --- |
| **User provides** | Build the layout with sized, clearly named slots. Use the user's files as they arrive. Until then, a slot shows a neutral surface with the intended aspect ratio and a label such as "Hero image, 16:9" (see the placeholder rule below). Tell the user which slots are waiting. |
| **AI generates images** | Use an available image-generation tool. If none exists, say so and ask the user. Each image is unique and fits its placement; never reuse one image for several slots. Grade them as in `visual-system.md`. |
| **AI creates SVG** | Write original, layered SVG for backgrounds, patterns, dividers, and spot illustrations that fit the chosen style and palette. This is the exception to the "never hand-draw SVG" rule in `icons-and-labels.md`, which still holds for UI icons. |

A deliberately minimal utility screen (a settings page, a login form) can use no imagery. Say so instead of adding filler.

## Backgrounds

Do not leave a designed background flat and empty. Use layered SVG (gradients with restraint, patterns, grids, shapes, scene motifs) in the palette, quiet enough that foreground text keeps its contrast. In Modern SaaS, subtle is the goal: a soft grid, a faint shape, a gentle gradient mesh, never a loud blob. Illustrated and anime styles go richer, as their files describe.

## Brand marks, profiles and avatars: no alphabet placeholders

When the UI shows a brand, company, product, person, or profile, do not stand in with a coloured circle or square holding one or two letters ("A", "JD") and do not use a generic grey silhouette.

Use, in this order:

1. **The real asset** the user provided: a logo, a photo, a headshot.
2. **A generated or created image or SVG** that fits the subject: a logo mark for a brand, a portrait or illustrated avatar for a person. Make each one distinct. Ask first if the user said they will provide the assets.
3. **Clever lettering**, only when the letters are designed as a mark: a custom monogram or wordmark with deliberate type, proportion, shape, and the brand colours, built as SVG. It must look like a logo, not like a default avatar circle.

Rules:
- Real customer, company, or person names get real logos or photos from the user. Never invent a logo that imitates a real brand.
- Lists with many people or companies (testimonials, team, logo walls, comment threads) need distinct art for each entry. Do not repeat one face or one mark.
- An unavoidable fallback (a user without a photo in a live app) uses a designed avatar: generated pattern art or illustration seeded by the user ID, not initials on a flat circle.
- Alt text describes the subject; decorative art has an empty `alt`.

## Quality

Set explicit width and height, use the framework's image component, lazy-load below the fold, compress (WebP or AVIF), and keep each SVG lean. Image grading and hover treatment live in `visual-system.md`.
