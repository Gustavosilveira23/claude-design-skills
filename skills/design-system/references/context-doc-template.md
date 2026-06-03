# System Context Document

Workflow and template for the **Context** mode.

Creates or updates `.docs/design-system-context.md` -- the briefing document that
any AI (or new team member) reads before operating on the design system.

Inspired by the pattern of project-level `CLAUDE.md` files, but scoped
specifically to the design system.

---

## Why this exists

AI needs context to be useful. Without a system context document, every
interaction with the design system starts from zero -- AI has to infer
intent, conventions, and constraints from scratch every time.

This document is the **briefing you would give a new designer or engineer
joining the team**, written so an AI can read it too.

**Rule of thumb:** if a quirk, decision, or constraint isn't obvious from
reading the code or the Figma file, it belongs here.

---

## When to generate

- **First time setup:** project has a design system but no context doc.
- **After foundation mode:** immediately after the design system is established.
- **Periodic refresh:** when the system has evolved significantly (new
  principles, new constraints, new components).
- **Before handing off:** when bringing a new contributor (human or AI) into
  the system.

---

## Workflow

### Step 1: Discovery (read the project)

Before asking the user anything, extract what you can from the code:

1. Read `globals.css` -- token categories, naming patterns, dark mode coverage.
2. Read `components/ui/` and `components/` -- installed components.
3. Read `package.json` -- stack, framework version, design dependencies.
4. Read existing styleguide pages -- documented decisions.
5. Check for `CLAUDE.md` -- project-level context that may reference the DS.

### Step 2: Interview (fill the gaps)

Ask the user only what you cannot extract from code. Keep it short -- 5-7
focused questions. Examples:

- "What product is this for? Who are the users?"
- "What are the 2-3 core design principles for this system?"
- "Accessibility target -- WCAG AA, AAA, or something custom?"
- "Are there organizational quirks (legal, brand, regulatory) that constrain
  design decisions?"
- "How are contributions to the system accepted? Who reviews?"
- "Are there products or contexts where this DS is explicitly NOT used?"

### Step 3: Draft

Generate `.docs/design-system-context.md` using the template below. Fill
sections from discovery + interview. Leave clearly-marked `TODO:` placeholders
for sections the user couldn't answer yet.

### Step 4: Review

Show the draft to the user. Ask for:
- Corrections to anything inferred from code.
- Additions for quirks or constraints not yet captured.
- Confirmation that principles match how the team actually works (not how they
  wish they worked).

### Step 5: Save and register

1. Save to `.docs/design-system-context.md`.
2. Reference it in the project's `CLAUDE.md` (if it exists) under a "Design
   System" section.
3. Note in the response that future skill invocations should read this file
   first (the SKILL.md Step 1 already does this if the file exists).

---

## Template

````markdown
# Design System Context

> Briefing document for anyone (human or AI) working on this design system.
> Read this BEFORE making changes to tokens, components, or documentation.

**Last updated:** [YYYY-MM-DD]
**Maintained by:** [team or person]

---

## 1. Product & Users

**Product:** [What is this product? One-paragraph description.]

**Primary users:** [Who uses the product? What are their key contexts and constraints?]

**Brand context:** [Standalone brand? Part of a brand family? Co-branded?]

---

## 2. Design Principles

The 2-5 principles that guide every design decision in this system.
These should be **opinionated** -- generic principles like "be consistent"
don't help.

1. **[Principle name]** -- [One-line explanation of what it means in practice.]
2. **[Principle name]** -- [...]
3. **[Principle name]** -- [...]

**Examples of opinionated principles:**
- "Density over whitespace" -- this is a data-dense product; default to
  compact spacing scales.
- "Predictable over delightful" -- avoid surprise animations or microinteractions
  that could distract during critical workflows.
- "Mobile is primary" -- all components designed mobile-first; desktop is
  an enhancement.

---

## 3. Decision Guides

Heuristics for choosing between alternatives when the principles aren't
specific enough.

