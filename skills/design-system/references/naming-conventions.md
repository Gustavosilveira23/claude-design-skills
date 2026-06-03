# Naming Conventions

Universal principles for naming tokens, components, and props in a design
system. Project-specific rules (prefixes, scales, exact patterns) live in
the project's `design-system-context.md`, not here.

---

## Why naming matters for AI

When names diverge between Figma and code, AI has to guess the mapping.
Guesses are where hallucinations and errors happen. Consistent, predictable
names are the cheapest way to make a design system AI-friendly.

**The test:** if a designer and an engineer separately list the same
component or token, they should write the same name without coordination.
If they don't, the naming convention is broken.

---

## Universal principles

### 1. Semantic over visual

Name things by **role**, not appearance.

| Good (semantic) | Bad (visual) |
|------|-----|
| `color-action-primary` | `blue-500` |
| `color-feedback-error` | `red-600` |
| `spacing-section-y` | `space-32` |
| `text-body-default` | `text-16` |

**Why:** visual names break the moment you rebrand, theme, or adapt the system.
Semantic names survive.

**Exception:** primitive scales (`gray-100` through `gray-900`) can keep visual
names -- they're the raw material that semantic tokens reference, not the
tokens used in components.

### 2. Same name in Figma and code

If a component is `PrimaryButton` in code, it is `PrimaryButton` in Figma.
Same casing, same separator, same word order.

This sounds obvious. It is also where most systems silently drift.

**Audit periodically:** export Figma library names, compare to component
filenames in code, flag any divergence.

### 3. One convention per category, applied consistently

Pick a casing convention per category and never mix within it.

| Category | Convention example | Example |
|----------|---------------------|---------|
| Tokens (CSS variables) | kebab-case | `--color-action-primary` |
| Components (code) | PascalCase | `PrimaryButton` |
| Component files | PascalCase or kebab-case (project choice) | `PrimaryButton.tsx` |
| Component props | camelCase | `isLoading`, `variant` |
| Component variants (values) | camelCase or kebab-case | `primary`, `secondary` |
| Showcase URLs | kebab-case | `/styleguide/components/primary-button` |

The exact choice matters less than picking one and sticking with it.

### 4. Descriptive without being verbose

Names should communicate purpose at a glance.

- Too short: `--c1`, `--bg`, `--p`
- Too verbose: `--color-of-the-primary-button-background-default-state`
- Just right: `--color-action-primary`, `--bg-card`, `--text-body`

**Rule of thumb:** if a name needs a comment to explain it, rename it.

### 5. Structure: category → role → variant → state

Layer specificity from general to specific:

```
[category]-[role]-[variant?]-[state?]

color-action-primary              -- category, role, variant
color-action-primary-hover        -- category, role, variant, state
spacing-component-y               -- category, role, variant
text-heading-display              -- category, role, variant
```

Not every token needs all four layers. Use what's needed; don't pad.

### 6. Avoid implementation details in names

Names should describe **what** something is, not **how** it's built.

| Good | Bad |
|------|-----|
| `Card` | `DivWithBorder` |
| `loading` | `showsSpinner` |
| `--color-surface-elevated` | `--color-with-shadow` |

### 7. Match the mental model, not the technical hierarchy

Designers reason about UI in terms of roles and patterns, not React component
trees. Name from the user/designer perspective.

| Good (user mental model) | Bad (technical implementation) |
|------|-----|
| `Modal` | `OverlayWithBackdrop` |
| `EmptyState` | `ContentlessStateRenderer` |
| `Toast` | `EphemeralNotificationContainer` |

---

## Token naming patterns

### Color tokens

Common patterns (pick one in the context doc):

**Role-based (recommended):**
```
color-action-primary
color-action-secondary
color-feedback-success
color-feedback-warning
color-feedback-error
color-feedback-info
color-text-default
color-text-muted
color-surface-default
color-surface-elevated
color-border-default
color-border-strong
```

**Element-based:**
```
button-primary-bg
button-primary-text
input-border
input-bg-focus
```

Role-based scales better as the system grows. Element-based works for tightly
scoped systems but creates token sprawl in larger ones.

### Spacing tokens

**Scale-based:**
```
spacing-xs, spacing-sm, spacing-md, spacing-lg, spacing-xl
```

**Role-based:**
```
spacing-component-x, spacing-component-y
spacing-section-y
spacing-page-margin
```

Most teams use scale-based for primitives + role-based for higher-level layout
decisions.

### Typography tokens

**Role-based (recommended):**
```
text-display-lg, text-display-md
text-heading-lg, text-heading-md, text-heading-sm
text-body-lg, text-body-md, text-body-sm
text-caption
text-code
```

Avoid numeric size names (`text-16`, `text-24`) -- they break when the scale
changes.

---

## Component naming patterns

### Component names

- PascalCase
- Descriptive of the role, not the appearance
- Singular noun (or noun phrase)

| Good | Bad |
|------|-----|
| `Button` | `Btn`, `ClickableElement` |
| `DataTable` | `Tbl`, `RowsAndColumns` |
| `EmptyState` | `NoContent`, `BlankView` |

### Variant prop values

- camelCase or kebab-case (be consistent within the project)
- Describe the role/intent of the variant

| Good | Bad |
|------|-----|
| `variant="primary"` | `variant="blueOne"` |
| `variant="destructive"` | `variant="red"` |
| `size="sm"` | `size="small14px"` |

### Boolean props

- Prefix with `is`, `has`, or `should` for boolean state
- Avoid negative names

| Good | Bad |
|------|-----|
| `isLoading` | `loading` (ambiguous), `notLoaded` |
| `isDisabled` | `disabled` (OK in HTML context), `notEnabled` |
| `hasIcon` | `icon` (ambiguous: presence or content?) |

---

## Audit checklist

When auditing naming consistency, check:

- [ ] All color tokens follow the same pattern (role-based vs element-based)
- [ ] No visual color names in semantic tokens (`blue`, `red` -- only in primitives)
- [ ] Spacing tokens follow one scale system
- [ ] Typography tokens are role-based, not size-based
- [ ] Every component name is PascalCase
- [ ] Component names in Figma exactly match code (same casing, same words)
- [ ] Prop names are consistent across components (no `loading` in one, `isLoading` in another)
- [ ] Variant values follow one casing convention across all components
- [ ] No abbreviations except universally understood ones (lg, md, sm, xl)
- [ ] No implementation details in names (no `DivWithBorder`, no `--color-with-shadow`)

**Output:** for each violation, report the file/location, the current name,
and the suggested replacement.

---

## When the project breaks these conventions

Sometimes a project has legacy naming that violates these principles. Don't
unilaterally rename -- that breaks consumers.

**Process:**
1. Document the inconsistency in the audit report.
2. Suggest the rename, mark it as a breaking change.
3. If the user approves, propose a migration path (alias old name, deprecate
   in next major version, remove later).
4. Update the context doc with the new convention.

Never rename tokens or components without checking call sites and discussing
with the user first.

---

## Notes

- **Project-specific rules belong in the context doc**, not here. This file
  is universal principles only.
- **Consistency beats correctness.** A "wrong but consistent" convention is
  easier to work with than a "right but mixed" one. Pick a side and audit.
- **The convention applies to humans too.** If the team can't follow it, AI
  won't either -- because AI is trained on what humans produced.
