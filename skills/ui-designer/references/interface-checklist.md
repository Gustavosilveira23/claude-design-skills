# Interface Checklist

The verifiable layer of polish. Every item here is a **binary check** -- you either
did it or you did not, and you can prove it by reading the CSS or the markup.

This file is deliberately different from the other references:

| File | Answers |
|------|---------|
| `component-taste.md` | What should this component be? |
| `polish-and-craft.md` | What effect makes it feel premium? |
| `ai-slop-detector.md` | What makes it look generated? |
| **this file** | **What detail is measurably missing?** |

Use it when polish is the task and "it looks off" is the complaint. Judgment
finds the problem; this list finds the cause.

## How to run it

1. Do not read all 9 sections. Pick the 2-3 that match what you are touching.
2. For each item, **check the code, not the screenshot**. A rendered image cannot
   tell you whether `transition: all` is in there.
3. Report a failed item as: rule broken -> where -> the one-line fix.
4. If an item does not apply, skip it silently. Do not pad an audit with N/A rows.

The **Quick Pass** at the bottom is the 12-item version for small changes.

---

## 1. Nesting and alignment

The two items that most consistently separate professional from amateur, and the
two nobody notices consciously.

- **Concentric border radius on any nested element.** `outer radius = inner radius
  + padding`. A 12px card inside 8px padding needs a 20px outer radius.
  *Check:* find every element with a radius that contains another element with a
  radius. Do the arithmetic. Mismatched radii read as "cheap" without the viewer
  knowing why.
- **Optical alignment beats geometric alignment.** When a button holds an icon and
  a label, the icon side needs slightly less padding. Same for any triangle,
  play, or asymmetric glyph.
  *Check:* look for equal padding on both sides of an icon+text button. Equal is
  usually wrong. Fix in the SVG viewBox when you own the icon, with margin when
  you do not.
- **Group gaps are at least 2x the gaps inside a group.** 8px within, 16px+
  between.
  *Check:* read the two `gap` values. If they are the same, the grouping is
  invisible and the eye has to do the work the layout should have done.
- **Images carry a 1px inset outline** -- black at 8% opacity in light, white at
  8% in dark, offset by -1px.
  *Check:* photos sitting directly on the background with no edge treatment. This
  is what makes images look pasted in.
- **Prefer a layered box-shadow over a solid 1px border** on cards and inputs.
  Shadows use transparency, so they survive being placed on an image or a colored
  background; a solid border does not.
  *Check:* `border: 1px solid` on a surface that can move. Three-layer recipe is
  in `polish-and-craft.md`.
- **No fixed width or height on a text container.** Text reflows; boxes that do
  not will clip it in another language.

## 2. Type details

- **Cap long-form measure at 60-75 characters.** *Check:* `max-width` on the
  prose container, or `max-w-prose`.
- **`text-wrap: balance` on headings, `text-wrap: pretty` on descriptions,
  neither on long-form body.** *Check:* headings that break with one orphan word
  on the last line.
- **`font-variant-numeric: tabular-nums` on every number that changes** --
  timers, counters, prices, table columns. Skip if the font is already mono.
  *Check:* a value that updates live and shifts the layout by a pixel or two.
- **`-webkit-font-smoothing: antialiased` set once on the root, never per
  component.** *Check:* grep for it; if it appears more than once you have a
  component that renders differently from its neighbours.
- **Font weight never changes on hover or on the active state.** Weight change
  reflows the text and shifts the layout. Change color or background instead.
- **No font weight below 400.** Medium headings sit best at 500-600.
- **Copy stored in natural case, presentation controlled with `text-transform`.**
  *Check:* `ALL CAPS` typed into the JSX. Now it cannot be lowercased for another
  surface, and screen readers may spell it out.
- **Smart punctuation:** curly quotes, en dash for ranges, em dash for asides, a
  single ellipsis character. *Check:* three periods and straight quotes in
  user-facing strings.
- **Truncated text keeps the full value reachable** via tooltip or expansion. A
  truncation that destroys information is a bug, not a style.
- **`overflow-wrap: break-word` where a long ID, URL or email can appear;
  `white-space: nowrap` on labels and badges.**

## 3. Color and tokens

- **Components consume semantic tokens, never primitives.**
  `--color-text-secondary`, not `--blue-500`. The primitive is the value; the
  token is the job.
  *Check:* grep component files for primitive names. Any hit is drift.
