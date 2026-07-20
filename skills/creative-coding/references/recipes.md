# Recipes -- from easiest to most advanced

Each recipe lists its tier, effort, and a starter prompt to adapt. Always build
the effect on a throwaway route (a `/lab` page) first, iterate in the browser,
and integrate into the real page only once it is approved.

Suggested order of attack: **1 -> 2 -> 3 -> 4 -> 5.** Each teaches what the next
one needs.

---

## 1 -- Global smooth scroll (tier 1, low effort, high impact)

The best return of all. Changes how the whole site feels without touching a
single section.

```
Add smooth scroll with Lenis in the site layout (App Router).
I want a smooth scroll, light weight, no exaggeration. It must respect
prefers-reduced-motion (disable for people who asked for less motion) and
coexist with anything that already reads window.scrollY (e.g. a canvas that
tracks scroll). Client component, wired into the root/locale layout.
```

Note: if the site uses GSAP ScrollTrigger, keep it in sync with Lenis (a single
sync bridge) so scroll-driven animations match the smoothed scroll.

---

## 2 -- Scroll reveals (tier 1, low effort)

Elements enter as they hit the viewport. Start from CSS/IntersectionObserver;
level up with GSAP ScrollTrigger timelines for finer control of when and how each
element enters.

```
Animate the entrance of the [cards/sections] as they enter the viewport:
rise 24px + fade, 80ms stagger between them, smooth curve.
Use GSAP + ScrollTrigger with the useGSAP hook. Respect prefers-reduced-motion.
Show me how to tune the distance and the stagger myself afterward.
```

---

## 3 -- Evolve an existing point/particle field (tier 2, medium effort)

Make a canvas 2D field more alive without rewriting: a slow noise wave crossing
the field, or inertia on the mouse glow (the glow chases the cursor with lag).

```
In the existing canvas point-field component, add a subtle noise wave
(Perlin/simplex) that slowly travels across the field, on top of the mouse glow.
Very low amplitude, so it "breathes" without distracting from the text.
Keep performance: same requestAnimationFrame, no heavy lib.
Put speed and amplitude in constants at the top so I can tune them.
```

---

## 4 -- Liquid image distortion on hover (tier 3, medium-high effort)

The classic agency effect: a card's cover image ripples or "melts" slightly on
hover and settles on leave. Shines when real cover images exist. Depends on a
shader but stays manageable via R3F.

```
I want a hover effect on the [project/gallery] cards: the cover image distorts
slightly (liquid ripple) and returns on leave, like the image hovers on
noomoagency. Subtle, elegant, not cartoonish. Use react-three-fiber + a simple
shader. Isolated component on a /lab route first, so I can validate before
integrating. Fall back to a static image on mobile and respect
prefers-reduced-motion.
```

---

## 5 -- Floating 3D object in the hero (tier 3, high effort)

A 3D form that turns slowly and reacts lightly to the mouse, behind or beside the
headline. The "WebGL moment" that signals you work with this. Start from a simple
geometry (distorted sphere, torus), not an imported model.

```
I want a 3D object in the hero: an organic form (a sphere with surface noise
distortion) that turns slowly and reacts subtly to mouse movement. Matte
material, in the site palette (dark background). react-three-fiber + drei.
Load with dynamic import ssr:false, pause when offscreen, static fallback on
mobile. On an isolated /lab route first.
```

---

## The method, every recipe

Same loop each time: you write the isolated component and explain the parameters;
they look in the browser; they adjust with concrete vocabulary (see
`motion-craft.md` and the main SKILL for the tuning vocabulary); integrate only
when it is approved. Nothing enters an approved page before it is seen running.
