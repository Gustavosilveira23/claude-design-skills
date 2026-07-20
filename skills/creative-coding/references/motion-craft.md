# Motion craft -- the designer edge and the fundamentals

The tools and libraries change; these do not. Block A is taste (where a designer
beats a dev who knows the API). Block B is the reusable technical base. If you
study only one thing, study Block A.

---

## Block A -- what pays off most for a designer

This is taste, not syntax. It is where you lead a dev who knows the API but not
what looks good.

- **The 12 principles of animation (Disney) applied to UI** -- anticipation,
  follow-through, staging, secondary action, slow-in/slow-out. This is what
  separates a living movement from a robotic one. Studying this pays more than
  any library.
- **Easing and timing as craft** -- understand *why* an ease-out feels natural
  and a linear feels dead. Knowing the why changes how you tune everything.
  - Ease-out for entering elements (fast start, gentle landing).
  - Ease-in for leaving elements (slow start, fast exit).
  - Ease-in-out for repositioning (smooth throughout).
  - Never linear except progress bars and shimmer loops.
- **Choreography and orchestration** -- stagger, hierarchy of movement, what
  enters first and what follows. Composition in time; a designer already thinks
  this way in layout.
- **Deconstructing references** -- open a site that impresses you, name the
  technique, isolate the parameter. A movement "swipe file" (screenshots + links)
  is worth as much as a moodboard.
- **When NOT to animate** -- restraint is craft. Movement that does not serve the
  content becomes noise. The headline always wins.

---

## Block B -- technical fundamentals that last

Learn once, reuse in every tool. These are concepts, not libraries.

- **Interpolation and damping** (`lerp`, chasing the target with lag) -- the
  secret of smoothness and inertia. Nearly every mouse-reactive movement with
  elegance uses this.
- **Noise (Perlin/Simplex)** -- the base of organic generative movement. What
  makes a wave look natural instead of mechanical.
- **The minimal math** -- `sin`/`cos` (wave and circular motion), vectors and
  distance (point-to-cursor), `map`/`remap` (convert value ranges), delta time
  (frame-rate-independent motion). A handful of functions, not heavy calculus.
- **Performance as material** -- the 16ms/frame budget (60fps), what causes jank,
  CPU vs GPU. Separates "runs on my machine" from "runs on everyone's phone".
- **Ethics of motion** -- `prefers-reduced-motion`, vestibular nausea, never
  sacrificing usability. As a designer this is your responsibility.

---

## If you only pick one thing now

Study **easing and the animation principles (Block A)**. Cheap, installs nothing,
instantly improves everything you already do with CSS/Framer Motion, and it is
the base for judging whether any effect landed or looks amateur. Noise, shaders
and Rive pay off more later, once the eye is trained for timing.
