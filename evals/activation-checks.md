# Activation checks

A skill fails in two directions, and only one of them is obvious.

**Under-activation** you notice: you ask for something and the skill does not kick in.
**Over-activation** you do not: the skill fires on a task it has no business touching, quietly
spends context, and steers the answer. Every skill in this repo carries an explicit
`Do NOT activate for` clause in its description precisely to prevent the second one.

This sheet tests both. Run it by hand in a **fresh session** -- activation is decided from the
description, so a session that already loaded the skill proves nothing.

## How to run

1. Open a new session in a project where the skills are installed.
2. Paste one prompt, verbatim, and stop before the work starts.
3. Note which skill activated, if any.
4. Compare with the expected column.

A miss is not automatically a bug. Ask which side is wrong: the prompt is genuinely ambiguous, or
the description is too greedy. Fix the description, not the test -- the description is the
contract.

## Should activate

| Prompt | Expected |
|---|---|
| "I need to decide whether to redesign the checkout" | `/ux-research` |
| "Write me an interview script for onboarding drop-off" | `/ux-research` |
| "Review this dashboard, users are getting lost" | `/ux-designer` |
| "How should this signup flow work?" | `/ux-designer` |
| "The spacing looks off on this card" | `/ui-designer` |
| "Make this landing page look less generic" | `/ui-designer` |
| "Audit the design system for token drift" | `/design-system` |
| "Add a Button component to the design system" | `/design-system` |
| "Add smooth scroll and animate the hero" | `/creative-coding` |
| "Make the background react to the mouse" | `/creative-coding` |
| "Fix the auto layout in this Figma frame" | `/figma-craft` |
| "Build this component in Figma via MCP" | `/figma-craft` |

## Should NOT activate

This half is the point of the sheet.

| Prompt | Must stay quiet | Why it is a trap |
|---|---|---|
| "Research which charting library to use" | `/ux-research` | "Research" without users is technical investigation |
| "Investigate this bug" | `/ux-research` | Debugging is not discovery |
| "Make this API easier to use" | `/ux-designer` | Developer ergonomics, no interface |
| "The dashboard is slow to load" | `/ui-designer`, `/ux-designer` | Performance problem wearing a UI costume |
| "Let's plan the design work for next quarter" | any design skill | Talking about design is not doing design |
| "Normalize this database schema" | any design skill | "Design" the verb, not the discipline |
| "Set up the CI pipeline" | any | DevOps |
| "Read this Figma file and implement it in React" | `/figma-craft` | Design-to-code, the official Figma skill owns it |
| "Add a fade-in on hover to this button" | `/creative-coding` | Micro-motion belongs to `/ui-designer` |
| "Why did our activation rate drop?" | `/ux-designer` | Retention diagnosis, hand off to growth-engagement |

## Boundary pairs

The hardest cases are the ones two skills could both claim. Run these and check that the
**handoff** is named, not that a single skill swallows the task.

| Prompt | Correct behaviour |
|---|---|
| "This screen is ugly and the flow is confusing" | Both are in scope: expect the flow question first (`/ux-designer`), then a handoff to `/ui-designer` for craft |
| "Our tokens are a mess and this button looks wrong" | `/design-system` for the tokens, `/ui-designer` for the button -- not one doing both silently |
| "We need a scroll story on the homepage" | `/creative-coding` leads; `/ui-designer` only for the static layer underneath |

## When `claude plugin eval` is available

This sheet is the manual version. The automated one runs the same prompts as cases under
`evals/**/case.yaml` with graders, and `--ablation with-without` reports the score delta with and
without the skill -- which answers the question this sheet cannot: *is the skill actually making
the output better, or just making it longer?*

Scaffold with `claude plugin eval init --bare <name>`. As of August 2026 the command exists but is
gated behind early access.
