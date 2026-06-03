# AI Slop Detector

Deterministic catalog of visual anti-patterns that mark interfaces as
AI-generated. Based on the Impeccable catalog (impeccable.style/slop), filtered
and adapted for the contexts this skill operates in.

## How to use this reference

1. **During generation** -- check your output against this list before showing
   the user. If any pattern matches, revise.
2. **During audit** -- scan the project's code for the detection signals listed
   in each rule. Report findings as part of the visual audit.
3. **During review of AI-generated code** -- the patterns marked `[CLI]` can be
   detected with grep/code search. The ones marked `[VISUAL]` need a human or
   LLM look at the rendered UI.

## Brand vs Product applicability

Some patterns are tolerable in **brand contexts** (landing pages, marketing,
portfolio) but never in **product contexts** (SaaS, dashboards, apps used
repeatedly). When a rule has different applicability, the column shows it.

| Context | Definition | Tolerance for ornament |
|---------|-----------|------------------------|
| **Brand** | Landing page, marketing site, portfolio, one-off campaign | Medium -- ornament OK if intentional |
| **Product** | App, dashboard, tool used repeatedly, internal system | Low -- restraint is the default |

---

## 1. Visual Details

### VD-01: Side-Tab Accent Border
- **Detection:** `[CLI]` grep for `border-l-` / `border-r-` with colored class on cards
- **What it is:** Thick colored border on one side of a card
- **Why slop:** The most recognizable tell of AI-generated UIs
- **Fix:** Bring color INSIDE the card (colored title, dot indicator, icon)
- **Applies to:** Brand + Product (never OK)

### VD-02: Rounded Card Border Accent
- **Detection:** `[CLI]` grep for thick borders (`border-2` or more) on `rounded-lg`+ cards
- **What it is:** Thick accent border on a rounded card -- border clashes with corners
- **Why slop:** Visual conflict between border and radius
- **Fix:** Drop the border, use shadow or subtle background tint
- **Applies to:** Brand + Product (never OK)

### VD-03: Glassmorphism Everywhere
- **Detection:** `[VISUAL]` count `backdrop-blur` + `bg-white/10` (or similar) instances
- **What it is:** Blur effects, glass cards, glow borders as decoration
- **Why slop:** Used as ornament rather than to solve real layering
- **Fix:** Use ONLY when there's real layering (sticky nav over content, modal over page)
- **Applies to:** Brand (rare OK) + Product (never OK except sticky nav)

### VD-04: Extreme Border-Radius on Cards
- **Detection:** `[VISUAL]` `rounded-3xl` or higher on small cards (<300px)
- **What it is:** Over-rounding everything (24px+ on a small card)
- **Why slop:** All elements blob together, lose distinction
- **Fix:** Cards: 8-12px. Sections: 0-8px. Pills: full.
- **Applies to:** Brand + Product

### VD-05: Hairline Border with Wide Shadow
- **Detection:** `[CLI]` `border` + `shadow-xl`/`shadow-2xl` on same element
- **What it is:** Hairline border paired with wide diffuse shadow
- **Why slop:** Recurring generated-UI signature, conflicting edge treatments
- **Fix:** Pick one -- border OR shadow, not both
- **Applies to:** Brand + Product

### VD-06: Repeating-Gradient Stripes
- **Detection:** `[CLI]` `repeating-linear-gradient` in CSS or arbitrary Tailwind
- **What it is:** Repeating-gradient stripes as surface decoration
- **Why slop:** Decorative pattern overuse, no functional purpose
- **Fix:** Solid surface or single subtle gradient
- **Applies to:** Brand (rare OK) + Product (never)

### VD-07: Amateurish Hand-Drawn SVG
- **Detection:** `[VISUAL]` inline SVG with simple paths used as illustration
- **What it is:** Hand-coded SVG illustrations of scenes/mascots
- **Why slop:** Reads as amateur doodle, not whimsy
- **Fix:** Use real illustration (commissioned, library, AI-generated raster), or remove
- **Applies to:** Brand + Product

---

## 2. Typography

### TY-01: Flat Type Hierarchy
- **Detection:** `[CLI]` check font sizes used -- if ratio between consecutive
  sizes < 1.2, hierarchy is flat
