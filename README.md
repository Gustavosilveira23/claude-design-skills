# Claude Design Skills

Six custom skills that turn Claude Code into a UX researcher, UX strategist, visual craftsperson, design system engineer, motion / creative-coding specialist, and Figma layout craftsperson -- plus the tooling to write your product's design rules down and verify them in a real browser.

Built by fusing the best of multiple sources into a cohesive system that covers the full design workflow -- from user research to pixel-perfect implementation to design system infrastructure.

| | |
|---|---|
| [`skills/`](skills/) | the six design skills -- the **method** |
| [`templates/`](templates/) | `DESIGN.md` template -- your product's **rules**, written as constraints |
| [`commands/`](commands/) | `/design-md` writes those rules, `/design-review` checks them |
| [`agents/`](agents/) | the `design-review` subagent that drives the browser |
| [`evals/`](evals/) | activation checks -- tests **over**-activation, not just under |

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

### `/creative-coding` -- Motion & Creative Coding
The layer beyond static UI: scroll-driven animation, WebGL/canvas, generative and interactive effects, and the craft of movement itself. Built for a designer who guides with intent and taste while Claude implements -- climbing from CSS to Canvas to WebGL only when the scene earns it.

**Includes:**
- The three tiers of effort (DOM/CSS/Framer -> Canvas 2D -> WebGL/shaders) with a "climb only when it pays" rule
- The vibe-coding loop: build isolated on a `/lab` route, iterate in the browser, integrate only when approved
- Prompt anatomy for visual effects (intent, reference, parameters, constraints, placement) + a tuning vocabulary
- Guardrails baked in: ssr:false, pause offscreen, prefers-reduced-motion, capped dpr, and hover-is-not-touch

**Reference guides (loaded on-demand):**
- `toolkit.md` -- the stack by objective (GSAP, Lenis, react-three-fiber, drei, postprocessing), the tiers in detail, the Processing->web map, and designer shortcuts (Rive, Spline, Lottie)
- `shaders.md` -- directing GPU/shader effects without writing GLSL: the per-pixel mental model, the concept toolkit (shaping functions, the noise/fBm/cellular family, image displacement, SDF/ray marching), a shader tuning vocabulary, and a Book of Shaders chapter map
- `recipes.md` -- five ready-to-adapt recipes (smooth scroll, scroll reveals, evolving a point field, liquid image hover, floating 3D object) with starter prompts and an order to tackle them
- `motion-craft.md` -- the 12 animation principles, easing as craft, choreography, and the reusable fundamentals (lerp/damping, noise, the minimal math, the 16ms budget, motion ethics)

### `/figma-craft` -- Layout Craft Inside Figma

Covers the layer the official Figma skills leave out: **writing** to a Figma file through the MCP
without the auto layout falling apart. Activates on any create/edit/fix task inside a Figma file --
screen, frame, card, component, variant, topbar, sidebar, table, FigJam.

**What it adds:**
- Decide the frame tree **before** generating code, not after the layout breaks
- Pick HUG / FILL / FIXED by the element's role, because the Figma default is usually the wrong one
- **Validate by property, never by screenshot** -- `node.screenshot()` renders the node in
  isolation and hides broken layout
- A list of gotchas verified on real client work, not theory

**Reference guide (loaded on-demand):**
- `audit-layout.md` -- runnable audit script that walks the tree and reports sizing, spacing and
  overflow problems by property

Pairs with the official Figma MCP skills (`figma-use` is a prerequisite). Does **not** cover
design-to-code -- for reading a Figma file and implementing it in React, use Figma's own skill.

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
/creative-coding                  # force motion / creative-coding mode
/creative-coding <ref-url>        # start from a reference site
```

Reference files inside each skill load **on-demand**, not all at once. This keeps your context clean while giving Claude access to deep knowledge when needed.

## Beyond skills: writing the rules down, and checking them

Skills carry *method*. They do not carry *your product's rules* -- and an agent with excellent
method still invents a teal accent on a monochrome site if nothing forbids it.

Two commands and a subagent close that gap. They live outside the skills because they apply to any
project with an interface, whatever the stack.

### `DESIGN.md` -- the rules, written as constraints

Every project with a UI gets two files **where the work happens**, not in a wiki:

| File | Job |
|---|---|
| `CLAUDE.md` | how to work: current state, where the truth lives, what not to touch |
| `DESIGN.md` | what the product looks like and **what is forbidden** |

The rule that makes `DESIGN.md` work is that it is written **by constraint, not by description**.

```
Bad:   primary: #1B4DFF
Good:  primary: #1B4DFF -- CTAs and active states only. Never a background,
       never decorative. One per screen. If you want two, the layout is wrong.
