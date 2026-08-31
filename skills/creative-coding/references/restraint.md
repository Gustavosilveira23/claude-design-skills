# Restraint -- the motion you should not build

This skill is good at adding movement. That is the easy half. The expensive
mistake is not a badly built effect; it is a well-built effect that should not
have existed. Nobody files a bug for "too much motion" -- the product just feels
tiring, and nobody can say why.

`motion-craft.md` covers restraint as a principle. This file makes it a decision
you can actually run.

---

## The gate: four questions before any effect

Answer all four before writing code. A "no" on 1, or a "yes" on 4, kills the
effect.

1. **What does the movement tell the user that the static frame does not?**
   Valid answers: where this came from, what changed, that the system heard you,
   how these two things relate, that something is still working. "It looks nice"
   is not an answer -- that is Brand context, and it needs to be named as such
   (see the Brand exception below).
2. **How often will one person see this?** Once per session is a budget. Forty
   times an hour is a tax. See the frequency matrix.
3. **What does it cost when it fails?** Slow device, reduced-motion on, a fast
   user clicking through, an interrupted state. If the failure mode is a stuck
   or blocked interface, the movement is now a bug surface.
4. **Would removing it make anything worse?** Build the static version, look at
   it, and be honest. If nothing is lost, you found your answer.

## The frequency matrix

The rule that settles most arguments: **animation cost scales with frequency and
falls with novelty.**

| | Low frequency | High frequency |
|---|---|---|
| **High novelty** (first time, rare, meaningful) | Animate. This is where motion earns its keep -- onboarding, a first success, a rare destructive confirm. | Animate, but shorten hard. It stops being novel by the fifth time. |
| **Low novelty** (routine, expected) | Light or none. A subtle transition at most. | **None.** This is the tax. |

The bottom-right cell is where almost all bad motion lives: context menus,
hovering rows in a table, adding and deleting list items, expanding a tree,
switching tabs in a tool someone uses all day.

macOS gets this right and it is worth copying: the native right-click menu
animates **out** but not **in**. Opening happens constantly, so it is instant;
closing is rarer and gets to be smooth.

## Where motion genuinely earns it

Short list on purpose. If the effect is not on it, argue for it explicitly.

- **Spatial continuity.** An element that moves from A to B instead of teleporting
  -- a card expanding into a detail view, a drawer coming from the edge it lives
  on. The movement carries the "where am I" the layout cannot.
- **Cause and effect.** Something changed because you did something. The
  connection is the message.
- **Continuity across a route change.** A shared element that persists tells the
  user the page did not reset.
- **Progress and system status.** Something is still working. This is the one
  case where looping motion is honest.
- **Attention direction on a first encounter.** Once. Onboarding, an empty state
  the user just emptied, a first success.
- **Brand expression on a Brand-context surface.** Landing page, hero, portfolio.
  Legitimate -- but say out loud that this is the reason, because it is the
  reason most often used to smuggle in Product-context ornament.

## Where motion always loses

- **Anything blocking the next action.** If the user has to wait out an animation
  to click, the animation is now latency you built on purpose.
- **Frequent, expected interactions.** See the matrix.
- **Data changing under a working user.** A dashboard where numbers roll up on
  every poll is unreadable. Animate the first paint, not the updates.
- **More than one thing competing for the eye at once.** Two effects on one
  screen means neither is a focal point.
- **Anything that moves while text is being read.** The headline always wins.
- **Decorating a slow response.** A skeleton that animates does not make the
  wait shorter; it makes the wait visible. Fix the wait.

## The removal test

The fastest way to settle it, and it beats any argument:

1. Comment out the animation.
2. Look at the static version for a full ten seconds.
3. Name what you lost, in one sentence, in terms of what the user now does not
   know.

If the sentence is about the user -- "you cannot tell the panel came from the
sidebar" -- keep it. If the sentence is about you -- "it feels flat", "it looks
unfinished" -- you are describing a static design problem, and motion is the
wrong fix. Go fix the static design.

## Cutting instead of deleting

Most over-animated effects are not wrong, just too loud. Try these before you
kill it:

- **Halve the duration.** Most interaction motion should land at or under 200ms.
  If it survives being twice as fast, it was too slow.
- **Drop one property.** An entrance that fades, scales, blurs and translates is
  doing four jobs. Two is usually enough.
- **Shrink the magnitude.** Scale from 0.96 rather than 0.8. Translate 8px rather
  than 40px.
- **Move it to the exit only.** Or to the entrance only. Both directions rarely
  need equal weight, and exits should be the subtler of the two.
- **Keep it, but only on first mount.** Not on every re-render, not on every
  data refresh.

## Say it precisely so the agent does not overshoot

An agent asked for "a nice animation" produces a 600ms bouncy ease-in-out on
everything. The fix is naming the four parameters. Give all four and you get the
motion you pictured in one round instead of five.

| Parameter | Say it as |
|---|---|
| **Trigger** | on mount / on hover / on press / on scroll into view / on state change |
| **Properties** | opacity and translateY only / opacity, scale and blur / transform only |
| **Magnitude** | from 8px below / scale from 0.96 / blur 4px to 0 |
| **Timing** | 150ms ease-out / spring, no bounce, ~0.4s / 80ms stagger between items |

Two more words worth knowing, because they change the whole feel:

- **Tween vs spring.** A tween has a fixed duration; a spring has physics and
  settles. Springs feel better for anything the user drags or dismisses. Say
  "spring, no bounce" unless you actually want overshoot -- `bounce: 0` is the
  professional default and `bounce: 0.3` already reads as playful.
- **Interruptible.** CSS transitions retarget mid-flight; keyframe animations run
  their fixed timeline. Anything a user can toggle must be a transition, or the
  interface will ignore a second click and feel broken.

### Curve reference

Defaults that are correct more often than not:

| Situation | Curve |
|---|---|
| Entering | ease-out -- `cubic-bezier(0, 0, 0.2, 1)` |
| Leaving | ease-in -- `cubic-bezier(0.4, 0, 1, 1)` |
| Moving / resizing in place | ease-in-out -- `cubic-bezier(0.4, 0, 0.2, 1)` |
| Progress, shimmer, marquee | linear -- the only honest use |
| Dragged or dismissible | spring, `bounce: 0` |

To compare curves visually rather than guessing at bezier numbers:
[easing.dev](https://www.easing.dev/).

Never `transition: all`. Name the properties -- it is the most common motion
defect in generated CSS, and it animates things you did not intend the moment
someone adds a style.

## Reporting a "no"

When the answer is that an effect should not be built, say it in one line and
offer the cheaper thing. Do not lecture:

> Skipping the animation on the table rows -- this is a high-frequency
> interaction, so motion there reads as lag. A 100ms background transition on
> hover gives the same feedback without the cost.

Then build the cheaper thing. A refusal without a replacement is not restraint,
it is just a no.