- **What it is:** Font sizes too close together
- **Why slop:** No clear visual hierarchy
- **Fix:** Use a scale ratio of at least 1.2 (see SKILL.md Step 1 Typography)
- **Applies to:** Brand + Product

### TY-02: Icon Tile Stacked Above Heading
- **Detection:** `[VISUAL]` small rounded-square icon container above a heading
  in feature cards
- **What it is:** Universal AI feature-card template
- **Why slop:** Ubiquitous generator signature
- **Fix:** Inline icon next to heading, or no icon container at all
- **Applies to:** Brand + Product

### TY-03: Italic Serif Display Headline
- **Detection:** `[CLI]` `font-serif italic` on hero/display headings
- **What it is:** Oversized italic serif as primary hero
- **Why slop:** Has become the universal AI-startup landing page hero
- **Fix:** Use sans-serif at scale, or different serif treatment
- **Applies to:** Brand (overused but tolerable) + Product (avoid)

### TY-04: Hero Eyebrow / Pill Chip Above Headline
- **Detection:** `[VISUAL]` tiny uppercase tracked label immediately above a
  display headline, or pill chip with same content
- **What it is:** Default AI SaaS hero pattern
- **Why slop:** Marker of template-driven hero
- **Fix:** Skip the eyebrow, or use a more distinctive treatment
- **Applies to:** Brand (avoid the default form) + Product (rare in product anyway)

### TY-05: Repeated Section Kicker Labels
- **Detection:** `[VISUAL]` multiple sections using same tiny uppercase tracked
  label pattern above headings
- **What it is:** Turns brand page into AI editorial scaffolding
- **Why slop:** Template structure becomes visible
- **Fix:** Vary section heading treatments, use the kicker sparingly
- **Applies to:** Brand (avoid) + Product (rare)

### TY-06: Oversized Hero Headline
- **Detection:** `[VISUAL]` full-sentence headline at display size dominates viewport
- **What it is:** Headline so big nothing else fits above the fold
- **Why slop:** Poor content prioritization
- **Fix:** Shorten the headline, reduce size, or let other content breathe
- **Applies to:** Brand + Product

### TY-07: Crushed Letter Spacing
- **Detection:** `[CLI]` `tracking-tighter` or `letter-spacing` < `-0.04em` on body
- **What it is:** Letter spacing pulled past where characters keep their shapes
- **Why slop:** Destroys legibility for visual style
- **Fix:** Body: 0 to -0.01em. Large display: -0.02 to -0.04em max.
- **Applies to:** Brand + Product

### TY-08: Overused Font
- **Detection:** `[CLI]` grep for `Inter`, `Geist`, `Space Grotesk`, `Instrument Serif`
- **What it is:** Most overused AI defaults
- **Why slop:** Lose distinctiveness through ubiquity
- **Fix:** Pair the safe font with something more distinctive, or pick alternates
  (Söhne, Suisse, Manrope, Fraunces, etc.)
- **Applies to:** Brand (avoid defaults) + Product (Inter is fine as system font)

### TY-09: Single Font for Everything
- **Detection:** `[CLI]` count font families used in project -- if only 1, flag
- **What it is:** Only one font family for the entire page
- **Why slop:** No contrast between heading and body
- **Fix:** Pair distinctive display font with refined body font
- **Applies to:** Brand (1-2 fonts recommended) + Product (1 font is OK for utility)

### TY-10: All-Caps Body Text
- **Detection:** `[CLI]` `uppercase` on `<p>` or long text blocks
- **What it is:** Long passages in uppercase
- **Why slop:** Removes word-shape recognition, hurts legibility
- **Fix:** Use uppercase only for short labels (3-4 words max)
- **Applies to:** Brand + Product

---

## 3. Color & Contrast

### CC-01: AI Color Palette (Purple/Violet + Cyan)
- **Detection:** `[CLI]` grep for `purple`, `violet`, `indigo`, `cyan` as primary brand
- **What it is:** Purple/violet gradients and cyan-on-dark
- **Why slop:** Most recognizable AI-UI palette
- **Fix:** Pick brand colors with intent. If you need purple/violet, use a
  specific shade with stated reasoning, not the default token range.
- **Applies to:** Brand + Product

