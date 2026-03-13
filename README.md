# Claude Design Skills

Three custom skills that turn Claude Code into a UX strategist, visual craftsperson, and creative design director.

Built by fusing the best of multiple sources into a cohesive system that covers the full design workflow -- from user psychology to pixel-perfect implementation.

## What's Inside

### `/ux-designer` -- Strategy & Psychology
Makes Claude think about the **human first**. Asks who the user is before building, applies psychology (ELMR, CLEAR, cognitive load, decision architecture), designs flows not just screens, and pushes back on bad UX decisions.

**Includes:**
- ELMR framework (Emotion, Logic, Motivation, Reward) for psychological intent mapping
- CLEAR scorecard (Copy, Layout, Emphasis, Accessibility, Reward) for detailed audits with 1-5 scoring
- 9-step UX workflow from understanding the user to suggesting what to test
- Two audit formats: quick Score /10 and detailed CLEAR Scorecard

**Reference guides (loaded on-demand):**
- `psychology-deep-dive.md` -- cognitive load theory, decision architecture, Gestalt principles, animation timing
- `patterns-and-flows.md` -- onboarding, auth, e-commerce, dashboard, navigation, cross-industry patterns
- `psychology-situations.md` -- 50+ psychology principles organized by 9 user situations (choosing, abandoning, trusting, overloaded, etc.)

### `/ui-designer` -- Visual Craft & Components
Turns Claude into a visual perfectionist. 8pt spacing grid, mathematical type scales, 60-30-10 color rule, consistent component sizing, dark mode done right, and the Senior Designer Filter that catches amateur mistakes before they ship.

**Includes:**
- Complete visual foundation system (spacing, typography, color, elevation)
- Senior Designer Filter -- 7-point checklist run before outputting any UI
- Pushback Protocol -- flags design problems proactively
- Anti-Pattern Registry -- hard blocks for common AI-generated UI mistakes

**Reference guides (loaded on-demand):**
- `design-tokens.md` -- full CSS custom property scales for spacing, color, typography, shadows, radii
- `component-library.md` -- specs for buttons, inputs, cards, tables, modals, tooltips, toasts with sizing tables
- `polish-and-craft.md` -- CSS code for animation easing, polish techniques, responsive patterns, accessibility
- `component-taste.md` -- "good vs bad" examples for 10 common components (cards, modals, tables, forms, nav, buttons, empty states, badges, toasts, dashboards)

### `/frontend-design` -- Bold Aesthetic Direction
For when the interface needs a distinctive, memorable visual identity. Landing pages, portfolios, marketing pages. Chooses intentional aesthetic directions and executes with precision.

## How Skills Work

Skills activate **automatically** -- Claude detects when they're relevant based on your conversation. You can also invoke them manually:

```
/ux-designer          # force UX strategy mode
/ui-designer          # force visual craft mode
/frontend-design      # force bold aesthetic direction
```

Reference files inside each skill load **on-demand**, not all at once. This keeps your context clean while giving Claude access to deep knowledge when needed.

## Install

### Option 1: Copy to global skills (works in all projects)

```bash
# Clone the repo
git clone https://github.com/Gustavosilveira23/claude-design-skills.git

# Copy skills to Claude Code's global skills directory
cp -r claude-design-skills/skills/* ~/.claude/skills/
```

### Option 2: Copy to a specific project

```bash
# Copy to your project's .claude directory
cp -r claude-design-skills/skills/* your-project/.claude/skills/
```

### Verify

Start a new Claude Code conversation and check that the skills appear. You can test with:

- "Review this dashboard" -- should activate `/ux-designer`
- "The spacing looks off" -- should activate `/ui-designer`
- "Create a landing page" -- should activate `/frontend-design`

## How They Work Together

```
User request
    |
    v
/ux-designer          -- "Who is the user? What's the strategy?"
    |                     ELMR mapping, psychology, flow design
    v
/ui-designer          -- "Make it look professional and polished"
    |                     8pt grid, tokens, Senior Designer Filter
    v
/frontend-design      -- "Make it distinctive and memorable"
                          Bold aesthetic direction (when needed)
```

The skills hand off to each other. `/ux-designer` focuses on strategy and psychology, then passes to `/ui-designer` for visual craft. `/frontend-design` adds bold aesthetic direction when the interface needs to stand out (portfolios, landing pages, marketing).

## Credits & Sources

This project fuses and extends work from multiple sources:

- **[Agave](https://github.com/cory-hess/agave)** by Cory Hess (MIT License) -- Senior Designer Filter, component taste guide, anti-pattern registry, design principles
- **[Yummy Labs](https://yummy-labs.com)** -- UX/UI skill structure, reference file architecture, psychology deep dive, patterns & flows, design tokens, component library, polish & craft
- **[Growth.Design](https://growth.design)** -- CLEAR framework (Copy, Layout, Emphasis, Accessibility, Reward)
- **[Reforge](https://reforge.com)** -- ELMR framework (Emotion, Logic, Motivation, Reward)
- **[Anthropic](https://github.com/anthropics/skills)** -- Frontend Design skill, skill format specification

The value here is in the **curation and fusion** -- combining UX strategy, visual craft, psychology, and taste into a unified system that covers the full design workflow.

## License

MIT License -- see [LICENSE](LICENSE).
