# Three.js 3D

Use this when a web UI needs 3D: product viewers, model previews, data or scene visualizations, or interactive 3D experiences.

## When 3D belongs

- Use 3D only when it shows something the product needs: a model, a space, spatial data, or an interaction that 2D cannot express.
- Do not add decorative 3D (floating shapes, spinning blobs, background scenes) to look modern; it falls under the AI-slop rules in `material-3-web.md`.
- Keep the primary task usable without the 3D view: text, controls, and key content stay in normal HTML around the canvas.

## Skills to follow

Follow the Three.js skills at https://github.com/cloudai-x/threejs-skills:

| Task | Skill |
| --- | --- |
| Scene, camera, renderer, object hierarchy, transforms | `threejs-fundamentals` |
| Built-in shapes, BufferGeometry, custom meshes, instancing | `threejs-geometry` |
| PBR and other materials, material performance | `threejs-materials` |
| Lights, shadows, environment lighting (IBL) | `threejs-lighting` |
| Texture types, UV mapping, environment maps | `threejs-textures` |
| Loading GLTF models, textures, HDR, loading progress | `threejs-loaders` |
| Raycasting, camera controls, mouse/touch input, selection | `threejs-interaction` |
| Keyframe, skeletal, morph target, GLTF animation | `threejs-animation` |
| GLSL, ShaderMaterial, uniforms, custom effects | `threejs-shaders` |
| EffectComposer, bloom, depth of field, screen effects | `threejs-postprocessing` |

Install the skills once per machine with `npx skills add cloudai-x/threejs-skills -g --all`. Install packages following `../package-installation/npm.md`: `npm install three@latest` and `npm install -D @types/three@latest`.

For DOM and UI animation around the scene (not inside it), use GSAP as described in `interaction-accessibility.md`.

## Rules for Next.js and React

- Three.js runs only in client components (`"use client"`). Load heavy scenes with `next/dynamic` and `ssr: false` so they do not block the first render.
- If the project already uses React Three Fiber, keep using it; do not mix it with a hand-written renderer in the same view. Otherwise use plain Three.js inside a client component.
- On unmount, stop the animation loop and dispose of geometries, materials, textures, and the renderer, or memory leaks on every navigation.

## Performance and accessibility

- Cap the pixel ratio: `renderer.setPixelRatio(Math.min(window.devicePixelRatio, 2))`.
- Render on demand for static scenes instead of a constant animation loop; pause rendering when the canvas is off-screen or the tab is hidden.
- Respect `prefers-reduced-motion`: stop auto-rotation and ambient animation, and keep user-driven interaction.
- Show a loading state while models load and an error or fallback image if WebGL is unavailable.
- Give the canvas an accessible name (`role="img"` and `aria-label`) or a text description, and make any 3D control also reachable from normal buttons.