### CC-02: Dark Mode with Glowing Accents
- **Detection:** `[CLI]` `box-shadow` with colored alpha on dark backgrounds
- **What it is:** Dark backgrounds + colored shadow glows
- **Why slop:** Cyberpunk aesthetic overuse, signals "AI generated"
- **Fix:** Use elevation via lighter surfaces, not glows
- **Applies to:** Brand (rare OK) + Product (never)

### CC-03: Gradient Text
- **Detection:** `[CLI]` `bg-clip-text` + `bg-gradient` pattern
- **What it is:** Gradient text as decoration
- **Why slop:** Reduces scannability, common AI tell on headings/metrics
- **Fix:** Solid text color. If absolutely needed, use ONCE on the primary hero
  only.
- **Applies to:** Brand (very limited use) + Product (never)

### CC-04: Gray Text on Colored Background
- **Detection:** `[VISUAL]` gray text on tinted/colored cards
- **What it is:** Gray text washes out on colored backgrounds
- **Why slop:** Contrast failure + amateur look
- **Fix:** Use darker shade of the background hue, or white/near-white
- **Applies to:** Brand + Product

### CC-05: Cream / Beige Palette
- **Detection:** `[CLI]` background color in cream/beige range (`#FAF7F0` style)
- **What it is:** Warm cream/beige page background
- **Why slop:** Default "tasteful" AI surface, reached by reflex
- **Fix:** If using warm neutrals, commit fully with intentional brand reason
- **Applies to:** Brand (overused) + Product (rare anyway)

---

## 4. Layout & Space

### LS-01: Identical Card Grids
- **Detection:** `[VISUAL]` same-sized cards with icon + heading + text repeated
- **What it is:** Default AI homepage layout
- **Why slop:** Template-driven repetition without variation
- **Fix:** Vary card sizes (asymmetric grid), or strip the icons, or use a
  different layout entirely (bento grid, masonry, list)
- **Applies to:** Brand + Product

### LS-02: Monotonous Spacing
- **Detection:** `[CLI]` count distinct spacing values used -- if all values are
  the same (e.g., all `gap-4`), flag
- **What it is:** Same spacing value used everywhere
- **Why slop:** No rhythm, no variation, no hierarchy
- **Fix:** Use tight groupings for related items, generous separations between
  sections (see Step 1 Spacing rules)
- **Applies to:** Brand + Product

### LS-03: Nested Cards
- **Detection:** `[CLI]` grep for `card` or `bg-` className inside another card
- **What it is:** Cards inside cards
- **Why slop:** Visual noise and excessive depth
- **Fix:** Use spacing, typography, dividers instead of nesting containers
- **Applies to:** Brand + Product

### LS-04: Hero Metric Layout
- **Detection:** `[VISUAL]` big number + small label + 3 supporting stats + gradient accent
- **What it is:** Generic "big metric" hero
- **Why slop:** Used everywhere, trusted nowhere
- **Fix:** Show one specific real metric with context, not a template
- **Applies to:** Brand (avoid template) + Product (use specific data with meaning)

### LS-05: Numbered Section Markers (01 / 02 / 03)
- **Detection:** `[VISUAL]` large `01`, `02`, `03` markers as section labels
- **What it is:** AI editorial scaffold one tier deeper than tracked eyebrow chips
- **Why slop:** Template scaffolding becomes visible
- **Fix:** Either remove numbering or integrate it differently (subtle, inline)
- **Applies to:** Brand (avoid default) + Product (rare anyway)

### LS-06: Line Length Too Long
- **Detection:** `[VISUAL]` body text wider than ~80 characters
- **What it is:** Text lines too wide
- **Why slop:** Eye loses place tracking back
- **Fix:** `max-width: 65ch` to `75ch` on body text blocks
- **Applies to:** Brand + Product

### LS-07: Content Overflowing Container
- **Detection:** `[CLI]` check for horizontal scroll, content wider than viewport
- **What it is:** Content renders wider than container
- **Why slop:** Breaks layout, forces horizontal scroll
- **Fix:** Let text wrap, constrain widths, or provide deliberate scroll
- **Applies to:** Brand + Product (bug, always fix)

### LS-08: Positioned Child Clipped by Overflow Container
- **Detection:** `[CLI]` `overflow-hidden` or `overflow-clip` wrapping absolutely
  positioned tooltips/menus/popovers
