# Shaders -- directing GPU effects without writing GLSL

The Tier 3 companion. You do not need to write GLSL; you need the mental model
and the vocabulary to **direct and tune** a shader effect. Claude writes the
shader; you name the look and the parameter.

---

## The mental model

A fragment shader is a tiny program that runs **once per pixel, all pixels in
parallel, on the GPU**. It receives the pixel's coordinate and returns its color.
No loop over pixels, no "objects" -- just "for this coordinate, what color?".

Consequences worth knowing:

- Cheap for full-screen effects (the GPU does millions of pixels at once),
  awkward to debug (you cannot `console.log` a pixel).
- Inputs arrive as **uniforms** -- values passed from JS: time, mouse, resolution,
  a texture. When you say "react to the mouse" or "animate over time", you are
  feeding a uniform.
- Everything is built from math on the coordinate: distance, angle, noise,
  thresholds. That is why the same handful of functions reappears everywhere.

---

## The concept toolkit (what it does -> the word to direct it)

You do not call these; you describe the look and Claude wires them.

**Shaping functions -- edges and curves**
- `step(edge, x)` -- hard cut at a threshold. -> "hard edge", "on/off".
- `smoothstep(a, b, x)` -- soft, eased transition between two edges. -> "soft
  edge", "feather", "ease the falloff". Wider a..b = softer.
- `mix(a, b, t)` -- blend/lerp between two things by t. -> "fade between", "blend".
- `fract`, `mod`, `clamp` -- fractional part, wrap, keep in range. -> "tile/repeat",
  "wrap".
- `pow(x, k)` -- bends a ramp. -> "punchier falloff" (k>1), "gentler" (k<1).
- `sin` / `cos` -- oscillation. -> "pulse", "wave", "breathing".

**The noise family -- organic vs mechanical**
- `random` (hash) -- static grain. -> "grain", "static", "TV snow".
- `noise` (Perlin/simplex) -- smooth organic variation. -> "organic", "cloudy",
  "flowing".
- **fBm** (fractional Brownian motion = layered noise octaves) -- detail at
  multiple scales. -> "richer detail", "more turbulent", "clouds/marble/terrain".
  More octaves = more fine detail.
- **cellular / Voronoi noise** -- cell-like regions. -> "cells", "cracked",
  "scales", "stained glass", "caustics".
- **domain warping** (feeding noise into the coordinates of more noise) -- flowing
  liquid distortion. -> "melting", "smoky", "liquid flow".

**Image effects (a shader over a texture)**
- **Displacement / distortion** -- push pixels around by a map or noise. -> the
  liquid image hover (recipe 5.4), ripples following the mouse, page-transition warps.
- **Kernel convolution** -- blur, sharpen, edge-detect by sampling neighbors. ->
  "blur on scroll", "soft focus".
- **Chromatic aberration** -- offset the R/G/B channels. -> "glitch", "lens fringe",
  "speed feel".

**Spatial / 3D inside a shader**
- **SDF (signed distance fields) + ray marching** -- render shapes and scenes by
  distance math instead of geometry. -> "blobby 3D", "infinite tunnel", "morphing
  metaballs" without a 3D model. Heavy; a hero moment, not a background.

---

## Vocabulary for tuning a shader (sensation -> concept)

The general tuning vocabulary (see the main SKILL), at the shader layer:

- **Edge:** harder / softer -> `step` vs `smoothstep`; widen the smoothstep band.
- **Detail:** simpler / richer -> fewer / more fBm octaves.
- **Organic vs mechanical:** organic -> noise/fBm; mechanical -> raw `sin`/`step`.
- **Flow / melt:** more -> domain warping; less -> straight noise.
- **Texture look:** grain -> `random`; cells/cracks -> cellular; clouds/marble -> fBm.
- **Motion:** speed -> the time-uniform multiplier; reactivity -> how strongly the
  mouse uniform feeds the distortion.
- **Contrast / punch:** more -> `pow` (k>1) or a tighter smoothstep band.

---

## The Book of Shaders -- chapter map

`thebookofshaders.com` (Patricio Gonzalez Vivo & Jen Lowe). Free. The reference to
pull a parameter or understand a look. Go straight to the chapter that matches the
effect you are directing:

- **Shaping functions** -- edges, ramps, curves (the smoothstep/pow vocabulary).
- **Colors / Patterns / Matrices** -- palettes, tiling, rotate/scale in shader space.
- **Random / Noise / Cellular noise / Fractal Brownian Motion / Fractals** -- the
  whole generative family above.
- **Image processing** (textures, convolutions, filters) -- distortion, blur, and
  channel effects for hover/scroll image work.
- **3D graphics** (ray marching, normals, reflect/refract) -- the SDF / 3D look.
- **Examples gallery + glossary** -- steal a parameter or a look, like Codrops but
  for shaders.

Use it the same way as any reference: find an effect, name the technique, isolate
the parameter, then adapt it on a `/lab` route.

---

## When to reach for a shader at all

Only when the effect genuinely needs per-pixel GPU work: liquid image distortion,
generative full-screen textures/backgrounds, large particle systems, SDF/ray-marched
shapes. If a CSS transition, an SVG filter, or a Canvas 2D loop can do it, stay
lower (see the tiers in `toolkit.md`).

And keep the Tier 3 guardrails every time: `"use client"` + `ssr: false`, pause
offscreen, `prefers-reduced-motion` fallback, capped `dpr`, and lazy-load the heavy
libs so the weight lands only on the page that uses the effect.
