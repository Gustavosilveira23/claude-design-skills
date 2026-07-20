# Toolkit -- stack, tiers, and designer shortcuts

The tools and mental map behind the effects. Pick by objective; do not install
the whole list up front.

---

## The three tiers of effort (detail)

### Tier 1 -- DOM, CSS, Framer Motion
HTML elements animated: fade, translate, stagger, route transitions, text
entrances. Cheap, accessible, great for SEO. Covers section reveals, button
hover, text entrance. **Limit:** cannot draw a particle, distort an image, or do
3D.

### Tier 2 -- Canvas 2D
A surface you paint by code. Particles, point fields, mouse-reactive lines,
generative noise. This is Processing/p5.js territory. Runs on CPU, so it has a
ceiling: a few thousand moving particles already tax a phone.

### Tier 3 -- WebGL (Three.js / shaders)
GPU compute. The "impossible" effects: liquid image distortion on hover, millions
of particles, 3D scenes, a drivable car (bruno-simon.com). Most expensive tier --
bigger bundle, extra mobile care, and GLSL shaders are almost a second language.
Worth it for one or two hero moments, rarely the whole site. To direct and tune
shader looks without writing GLSL, see [shaders.md](shaders.md).

---

## The stack, by objective

In a React/Next project, prefer the component versions so 3D becomes a `<mesh>`
in your JSX instead of a parallel script fighting React.

- **Scroll-tied animation and precise timelines** -> `gsap` + `@gsap/react`
  (the `useGSAP` hook) + the `ScrollTrigger` plugin. Industry standard for scroll
  choreography.
- **Buttery smooth scroll** -> `lenis` (React wrapper `lenis/react`, `<ReactLenis>`).
  This is the premium-feel scroll. Cheap to add, big effect.
- **3D in the browser, in React** -> `@react-three/fiber` (Three.js as components,
  aka R3F) + `@react-three/drei` (ready-made helpers: camera, lights, 3D text,
  controls).
- **Post-processing (bloom, blur, glitch)** -> `@react-three/postprocessing`.
- **UI animations you may already have** -> `framer-motion`. It handles tier 1
  well; keep it or replace with CSS/GSAP depending on the project.

**Do NOT start with:** raw GLSL from scratch, 3D physics (Rapier/Cannon), WebGPU.
Great, but the top of the mountain -- reach them after R3F and GSAP feel natural.

---

## Processing (faculty) -> web vocabulary

Same ideas, different runtime. Useful when the person has a Processing/p5
background.

| Processing (Java) | Web equivalent | Notes |
|---|---|---|
| `setup()` / `draw()` | `requestAnimationFrame` loop | the animation loop |
| Canvas 2D | Canvas API 2D | CPU raster |
| `P3D` / OpenGL | WebGL via Three.js / R3F | GPU |
| Shaders GLSL | Shaders GLSL (identical) | same language |
| `map()`, `lerp()`, `noise()` | same functions, by hand or via lib | reusable |

The mental model transfers directly: loop, coordinates, distance, time, color.
What changes is *where* the calc runs (CPU -> GPU) and *which tools* make it
viable without writing everything from scratch.

---

## Designer shortcuts (visuals without writing shaders)

Visual tools that generate animation/3D for the web without coding from zero.
Aligned to a Figma -> implementation flow.

- **Rive** -- interactive animation with state machines, light runtime, runs in
  React. Design and wire the logic in the editor; the site just consumes it.
  Often the most useful for a designer.
- **Spline** -- 3D editor in the browser, exports to React. Good to prototype a
  hero 3D object without touching Three.js.
- **Lottie** -- vector animations from After Effects, light, good for icons and
  micro-interactions.
- **The Book of Shaders** (free, online) -- when ready to climb. Teaches thinking
  "per pixel", the key shift for WebGL.

---

## Resources

- **Three.js Journey** (Bruno Simon) -- the definitive WebGL/Three.js course.
  Paid, English.
- **editor.p5js.org** -- play with creative coding Processing-style, no install.
  Good to prototype a movement idea before bringing it to the site.
- **react-three-fiber + drei docs** -- `docs.pmnd.rs`.
- **GSAP docs + ScrollTrigger** -- `gsap.com/docs`. Focus on ScrollTrigger and
  the `useGSAP` hook.
- **Lenis** -- `github.com/darkroomengineering/lenis`. Quick smooth-scroll setup.
- **Codrops** -- `tympanus.net/codrops`. Agency-effect tutorials (image hover,
  WebGL transitions) with open code. Great for stealing parameter references.
- **Awwwards / Godly** -- visual reference hunting. Found an effect? Bring the
  link and deconstruct the technique + parameters.
