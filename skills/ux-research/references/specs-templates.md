# Specs & Output Templates

Templates for research outputs: Research Brief (before research), Insight
Report (after research), and Design Brief (ready for design). Use this
reference in Step 6 (Define Outputs) and Step 10 (Generate Specs).

---

## 1. Research Brief

Use BEFORE starting research to get alignment and approval on the plan.
This is the output of the Plan phase.

```markdown
# Research Brief: [Topic]

## Decision
[The specific decision this research will inform]

## Stage
[Discover / Design / Develop / Deploy] -- [brief justification]

## Splash Zone
[Small / Medium / Large]
- Work size: [assessment]
- Stakeholder involvement: [who needs to know]
- User impact: [who is affected]

## What We Need to Learn
[Evidence needs from Step 4, organized by priority]

1. **Must know:** [critical evidence without which the decision can't be made]
2. **Should know:** [important context that strengthens the decision]
3. **Nice to know:** [additional information if time/budget allows]

## Method
[Selected method(s) with justification]

- **Method:** [name]
- **Why this method:** [how it maps to evidence needs]
- **Participants:** [who, how many, how recruited]
- **Timeline:** [dates]

## Expected Output
- **Artifact:** [report type, presentation, etc.]
- **Million Dollar Slide:** [description of the ONE visual that drives the decision]

## Risks & Limitations
- [What this research WON'T answer]
- [Known biases or constraints]
- [What to do if the research is inconclusive]
```

---

## 2. Insight Report

Use AFTER research to present findings using the Atomic Research structure.
This is the output of the Synthesize phase.

```markdown
# Insight Report: [Topic]

## Research Summary
- **Decision:** [what this research informed]
- **Method:** [what we did]
- **Participants:** [who, how many]
- **Date:** [when]

## Key Findings

### Insight 1: [declarative statement]
**Confidence:** [HIGH / MEDIUM / LOW]

Supporting facts:
- FACT: [observation] -- Source: [experiment]
- FACT: [observation] -- Source: [experiment]
- FACT: [observation] -- Source: [experiment]

> "[Verbatim quote that best captures this insight]"
> -- Participant [ID]

**Implication:** [what this means for the decision]

---

### Insight 2: [declarative statement]
**Confidence:** [HIGH / MEDIUM / LOW]

Supporting facts:
- FACT: [observation] -- Source: [experiment]
- FACT: [observation] -- Source: [experiment]

**Implication:** [what this means for the decision]

---

[Repeat for each insight]

## Recommendations

### 1. [Action] -- backed by Insights [X, Y]
**Expected outcome:** [what should change]
**How to measure:** [metric]

### 2. [Action] -- backed by Insight [Z]
**Expected outcome:** [what should change]
**How to measure:** [metric]
**Note:** LOW confidence -- based on limited evidence. Consider further validation.

## What We Didn't Learn
- [Gaps in the research]
- [Questions that emerged but weren't answered]
- [Suggested follow-up research]

## Raw Data
[Link to interview recordings, survey data, analytics exports]

**Human review note:** These insights were structured with AI assistance.
Review raw data to verify key nuances and edge cases were captured.
```

---

## 3. Design Brief

Use to hand off research findings to the `/ux-designer` skill. This is the
"Ready to Dev" artifact -- the output of the Specify phase.

```markdown
# Design Brief: [Feature / Screen Name]

## Decision
[The original decision this research informed]

## Problem
[One paragraph describing the user problem, grounded in research evidence.
Not a feature description -- the PROBLEM users face.]

## Target User
- **Who:** [based on research, not assumptions]
- **Emotional state:** [how they feel when encountering this problem]
- **Context:** [where, when, on what device, under what circumstances]
- **Current behavior:** [how they solve this today, including workarounds]

## Requirements

### Must have (HIGH confidence)
1. [Requirement]
   - Backed by: Insight [X] (facts: [A, B, C])
   - Rationale: [why this matters to the user]

2. [Requirement]
   - Backed by: Insight [Y] (facts: [D, E])
   - Rationale: [why this matters to the user]

### Should have (MEDIUM confidence)
3. [Requirement]
   - Backed by: Insight [Z] (facts: [F, G])
   - Rationale: [why this matters to the user]

### Assumptions (LOW confidence -- needs validation)
4. [Requirement/hypothesis]
   - Based on: [limited evidence]
   - Risk if wrong: [what happens if this assumption is incorrect]
   - How to validate: [cheapest way to test this]

## Constraints
- [Technical constraints that affect design]
- [Business constraints (timeline, budget, legal)]
- [User constraints (accessibility needs, device limitations)]

## Success Metrics
- **Primary:** [the metric that tells us the decision was right]
- **Secondary:** [supporting metrics]
- **Guardrail:** [metrics that should NOT get worse]

[Metrics should connect directly back to the original decision]

## Open Questions
- [Anything research didn't resolve -- be honest]
- [Trade-offs that need design judgment, not more research]

## Reference
- [Link to full Insight Report]
- [Link to raw research data]
- [Link to competitive analysis if applicable]
```

---

## 4. Million Dollar Slide

The ONE visual that most powerfully communicates the key finding. Design this
BEFORE starting research to ensure you collect the right data.

### Common formats:

**Comparison chart** (when the finding is a difference):
```
Before vs. After
Control vs. Treatment
Current vs. Desired
Competitor A vs. Competitor B vs. Your product
```

**Quote + number** (when the finding is a human truth backed by data):
```
"I wanted to see if it's worth my time before I started."
-- 4 out of 5 first-time users tried to find analytics
   before creating their first post
```

**Journey map highlight** (when the finding is a specific moment of friction):
```
[Step 1] -> [Step 2] -> [FRICTION POINT] -> [Drop-off: 67%]
                              |
                        "This is where we lose them"
```

**2x2 matrix** (when the finding is about positioning or segmentation):
```
              High effort
                 |
  Segment A      |      Segment B
  (small, vocal) |   (large, silent)
  ---------------+------------------
  Segment C      |      Segment D
  (churned)      |   (power users)
                 |
              Low effort
```

**Funnel with drop-off** (when the finding is about conversion):
```
Landing:    100%  ████████████████████
Signup:      45%  █████████
Onboarding:  28%  ██████
First use:   12%  ███        <-- 57% drop between signup and first use
Retention:    8%  ██
```

### Tips:
- One number, one quote, one visual. Not all three.
- The slide should provoke a reaction: "We need to fix this" or "This
  confirms we're on the right track"
- If stakeholders remember one thing from your research, it should be this slide
- Test it: show the slide to someone not involved in the research. If they
  can't immediately understand the implication, simplify.