```

Description gets ignored. Constraint gets obeyed.

**Never let the model write this file alone** from your Figma or your CSS. It produces perfect
tokens and invented principles -- a document that reads plausible and is wrong, which is the
hardest kind to catch. Extract the values with the agent; write the *why* yourself.

Start from [`templates/DESIGN.template.md`](templates/DESIGN.template.md), or run `/design-md`,
which reads the code for the values and interviews you for the reasoning.

### `/design-review` -- verify in a real browser

Runs the [`design-review`](agents/design-review.md) subagent: loads the project's `DESIGN.md`,
scopes to the git diff, opens the screen in a real browser, and checks three viewports and both
themes.

The rule it enforces on itself: **a screenshot is not the first proof.** Measure the computed
property, then let the image confirm it.

Its five universal checks target what makes agent-built UI read as generic:

1. **Declared font is actually loaded** -- the theme names a family and ships no file
2. **The code's promise matches the pixel** -- "subtly raised" that is invisible at arm's length
3. **Each color has one job** -- two accents under ~20 degrees of hue are one accent twice
4. **States are derived, not invented** -- hover values written by hand mean there is no ramp
5. **Density varies** -- one deliberately oversized element per screen, or a uniform stack

Every finding carries a measured value. "The contrast looks low" is not a finding; "#7b7970 on
#f5ede5 is 3.1:1, below 4.5:1" is.

**Requires** the [Playwright MCP](https://github.com/microsoft/playwright-mcp) to interact and the
[Chrome DevTools MCP](https://github.com/ChromeDevTools/chrome-devtools-mcp) to audit. With only
one of them it still runs, and says what it could not cover.

## Complementary: `/frontend-design`

For bold aesthetic direction (landing pages, portfolios, marketing pages), use the official **[Frontend Design skill](https://github.com/anthropics/claude-code/tree/main/plugins/frontend-design)** from Anthropic. It complements these skills by adding creative, distinctive visual identity when an interface needs to stand out.

## Install

### Option 1: skills CLI (recommended)

Installs versioned, and `skills update` pulls later changes -- no manual copy to drift out of sync.
Works with Claude Code, Cursor, Codex and ~70 other agents.

```bash
# All six skills, global (user-level)
npx skills add Gustavosilveira23/claude-design-skills --all -g

# Or pick the ones you want
npx skills add Gustavosilveira23/claude-design-skills -s ui-designer -s ux-designer -g

# See what's available first
npx skills add Gustavosilveira23/claude-design-skills --list
```

Later: `npx skills update -g` to pull changes, `npx skills list -g` to see what is installed.

The CLI installs **skills only**. For `/design-md`, `/design-review` and the subagent, copy those
three files -- they are plain markdown with no dependencies:

```bash
git clone https://github.com/Gustavosilveira23/claude-design-skills.git

mkdir -p ~/.claude/commands ~/.claude/agents
cp claude-design-skills/commands/*.md ~/.claude/commands/
cp claude-design-skills/agents/design-review.md ~/.claude/agents/
```

Then add the two MCP servers `/design-review` drives:

```bash
claude mcp add playwright --scope user -- npx @playwright/mcp@latest
claude mcp add chrome-devtools --scope user -- npx chrome-devtools-mcp@latest
```

Restart Claude Code -- commands and MCP servers load at startup.

### Option 2: Copy manually

```bash
git clone https://github.com/Gustavosilveira23/claude-design-skills.git

# Global (all projects)
cp -r claude-design-skills/skills/* ~/.claude/skills/

# Or a single project
cp -r claude-design-skills/skills/* your-project/.claude/skills/
```

If you copy manually, the copies drift the moment you edit one side. Diff them with
`diff -r --strip-trailing-cr` -- plain `diff` reports every line as changed when the line endings
differ, which hides the real change.

### Verify

Start a new Claude Code conversation and check that the skills appear. You can test with:

- "I need to decide whether to redesign the checkout" -- should activate `/ux-research`
- "Review this dashboard" -- should activate `/ux-designer`
- "The spacing looks off" -- should activate `/ui-designer`
- "Audit the design system" -- should activate `/design-system`
- "Add a smooth scroll and animate the hero" -- should activate `/creative-coding`
- "Fix the auto layout in this Figma frame" -- should activate `/figma-craft`

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
    |                     8pt grid, tokens, Senior Designer Filter
    v
/creative-coding      -- "Make it move and feel alive"
                          Scroll animation, WebGL/canvas, motion craft
```

The skills hand off to each other:
- `/ux-research` turns questions into evidence -- plans research, synthesizes findings, and produces specs
- `/ux-designer` focuses on strategy and psychology -- who is the user, what's the flow, how does it feel
- `/design-system` ensures the infrastructure is solid -- tokens defined, components available, everything consistent
- `/ui-designer` handles visual craft -- spacing, color, typography, polish
- `/creative-coding` handles motion & interactive graphics -- scroll animation, WebGL/canvas, generative effects (micro-motion stays with `/ui-designer`)

**You don't need to run the full pipeline every time.** Each skill works independently. Use what you need:
- Quick visual fix? Go straight to `/ui-designer`
- Adding a component? Go straight to `/design-system component`
- Need to validate an assumption? Use `/ux-research plan`
- Want a scroll animation or a WebGL hero? Go straight to `/creative-coding`

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
- **[The Book of Shaders](https://github.com/patriciogonzalezvivo/thebookofshaders)** by Patricio Gonzalez Vivo & Jen Lowe ([thebookofshaders.com](https://thebookofshaders.com)) -- shader concept vocabulary and chapter map behind the `/creative-coding` shaders reference (fragment-shader mental model, shaping functions, the noise/fBm/cellular family, image effects, SDF/ray marching)

The value here is in the **curation and fusion** -- combining UX research, strategy, visual craft, psychology, design system infrastructure, and taste into a unified system that covers the full design workflow.

## License

MIT License -- see [LICENSE](LICENSE).