- **A token is never named for its appearance or its first use.**
  `--color-accent-solid`, not `--color-blue-button` or `--color-sidebar-gray`.
- **Never borrow a token from another role because the color happens to match.**
  When that role changes, your element changes with it. Add a token for the new
  role.
- **Every step in the palette has a job** -- page background, hover, border,
  solid fill, body text. A step nothing uses is dead weight.
- **Contrast is measured against the background the element actually renders on**,
  not the page background. A muted label on a card is a different test than the
  same label on canvas.
- **Dark mode is not the light palette inverted.** *Check:* dark values that are
  arithmetic mirrors of the light ones.
- **One theme mechanism for every token:** `prefers-color-scheme` or a `.dark`
  class, never both in the same project.
- **Status is never carried by color alone.** Add an icon, a label, or an
  underline.

## 4. Motion mechanics

Motion craft (what to animate, easing, when to stay still) lives in
`polish-and-craft.md` and the `creative-coding` skill. These are the mechanical
faults.

- **Never `transition: all`.** Name the properties.
  *Check:* grep. This is the single most common motion bug in AI-generated CSS.
- **Interactions use CSS transitions; one-shot sequences use keyframes.**
  Transitions retarget when the user changes their mind mid-animation; keyframes
  run their fixed timeline no matter what. A dropdown that ignores a second click
  feels broken.
  *Check:* keyframe animations on anything a user can toggle.
- **Interaction duration stays at or under ~200ms.** Longer reads as lag.
- **Animation magnitude is proportional to the element.** Dialogs fade and scale
  from ~0.8, not from 0. Buttons press to ~0.96, not to 0.8.
- **Exit animations are subtler than enter animations.** Entering earns
  attention; leaving should not demand it. Animate opacity and blur out rather
  than replaying the full entrance in reverse.
- **Icon swaps cross-fade.** Entering icon: scale 0.25 -> 1, opacity 0 -> 1, blur
  4px -> 0. Exiting reverses. *Check:* an icon that hard-swaps on state change.
- **Entrances are staggered by group, not fired as one block.** ~100ms between
  sections, ~80ms between words when splitting a headline.
- **Theme switching kills all transitions for the duration.** Otherwise every
  hover transition on the page fires at once when the user toggles dark mode.
- **No animation on high-frequency, low-novelty interactions:** hovering rows in
  a list, opening a context menu, adding or deleting list items.
- **Looping animations pause when off-screen.**
- **`will-change` only on properties that actually change** -- `transform`,
  `opacity`, `filter` -- and only as a last resort.

## 5. Inputs and forms

- **Clicking the label focuses the input.** *Check:* `<label htmlFor>` or a
  wrapping label. Missing this is the most common form defect.
- **Inputs live inside a `<form>`** so Enter submits.
- **Correct `type` and `inputmode`** -- `email`, `password`, `numeric`.
- **`spellcheck` and `autocomplete` disabled** where they do not apply.
- **Input font-size is at least 16px** or iOS zooms the whole page on focus.
- **No autofocus on touch.** The keyboard covers the screen.
- **Prefix and suffix icons are absolutely positioned over the input with
  padding**, not laid out beside it, and clicking them focuses the input.
- **Paste is never blocked.** People paste passwords and one-time codes.
- **Submit stays enabled until the request starts**, then: `aria-invalid="true"`,
  `aria-describedby` pointing at the error, focus moved to the first invalid
  field.
- **Submit disables after firing** to prevent duplicate requests.
- **Errors are shown at their trigger** -- highlight the offending input. A
  summary at the top of a long form makes the user hunt.
- **Toggles apply immediately.** A toggle that needs a Save button is a checkbox.

## 6. Hit areas and pointer

- **Minimum hit area 24x24px; 40x40 on desktop, 44x44 on touch where the layout
  allows.** Extended hit areas must not overlap each other.
- **No dead zones between items in a list.** Increase padding rather than adding
  margin -- a 4px gap where nothing is clickable feels like the interface is
  ignoring you.
  *Check:* `gap` between rows in a nav or menu. Convert to padding on the row.
- **Decorative elements get `pointer-events: none`** -- glows, gradients, blurred
  blobs. *Check:* any absolutely positioned ornament without it is swallowing
  clicks.
