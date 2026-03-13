# Component Taste Guide

Framework-agnostic reference for common UI patterns. For each component: what
good looks like, and the mistakes AI-generated UI consistently makes.

---

## Cards

**Good taste:**
- Generous internal padding. Content breathes, doesn't press against edges.
- Clear hierarchy: one heading, one supporting detail, one action. In that order.
- Visual weight concentrated at the top (image or heading) with details flowing downward.
- Consistent card dimensions in a grid. Alignment communicates system.
- Subtle shadow for elevation, soft and nearly invisible. Layer two shadows for depth: tight ambient + softer directional.
- Hover state that's subtle (slight shadow increase), not dramatic.
- Color accents belong INSIDE the card (colored titles, values, dot indicators). Never as a colored top-border on a rounded card.

**Common AI mistakes:**
- Cramming 5-6 elements into one card (badge + icon + title + subtitle + description + two buttons + status + timestamp).
- Every card has a different internal structure, breaking grid rhythm.
- Loud, saturated gradient backgrounds on every card.
- Equal visual weight on all text, no distinction between heading and metadata.
- Rounded corners so large the card looks like a pill.
- Colored top-border accents on rounded cards (straight line clashes with curves).
- Using `border: 1px solid` for containment instead of a soft shadow.

---

## Modals / Dialogs

**Good taste:**
- One focused task or decision. A modal should do one thing.
- Clear title that states the action ("Delete this project?" not "Confirm").
- Obvious dismiss path: close button AND clicking overlay AND escape key.
- Overlay with backdrop blur preserves spatial context.
- Primary action button reflects the action's nature (destructive = red, confirmation = primary color).

**Common AI mistakes:**
- Using modals for content that should be a page (long forms, multi-step flows).
- No visual hierarchy inside. Flat list of fields with uniform styling.
- Confirmation modals that say "Are you sure?" without stating what will happen.
- Two buttons that look identical for destructive vs. safe actions.
- Missing escape hatch.

---

## Tables / Data Grids

**Good taste:**
- Right-aligned numbers, left-aligned text. Column alignment matches data type.
- Clear header row with visual weight distinguishing it from data rows.
- Alternating row backgrounds OR subtle row dividers, not both.
- Cell padding that allows scanning (minimum 12px vertical per row).
- Sortable columns indicated clearly (icon + current sort state visible).

**Common AI mistakes:**
- Everything center-aligned regardless of data type.
- Dense rows with no breathing room.
- Every column the same width regardless of content.
- Heavy borders on every cell creating a spreadsheet feel.
- No distinction between primary and secondary/metadata columns.

---

## Forms

**Good taste:**
- Logical grouping. Related fields together, separated by spacing or section headings.
- Labels above inputs (not placeholder-as-label).
- Error messages adjacent to the field, not in a banner at the top.
- Clear required vs. optional distinction (mark the minority).
- Progressive disclosure. Don't show 20 fields when 5 are relevant to start.

**Common AI mistakes:**
- Flat list of fields with no grouping or visual rhythm.
- Using placeholder text as labels (accessibility + UX failure).
- All fields same width regardless of expected content.
- Submit button that doesn't reflect the action ("Submit" instead of "Create Account").
- No indication of progress in multi-step forms.

---

## Navigation

**Good taste:**
- Clear indication of current location (visually distinct active state).
- Reasonable depth. Primary nav visible, secondary revealed in context.
- Consistent position. Nav shouldn't move between pages.
- Mobile nav that's accessible without complex gestures.
- Logical grouping. Related items together.

**Common AI mistakes:**
- Too many items at the top level (8+ primary nav items competing).
- Active state is subtle font-weight or color change that's hard to spot.
- Icon-only nav with no labels and no tooltips.
- Hamburger menu on desktop when there's room for visible navigation.
- Dropdowns nested 3+ levels deep.

---

## Buttons

**Good taste:**
- Clear primary/secondary/tertiary hierarchy. One style dominates, others support.
- Button text describes the action ("Save Changes" not "Submit").
- Size proportional to importance and context.
- Adequate padding. Horizontal padding > vertical padding.
- The "Label, Qualifier" pattern for CTAs: "Get Started, It's Free".
- Disabled state clearly non-interactive (reduced opacity + cursor change).

**Common AI mistakes:**
- Multiple button styles with no clear hierarchy.
- Generic labels ("Submit", "OK", "Click Here", "Yes").
- Buttons too small to tap on mobile (under 44px height).
- Decorative treatments (gradients, shadows, animated borders) on every button.
- "Cancel" and "Delete" styled identically.

---

## Empty States

**Good taste:**
- Explains what will appear here and how to populate it.
- Single clear CTA to take the first action ("Create your first project").
- Tone matches the product. Warm and encouraging, not clinical.
- Illustration or icon is supplementary, not the focal point.
- Vertically centered in the available space.

**Common AI mistakes:**
- Just "No data" or "No results found" with no guidance.
- Generic stock illustration unrelated to the feature.
- Empty state styled completely differently from the populated state.
- Multiple CTAs competing in a single-focus moment.
- Tiny text lost in a huge empty container.

---

## Status Indicators / Badges

**Good taste:**
- Semantic color: green=success, yellow=warning, red=error, blue=info, gray=neutral.
- Readable at small sizes. Sufficient contrast.
- Consistent shape and size across the application.
- Used sparingly. If every item has 3 badges, none stand out.
- Text labels that are scannable ("Active", "Pending", not "Status Code 200").

**Common AI mistakes:**
- Rainbow of badge colors with no semantic meaning.
- Badges so small the text is illegible.
- Too many badges per item (status + category + priority + type + date).
- Inconsistent styling (pills, squares, and colored text mixed).

---

## Toasts / Notifications

**Good taste:**
- Minimal. Just enough text to confirm or communicate.
- Auto-dismiss for confirmations (3-5 seconds). Persist for errors.
- Positioned consistently (top-right or bottom-center, pick one).
- Don't block page interaction.
- Semantic styling for success/error/warning/info.

**Common AI mistakes:**
- Full sentences when 3 words would do ("Changes saved" not "Your changes have been successfully saved to the database").
- Stacking 5+ toasts that obscure content.
- Error toasts that auto-dismiss before users can read them.
- Using toasts for critical info that should be inline.
- Identical styling for success and error.

---

## Dashboards

**Good taste:**
- Clear information hierarchy. KPIs/summary at top, detail below.
- Cards sized proportional to importance. Most critical metric gets most space.
- Scannable at a glance (understand overall status in 3 seconds).
- Consistent card styling within the dashboard.
- Meaningful empty space between sections communicating grouping.

**Common AI mistakes:**
- Every card the same size regardless of content importance.
- Too many metrics with no hierarchy (12 identical KPI cards).
- Charts with no context (line going up -- is that good or bad?).
- Dense layout with no breathing room.
- Decorative chart types (3D pie charts, radial gauges) that obscure data.