- **What it is:** Tooltips/dropdowns get clipped
- **Why slop:** Bug masquerading as design
- **Fix:** Use Portal pattern (Radix Portal), or remove the clipping
- **Applies to:** Brand + Product (bug, always fix)

---

## 5. Motion

### MO-01: Bounce or Elastic Easing
- **Detection:** `[CLI]` `cubic-bezier` with overshoot, or `ease-in-back`/`ease-out-elastic`
- **What it is:** Bounce/elastic easing on UI elements
- **Why slop:** Feels dated and tacky, especially on dialogs and cards
- **Fix:** Use `ease-out` for entering, `ease-in` for leaving, smooth throughout
- **Applies to:** Brand + Product

### MO-02: Layout Property Animation
- **Detection:** `[CLI]` `transition: width` / `transition: height` / `transition: padding`
- **What it is:** Animating width, height, padding, margin
- **Why slop:** Layout thrash, janky performance
- **Fix:** Use `transform` and `opacity`. For height, `grid-template-rows: 0fr -> 1fr`
- **Applies to:** Brand + Product (performance, always fix)

### MO-03: Image Hover Transform
- **Detection:** `[CLI]` `hover:scale-` or `hover:rotate-` on `<img>` tags
- **What it is:** Scaling/rotating images on hover
- **Why slop:** Recurring generated-UI signature
- **Fix:** Use overlay or subtle filter change instead
- **Applies to:** Brand (rare OK) + Product (avoid)

---

## 6. Copy

### CO-01: Em-Dash Overuse
- **Detection:** `[CLI]` count `—` in body copy -- more than 2 per page is suspect
- **What it is:** Multiple em-dashes in body copy
- **Why slop:** AI cadence tell
- **Fix:** Use commas, colons, periods, parentheses instead
- **Applies to:** Brand + Product

### CO-02: Marketing Buzzword
- **Detection:** `[CLI]` grep for `streamline`, `empower`, `supercharge`,
  `world-class`, `enterprise-grade`, `seamless`, `revolutionary`
- **What it is:** Generic SaaS phrases
- **Why slop:** Instant AI tells
- **Fix:** Specific verbs and nouns describing actual functionality
- **Applies to:** Brand (avoid) + Product (rare in product copy)

### CO-03: Aphoristic-Cadence Copy
- **Detection:** `[VISUAL]` sections ending with "Not X. Y." or "Less X, more Y."
- **What it is:** Manufactured-contrast aphorisms
- **Why slop:** AI cadence, not voice
- **Fix:** State the thing plainly without rhetorical flourish
- **Applies to:** Brand (avoid) + Product (rare)

### CO-04: Theater Framing Copy
- **Detection:** `[CLI]` grep for "theater" used dismissively in copy
- **What it is:** "X is theater" dismissive framing
- **Why slop:** Recurring generated-copy tic
- **Fix:** State what the thing does or doesn't do
- **Applies to:** Brand + Product

---

## 7. Imagery

### IM-01: Broken or Placeholder Image
- **Detection:** `[CLI]` `<img>` with empty/missing `src`, or `src="placeholder.jpg"`
- **What it is:** Broken image boxes
- **Why slop:** Ships broken
- **Fix:** Use real images, generated assets, or remove the tag
- **Applies to:** Brand + Product (bug, always fix)

---

## 8. General Quality

### GQ-01: Cramped Padding
- **Detection:** `[VISUAL]` text touching the edge of bordered/colored containers
- **What it is:** Text too close to container edge
- **Why slop:** Cramped, unprofessional
- **Fix:** At least 8px, ideally 12-16px inside bordered or colored containers
- **Applies to:** Brand + Product

### GQ-02: Body Text Touching Viewport Edge
- **Detection:** `[CLI]` body content without container padding or max-width
- **What it is:** Body flush against viewport edge
- **Why slop:** No breathing room
- **Fix:** Wrap content in container with at least 16px horizontal padding,
  or apply max-width with `mx-auto`
- **Applies to:** Brand + Product

### GQ-03: Justified Text
- **Detection:** `[CLI]` `text-align: justify` or `text-justify`
- **What it is:** Justified text without hyphenation
- **Why slop:** Creates "rivers of white" -- uneven word spacing
- **Fix:** `text-align: left` for body text, or enable `hyphens: auto`
- **Applies to:** Brand + Product