- **Interactive elements disable `user-select` on their inner content.** Nothing
  reads as unfinished faster than dragging across a button and selecting its
  label.
- **Hover styling sits behind `@media (hover: hover)`.** On touch, `:hover` sticks
  after a tap and the element looks permanently selected.
- **Replace the iOS tap highlight, do not just delete it.**
  `-webkit-tap-highlight-color: rgba(0,0,0,0)` with no substitute removes all
  touch feedback.
- **Dropdown menus open on `mousedown`, not `click`.**
- **Nested menus use a prediction cone** so a diagonal pointer path does not close
  the parent.

## 7. Focus and keyboard

- **Native elements for native jobs.** `<button>` for actions, `<a>` for
  navigation. A `div` with an onClick has no focus, no Enter, no role.
- **Style `:focus-visible`.** Never `outline: none` without a replacement.
- **Focus rings use `box-shadow`, not `outline`** -- outline still ignores border
  radius in older Safari.
- **`tabindex` is only ever 0 or -1.** Positive values break the natural order.
- **Sequential lists are navigable with arrow keys**, and deletable with
  Cmd+Backspace where deletion is a primary action.
- **Icon-only controls carry a descriptive `aria-label`**, and `aria-hidden` never
  lands on a focusable element.
- **Alt text describes purpose, not appearance.** `alt="Search"`, not
  `alt="magnifying glass"`. Decorative images get `alt=""`.
- **A disabled control never carries a tooltip.** It is not in the tab order, so
  the explanation is unreachable. Put the reason in visible text, or use
  `aria-disabled="true"` to keep it focusable.
- **Tooltips triggered by hover contain no interactive content.**
- **Skip-to-content is the first focusable element**, and anchored headings have
  `scroll-margin-top`.
- **`role="status"` for routine updates, `role="alert"` only for urgent errors.**
- **Motion is wrapped in `@media (prefers-reduced-motion: no-preference)`.**

## 8. Feedback and state

- **Feedback appears at its trigger.** An inline checkmark on the copy button,
  not a toast in the corner.
- **Mutations update optimistically and roll back with a message on failure.**
- **Auth redirects resolve on the server** before the client paints, so the user
  never sees a URL flash.
- **The document selection state is styled with `::selection`**, and gradient text
  unsets its gradient there or the selection is unreadable.
- **Empty states offer one next action**, not "No results". Templates if the
  action is creation.
- **Every component has an answer for: empty, loading, error, one item, many
  items, longest realistic string.** If you cannot name the answer, the state
  does not exist yet.

## 9. Microcopy

`ux-designer` owns voice and the AI-tell audit. These are the mechanical rules.

- **Button labels start with a verb.** "Save draft", "Delete project". Never "OK"
  or a bare "Yes".
- **Confirmation buttons repeat the consequence.** "Delete project" beside
  "Cancel", so the destructive option is readable without the dialog text.
- **One word per concept per flow.** "Continue" or "Next", never both.
- **Link text names the destination.** "Read docs", never "Click here".
- **Toggle labels name the state they turn on.** "Send read receipts", not
  "Disable read receipts".
- **Casing is consistent across buttons, headings and labels.** Sentence case is
  the safer default.
- **Address the reader as "you", never "the user".**

---

## Quick Pass

For a small change or a fast second opinion. These 12 catch the majority of real
defects:

1. Concentric radius on nested elements
2. Group gap at least 2x inner gap
3. Icon+text button optically aligned
4. `transition: all` absent
5. Toggleable animation uses a transition, not keyframes
6. Label click focuses the input
7. Hit area 24px minimum, no dead zones between list items
8. `:focus-visible` styled, never removed
9. `pointer-events: none` on decorative layers
10. Tabular numbers on any value that updates
11. Components use semantic tokens, not primitives
12. Empty, loading and error states exist

## Sources

Compiled from three references, cross-checked and deduplicated:

- [Web Interface Guidelines](https://interfaces.rauno.me/) -- Rauno Freiberg
- [Interface Cheat Sheet](https://interfaces.dev/cheat-sheet) -- Jakub Krehel
- [Details That Make Interfaces Feel Better](https://jakub.kr/writing/details-that-make-interfaces-feel-better) -- Jakub Krehel

Where the sources disagreed, the stricter rule was kept. Items already covered by
`polish-and-craft.md` (easing curves, shadow recipes, touch target tables) are
referenced rather than repeated.
