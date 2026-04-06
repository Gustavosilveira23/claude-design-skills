# Claude Design Skills

Four custom skills that turn Claude Code into a UX researcher, UX strategist, visual craftsperson, and design system engineer.

Built by fusing the best of multiple sources into a cohesive system that covers the full design workflow -- from user research to pixel-perfect implementation to design system infrastructure.

## What's Inside

### `/ux-research` -- Evidence & Discovery
Makes Claude think about the EVIDENCE first. Plans research efforts, generates interview scripts, synthesizes findings into atomic knowledge, and produces design specs ready for implementation.

**Combines three frameworks:**
- **Research Planning** (Behzod Sirjani) -- decision-first research: splash zone, evidence mapping, method selection
- **Atomic Research** (Daniel Pidcock) -- knowledge as atoms: Experiment -> Fact -> Insight -> Recommendation
- **Continuous Discovery** (Teresa Torres) -- "excavate the story" interview technique, Opportunity Solution Tree

**4 independent modes:**

| Mode | What it does |
|------|-------------|
| **Plan** | Structures a research effort from decision to method selection |
| **Interview** | Generates research instruments (scripts, surveys, test plans) |
| **Synthesize** | Organizes findings into atomic knowledge with confidence scoring |
| **Specify** | Transforms insights into actionable design specs (Ready to Dev) |

**Reference guides (loaded on-demand):**
- `research-methods.md` -- method cards by stage (Discover/Design/Develop/Deploy), selection matrix, viability filter
- `interview-guide.md` -- "excavate the story" technique, script templates, survey builder, usability test plans
- `atomic-research.md` -- 4-level atom framework, confidence scoring, synthesis workflow, repository maintenance
- `specs-templates.md` -- Research Brief, Insight Report, Design Brief, Million Dollar Slide examples

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
- `copy-and-content.md` -- terminology governance, persuasion frameworks, copy by component, voice & tone

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

### `/design-system` -- Infrastructure & Consistency
Manages the foundation that makes everything else work: design tokens, component libraries, documentation, audits, and Figma sync. Built for **shadcn/ui + Tailwind CSS + Next.js** projects.

**6 modes:**

| Mode | What it does |
|------|-------------|
| **Audit** | Scans for token drift, hardcoded colors, WCAG violations, spacing off the 8pt grid, dark mode gaps, undocumented components |
| **Foundation** | Creates a design system from a screenshot (new project) OR extracts and organizes tokens from an existing codebase |
| **Component** | Checks for duplicates, searches shadcn registry, installs, customizes, creates showcase page, updates navigation |
| **Page** | Analyzes a design (screenshot/Figma), maps to existing DS components, builds the page, verifies compliance post-build |
| **Document** | Auto-generates design system documentation (token inventory, component catalog, usage guidelines) |
| **Sync Figma** | Pulls tokens from Figma, compares parity between Figma and code, generates code from Figma components |

**Reference guides (loaded on-demand):**
- `foundation-workflow.md` -- complete workflow for creating or extracting a design system foundation
- `component-workflow.md` -- adding components with duplicate detection and showcase generation
- `page-workflow.md` -- building pages that import from the design system
- `audit-checklist.md` -- token drift scanning, WCAG compliance, component consistency checks
- `shadcn-tailwind-patterns.md` -- patterns for shadcn/ui + Tailwind CSS 3/4, CVA, dark mode, token naming

## How Skills Work

Skills activate **automatically** -- Claude detects when they're relevant based on your conversation. You can also invoke them manually:

```
/ux-research                      # force research mode
/ux-research plan                 # plan a research effort
/ux-research synthesize           # synthesize findings into atoms
/ux-designer                      # force UX strategy mode
/ui-designer                      # force visual craft mode
/design-system                    # force design system mode
/design-system audit              # run a design system audit
/design-system foundation         # create or extract a design system
/design-system component button   # add a component to the DS
```

Reference files inside each skill load **on-demand**, not all at once. This keeps your context clean while giving Claude access to deep knowledge when needed.

## Complementary: `/frontend-design`

For bold aesthetic direction (landing pages, portfolios, marketing pages), use the official **[Frontend Design skill](https://github.com/anthropics/claude-code/tree/main/plugins/frontend-design)** from Anthropic. It complements these skills by adding creative, distinctive visual identity when an interface needs to stand out.

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

- "I need to decide whether to redesign the checkout" -- should activate `/ux-research`
- "Review this dashboard" -- should activate `/ux-designer`
- "The spacing looks off" -- should activate `/ui-designer`
- "Audit the design system" -- should activate `/design-system`

## How They Work Together

```
User request
    |
    v
/ux-research          -- "What should we build? Do we have evidence?"
    |                     Decision, discovery, synthesis, specs
    v
/ux-designer          -- "How should this experience work?"
    |                     ELMR mapping, psychology, flow design
    v
/design-system        -- "Is the infrastructure ready?"
    |                     Tokens, components, consistency, docs
    v
/ui-designer          -- "Make it look professional and polished"
                          8pt grid, tokens, Senior Designer Filter
```

The skills hand off to each other:
- `/ux-research` turns questions into evidence -- plans research, synthesizes findings, and produces specs
- `/ux-designer` focuses on strategy and psychology -- who is the user, what's the flow, how does it feel
- `/design-system` ensures the infrastructure is solid -- tokens defined, components available, everything consistent
- `/ui-designer` handles visual craft -- spacing, color, typography, polish

**You don't need to run the full pipeline every time.** Each skill works independently. Use what you need:
- Quick visual fix? Go straight to `/ui-designer`
- Adding a component? Go straight to `/design-system component`
- Need to validate an assumption? Use `/ux-research plan`

## Credits & Sources

This project fuses and extends work from multiple sources:

- **[Agave](https://github.com/cory-hess/agave)** by Cory Hess (MIT License) -- Senior Designer Filter, component taste guide, anti-pattern registry, design principles
- **[Yummy Labs](https://yummy-labs.com)** -- UX/UI skill structure, reference file architecture, psychology deep dive, patterns & flows, design tokens, component library, polish & craft
- **[Growth.Design](https://growth.design)** -- CLEAR framework (Copy, Layout, Emphasis, Accessibility, Reward)
- **[Reforge](https://reforge.com)** -- ELMR framework (Emotion, Logic, Motivation, Reward), Research Planning framework (Behzod Sirjani)
- **[Daniel Pidcock](https://blog.prototypr.io/what-is-atomic-research-e5d9fbc1285c)** -- Atomic Research framework (Experiments, Facts, Insights, Recommendations)
- **[Teresa Torres / Product Talk](https://www.producttalk.org)** -- Continuous Discovery Habits, "excavate the story" interview technique, Opportunity Solution Tree
- **[Anthropic](https://github.com/anthropics/skills)** -- skill format specification
- **[Design System Agent](https://github.com/jarvismoore1016/design-system-agent)** by Jarvis Moore -- inspiration for audit workflows, Figma sync modes, and component generation patterns
- **[Awesome Design Systems](https://github.com/jcusick93/awesome-design-systems)** -- reference catalog for design system benchmarking

The value here is in the **curation and fusion** -- combining UX research, strategy, visual craft, psychology, design system infrastructure, and taste into a unified system that covers the full design workflow.

## License

MIT License -- see [LICENSE](LICENSE).