### GQ-04: Low Contrast Text
- **Detection:** `[CLI]` calculate contrast ratio of text color vs background
- **What it is:** Text below WCAG AA (4.5:1 body, 3:1 large)
- **Why slop:** Accessibility failure
- **Fix:** Increase contrast between text and background
- **Applies to:** Brand + Product (always fix)

### GQ-05: Skipped Heading Level
- **Detection:** `[CLI]` check heading sequence -- `h1 -> h3` without `h2`, etc.
- **What it is:** Heading levels skip
- **Why slop:** Breaks document outline for screen readers
- **Fix:** Maintain sequential heading levels (or use `aria-level` if visual
  requires it)
- **Applies to:** Brand + Product (accessibility, always fix)

### GQ-06: Tight Line Height
- **Detection:** `[CLI]` `leading-` < 1.3 on body text
- **What it is:** Line height below 1.3x font size
- **Why slop:** Multi-line text hard to read
- **Fix:** 1.5 to 1.7 for body text, 1.1-1.3 for headings only
- **Applies to:** Brand + Product

### GQ-07: Tiny Body Text
- **Detection:** `[CLI]` `text-xs` (12px) on body content
- **What it is:** Body below 12px
- **Why slop:** Hard to read, especially on high-DPI
- **Fix:** 14px minimum for body, 16px ideal
- **Applies to:** Brand + Product

### GQ-08: Wide Letter Spacing on Body Text
- **Detection:** `[CLI]` `tracking-` > 0.05em on body text (`<p>`, long content)
- **What it is:** Letter spacing above 0.05em on body
- **Why slop:** Disrupts character groupings, slows reading
- **Fix:** Wide tracking only for short uppercase labels (badges, eyebrows)
- **Applies to:** Brand + Product

---

## Audit output format

When running this detector as part of an audit, format the output as:

```
AI Slop Detection: [project name]

Score: [X/46] patterns clean -- [one-sentence verdict]

Critical (always fix):
- [Pattern ID] [Pattern name] -- [file:line]
  Why: [one-line explanation]
  Fix: [actionable suggestion]

Brand-only context tolerable (flag for awareness):
- [Pattern ID] [Pattern name] -- [file:line]
  Note: [if this is a brand page, OK; if product, should fix]

Clean categories: [list categories where no patterns found]
```

---

## Quick-reference grep patterns

For fast scanning of a project, run these and review results:

```bash
# CC-03 Gradient text
grep -rn "bg-clip-text\|background-clip: text" --include="*.tsx" --include="*.css"

# VD-01 Side accent border
grep -rn "border-l-[0-9]\|border-r-[0-9]" --include="*.tsx" | grep -v "border-l-0\|border-r-0"

# VD-03 Glassmorphism (count)
grep -rn "backdrop-blur" --include="*.tsx" | wc -l

# CC-01 AI palette
grep -rEn "purple-[0-9]+|violet-[0-9]+|indigo-[0-9]+|cyan-[0-9]+" --include="*.tsx" --include="*.css"

# TY-08 Overused fonts
grep -rn "Inter\|Geist\|Space Grotesk\|Instrument Serif" --include="*.tsx" --include="*.css"

# MO-02 Layout property animation
grep -rEn "transition.*(width|height|padding|margin)" --include="*.css" --include="*.tsx"

# CO-02 Marketing buzzwords
grep -rEni "streamline|empower|supercharge|world-class|enterprise-grade|seamless|revolutionary" --include="*.tsx" --include="*.md"

# CO-01 Em-dash count
grep -rcn "—" --include="*.tsx" --include="*.md"

# IM-01 Broken images
grep -rEn 'src=("|\x27)(\x27|"|placeholder)' --include="*.tsx"

# GQ-07 Tiny body text
grep -rn "text-xs" --include="*.tsx" | grep -v "label\|badge\|caption"

# GQ-03 Justified text
grep -rn "text-justify\|text-align: justify" --include="*.tsx" --include="*.css"
```

---

## Source and credit

Patterns adapted from the Impeccable catalog (https://impeccable.style/slop).
Adaptation for this skill includes:
- Reorganization by ID for cross-referencing
- Brand vs Product applicability column
- Concrete `grep` patterns for Tailwind/Next.js projects
- Removal of patterns that don't apply to product/web-app context
- Integration with the skill's existing 8pt grid, 60-30-10, and type scale rules