- **When in doubt about color:** [e.g., "default to neutral; reserve primary
  for the single most important action on screen"]
- **When in doubt about spacing:** [e.g., "use the next smaller value on the
  8pt grid -- this product errs on the dense side"]
- **When in doubt about a new component:** [e.g., "check if combining two
  existing ones solves it before proposing new"]

---

## 4. Token Overview

How tokens are organized in this system.

**Naming convention:** [e.g., "semantic role-based: `color-action-primary`,
`spacing-section-y`, `radius-card`"]

**Categories:**
- Colors: [primary, secondary, semantic feedback (success/warning/error), neutrals]
- Typography: [type scale name and size range]
- Spacing: [scale name, base unit (4px? 8px?)]
- Radius: [scale or single value]
- Shadows: [scale or single value]
- Motion: [if applicable]

**Single source of truth:** [path, e.g., `app/globals.css`]

**Sync with Figma:** [e.g., "Figma Variables are exported via the Figma MCP;
manual sync after token changes"]

---

## 5. Component Map

Components in this system, grouped by category. Mark each as:
- ✅ Stable -- production-ready, documented
- 🟡 Beta -- usable but evolving
- 🚧 In progress -- being built
- ⚠️ Deprecated -- do not use; replacement listed

| Component | Status | Notes |
|-----------|--------|-------|
| Button | ✅ | Primary, secondary, ghost, destructive variants |
| Card | ✅ | |
| Input | 🟡 | Validation states being refined |
| ... | | |

---

## 6. Accessibility Constraints

**Target:** [WCAG AA / AAA / custom]

**Non-negotiables:**
- Contrast: minimum [4.5:1 for body, 3:1 for large text]
- Touch targets: minimum [44x44px]
- Keyboard navigation: [all interactive elements reachable via Tab]
- Screen reader: [all interactive elements have accessible names]
- Focus indicators: [visible on every interactive element]

**Project-specific requirements:**
- [e.g., "Health product -- all error messages must include both color and icon"]
- [e.g., "Government client -- AAA contrast on all primary actions"]

---

## 7. Contribution Process

How new components, tokens, or changes enter the system.

**Who can contribute:** [Just DS team? Any designer? Engineering too?]

**Process:**
1. [e.g., "Propose in #design-system Slack channel with the problem and
   intended solution"]
2. [e.g., "DS team reviews and either accepts, asks for revision, or rejects
   with reasoning"]
3. [e.g., "Approved contributions get a Figma + code implementation in
   parallel, then docs"]

**Review criteria:** [What does a contribution need to demonstrate to be
   approved?]

---

## 8. Organizational Quirks & Constraints

The "why we don't do the obvious thing" section. Every team has these --
write them down so they don't get re-discovered painfully.

- [e.g., "We don't use modal dialogs for confirmations -- legal requires
  destructive actions to live on their own page after a 2023 incident."]
- [e.g., "Primary color is not used for any interactive element except CTAs --
  brand restriction."]
- [e.g., "Date pickers must support [specific format] because of integration
  with [system]."]
- [e.g., "We support IE11 in [admin product] -- avoid CSS features that don't
  polyfill cleanly."]

---

## 9. Out of Scope

What this design system explicitly does NOT cover. Listing this prevents
scope creep.

- [e.g., "Marketing site -- has its own visual language and uses a different
  system."]
- [e.g., "Email templates -- live in [tool], not in this DS."]
- [e.g., "Native mobile -- iOS and Android use platform conventions."]

---

## 10. Pointers

- **Code repo:** [path]
- **Figma library:** [URL]
- **Documentation site:** [URL if any]
- **Token source of truth:** [path]
- **Sync workflow:** [reference to internal doc if any]
````

---

## Output format (what to report to the user)

When the context doc is generated, report:

```
Design System Context Document: created

Location: .docs/design-system-context.md

Filled from project:
- [List sections filled from code/files]

Filled from interview:
- [List sections filled from user answers]

Marked TODO (needs your input later):
- [List sections left as TODO]

Next steps:
1. Review the draft and confirm or correct.
2. Fill any remaining TODOs.
3. Reference this file in CLAUDE.md so future sessions read it first.
```

---

## Notes

- **Keep it scannable.** This doc is read by humans skimming and by AI
  reading top-to-bottom. Short paragraphs, clear headings, no fluff.
- **Update it.** A stale context doc is worse than no doc -- it teaches AI
  the wrong things. Add a "Last updated" date and treat it as a maintained
  artifact, not a write-once file.
- **Resist generic content.** If a section ends up generic ("be consistent",
  "use the design system"), delete it. Only specific, opinionated content
  earns its place here.
- **Don't duplicate code.** Token values, component props, etc. live in
  the code -- this doc references them, doesn't restate them.
