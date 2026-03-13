# Audit Checklist

Complete workflow for auditing design system consistency.
Read this when the mode is **Auditar**.

---

## Overview

A design system audit scans the project for violations of the design system:
token drift, hardcoded values, WCAG violations, component inconsistencies,
and documentation gaps.

---

## Step 1: Scan for Token Drift

Search the entire project for values that should come from the design system
but are hardcoded instead.

### Colors

```
Search for:
- Hex colors: #[0-9a-fA-F]{3,8}
- RGB: rgb\(, rgba\(
- HSL: hsl\(, hsla\(
- OKLCH: oklch\(

Where to search:
- components/**/*.tsx
- app/**/*.tsx
- app/**/*.css (exclude globals.css -- that's the source of truth)
- Any .module.css files

Exclude:
- globals.css (source of truth)
- node_modules/
- .next/
- components/ui/ (shadcn auto-generated, acceptable)
```

**For each hardcoded color found:**
1. Check if a matching CSS variable exists in globals.css
2. If yes → report as "should use token" with suggested replacement
3. If no → report as "needs new token" with suggested token name

### Spacing

```
Search for:
- Arbitrary Tailwind values: p-\[, m-\[, gap-\[, space-\[
- Inline style spacing: padding:, margin:, gap: (with px values)

Check values against 8pt grid: 0, 4, 8, 12, 16, 20, 24, 32, 40, 48, 64, 80, 96, 128
Any value NOT on this grid is a violation.
```

### Typography

```
Search for:
- Arbitrary font sizes: text-\[, font-size:
- Inline font weights: font-weight: (with numeric values)
- Font families not from the system

Check against the project's type scale (in globals.css or tokens file).
```

### Border Radius

```
Search for:
- Arbitrary radius: rounded-\[, border-radius:

Check against the project's radius scale.
Nested elements should have SMALLER radius than parents.
```

### Shadows

```
Search for:
- Arbitrary shadows: shadow-\[, box-shadow:

Check against the project's shadow scale.
```

---

## Step 2: Check WCAG Compliance

### Color Contrast

For each text element with explicit color:
1. Determine text color and background color
2. Calculate contrast ratio
3. Flag if below 4.5:1 (normal text) or 3:1 (large text 18px+)

**Common violations:**
- `text-muted-foreground` on `bg-muted` -- check contrast
- Light gray text on white/light backgrounds
- Colored text (success, warning) on light backgrounds
- Text over images or gradients without overlay

### Form Accessibility

```
Search for:
- <input without associated <label
- <textarea without associated <label
- <select without associated <label
- placeholder used as only label
- Custom inputs without aria-label
```

### Touch Targets

```
Search for buttons, links, interactive elements with:
- height < 44px or width < 44px
- padding that results in < 44px touch area
- Icon-only buttons without sufficient size
```

### Focus Indicators

```
Check for:
- outline: none or outline: 0 without replacement focus style
- Custom components missing focus-visible styles
- Interactive elements not reachable via Tab
```

---

## Step 3: Check Component Consistency

### Duplicate Patterns

Search for components that do the same thing differently:

```
Search for:
- Multiple card-like components with different patterns
- Multiple button styles not using the Button component
- Inline implementations of existing components (e.g., custom dropdown
  when DropdownMenu exists)
- Direct DOM elements (div with onClick) instead of proper components
```

### Missing States

For each component in `components/ui/` and `components/`:

Check if the following states are handled:
- [ ] Default/resting state
- [ ] Hover state
- [ ] Focus state (visible ring)
- [ ] Disabled state
- [ ] Loading state (where applicable)
- [ ] Error state (where applicable)
- [ ] Empty state (where applicable)

### Component Usage Patterns

```
Check for:
- Components imported but never used
- Components used differently across pages (inconsistent props)
- Inline styles overriding component defaults
- className props fighting with component styles
```

---

## Step 4: Check Dark Mode

### Token Completeness

1. Read all variables in `:root {}` from globals.css
2. Read all variables in `.dark {}` from globals.css
3. Compare: every :root variable should have a .dark equivalent
4. Flag missing dark mode variables

### Component Dark Mode

```
Search for:
- Hardcoded colors that won't adapt to dark mode
- Components using light-only colors (e.g., bg-white instead of bg-background)
- Shadows that won't work on dark backgrounds
- Images or icons that become invisible in dark mode
```

---

## Step 5: Check Documentation

### Styleguide Completeness

1. List all components in `components/ui/` and `components/`
2. List all showcase pages in `app/styleguide/components/`
3. Compare: every component should have a showcase page
4. Flag components without documentation

### Navigation Accuracy

1. Read `app/styleguide/navigation.ts`
2. Compare with actual showcase pages
3. Flag: items in nav that don't have pages, pages that aren't in nav

---

## Step 6: Generate Report

### Scoring

Calculate score based on findings:

| Category | Weight | Scoring |
|----------|--------|---------|
| Token coverage | 30% | % of values from design system |
| WCAG compliance | 25% | % passing contrast, labels, targets |
| Component consistency | 20% | % using DS components vs. custom |
| Dark mode completeness | 15% | % of tokens with dark mode values |
| Documentation coverage | 10% | % of components with showcase pages |

**Score calculation:**
- 9-10: Excellent -- minimal drift, fully accessible, well-documented
- 7-8: Good -- some drift, minor issues, mostly documented
- 5-6: Fair -- significant drift, accessibility gaps, sparse docs
- 3-4: Poor -- heavy drift, multiple violations, minimal docs
- 1-2: Critical -- design system exists but isn't being followed

### Report Format

```
Design System Audit: [project name]
Date: [date]
Score: [X/10] -- [one-sentence summary]

Token Coverage: [X]% of values come from the design system
  - Colors: [X]% tokenized, [Y] hardcoded values found
  - Spacing: [X]% on 8pt grid, [Y] arbitrary values found
  - Typography: [X]% from type scale
  - Radius: [X]% from radius scale
  - Shadows: [X]% from shadow scale

WCAG Compliance:
  - Contrast: [X] passing, [Y] violations
  - Labels: [X] inputs with labels, [Y] without
  - Touch targets: [X] meeting 44px, [Y] below

Critical (breaks consistency or accessibility):
1. [File:line] [Finding] → [Fix]
2. [File:line] [Finding] → [Fix]

Important (drift or inconsistency):
1. [File:line] [Finding] → [Fix]
2. [File:line] [Finding] → [Fix]

Maintenance (cleanup and documentation):
1. [Finding] → [Action]
2. [Finding] → [Action]

Healthy patterns (what's working well):
1. [Specific positive finding]
2. [Specific positive finding]

Recommended Actions (prioritized):
1. [Highest impact fix] -- affects [X] files
2. [Next priority] -- affects [X] files
3. [Next priority] -- affects [X] files
```

---

## Quick Audit Mode

For a fast check (< 5 minutes), focus only on:

1. **Hardcoded colors** in components/ and app/ (excluding globals.css and components/ui/)
2. **Arbitrary Tailwind values** (p-[X], m-[X], text-[X])
3. **Missing dark mode tokens** (compare :root vs .dark)
4. **Undocumented components** (components without showcase pages)

Report in abbreviated format:

```
Quick Audit: [project name]
Score: [X/10]

Hardcoded colors: [X] found in [Y] files
Arbitrary values: [X] found in [Y] files
Dark mode gaps: [X] tokens missing
Undocumented components: [X] of [Y] total

Top 3 fixes:
1. [Fix]
2. [Fix]
3. [Fix]
```

---

## Notes

- Always exclude `node_modules/`, `.next/`, `dist/`, `build/` from scans
- `components/ui/` files are auto-generated by shadcn -- hardcoded values
  there are acceptable (they reference CSS variables internally)
- `globals.css` is the source of truth -- don't flag values defined there
- Focus on actionable findings with specific file paths and line numbers
- Prioritize fixes by impact: how many files affected, how visible to users
