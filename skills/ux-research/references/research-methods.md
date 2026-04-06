# Research Methods Catalog

Method cards organized by stage and evidence type. Use this reference when
selecting methods in Step 5 of the Plan phase.

---

## Method Selection Matrix

Quick reference: which methods work best at each stage.

| Method | Discover | Design | Develop | Deploy | Evidence Type |
|--------|----------|--------|---------|--------|---------------|
| User interviews | ++ | ++ | + | + | Qual + Attitudinal |
| Contextual inquiry | ++ | + | | | Qual + Behavioral |
| Ethnography | ++ | | | | Qual + Behavioral |
| Focus groups | + | + | | | Qual + Attitudinal |
| Card sorting | + | ++ | | | Qual + Behavioral |
| Diary studies | ++ | | | + | Qual + Behavioral |
| Mapping surveys | ++ | | | | Quant + Attitudinal |
| Intercept surveys | | | | ++ | Quant + Attitudinal |
| NPS / CSAT | | | | ++ | Quant + Attitudinal |
| Concept testing | | ++ | | | Qual + Attitudinal |
| Usability testing | | + | ++ | | Quant + Behavioral |
| A/B testing | | | + | ++ | Quant + Behavioral |
| Beta testing | | | ++ | + | Quant + Behavioral |
| Analytics review | + | | + | ++ | Quant + Behavioral |
| Heat maps / Recordings | | | ++ | + | Quant + Behavioral |
| Tree testing | | ++ | + | | Quant + Behavioral |
| First-click testing | | + | ++ | | Quant + Behavioral |
| Competitive analysis | ++ | + | | | Qual + Attitudinal |

Legend: ++ = strong fit, + = useful, blank = poor fit

---

## Key Tendencies

- **Observational methods** work best early (Discover) -- watch before you ask
- **Conversational methods** are strong in Discover and Design, but lose
  effectiveness after Design -- people can't reliably report on usability
- **Interviews work in ALL stages** because they're infinitely adaptable
- **Testing is crucial in Develop and Deploy** -- focus on behavior, not opinion
- **Surveys and interviews are complementary** -- surveys find breadth,
  interviews find depth

---

## Method Cards

### User Interviews

**What:** 1-on-1 conversations to understand experiences, needs, and behaviors.

**When to use:**
- Any stage, especially Discover and Design
- When you need depth and context behind behaviors
- When you need to understand the "why" behind data

**When NOT to use:**
- When you need statistical significance (use surveys)
- When you need to measure task completion (use usability testing)
- When people can't reliably self-report (use observation)

**Sample size:** 5-8 per user segment for thematic saturation. 3-5 is often
sufficient for small splash zone decisions.

**Time:** 1-2 weeks (recruit + conduct + synthesize)

**Output:** Interview snapshots, theme analysis, verbatim quote bank

**Tips:**
- Use Teresa Torres' "excavate the story" technique (see interview-guide.md)
- Record with permission -- notes alone miss nuance
- Interview in pairs when possible (one leads, one notes)

---

### Contextual Inquiry

**What:** Observing users in their natural environment while they work.

**When to use:**
- Discover stage -- understanding current workflows
- When self-reported behavior might differ from actual behavior
- When environment and context matter (tools, interruptions, workarounds)

**When NOT to use:**
- When you need to test a specific solution (use usability testing)
- When remote observation is impossible
- When the behavior is infrequent or hard to schedule

**Sample size:** 4-6 sessions

**Time:** 2-4 weeks (schedule + observe + synthesize)

**Output:** Workflow maps, pain point inventory, workaround documentation

---

### Mapping Surveys

**What:** Broad surveys to map landscape, segment users, or quantify problems.

**When to use:**
- Discover stage -- understanding prevalence and distribution
- When you need to quantify something interviews revealed
- When you need to segment users by behavior or attitude

**When NOT to use:**
- When you don't know what questions to ask yet (do interviews first)
- When you need behavioral data (use analytics or testing)
- When your audience is too small for meaningful sample sizes

**Sample size:** 100+ for basic segmentation, 300+ for statistical comparisons
between segments

**Time:** 1-2 weeks (design + distribute + analyze)

**Output:** Segment profiles, prevalence data, priority rankings

**Tips:**
- Keep under 10 minutes
- Open-ended questions are expensive to analyze -- use sparingly
- Always include screening questions to ensure respondent quality

---

### Usability Testing

**What:** Observing users attempt specific tasks with a product or prototype.

**When to use:**
- Develop stage -- validating that a solution works
- When you need to find usability problems before launch
- When you need to compare two approaches (preference testing)

**When NOT to use:**
- When you don't have a prototype or live product
- When you're still in Discover (you're not ready to test solutions)
- When you need to measure long-term behavior (use beta testing)

**Sample size:** 5 users find ~85% of usability problems (Nielsen). 8-12 for
quantitative comparison between variants.

**Time:** 1-2 weeks (prepare tasks + recruit + test + analyze)

**Output:** Task success rates, time on task, error counts, severity ratings,
verbatim user comments

**Variants:**
- Moderated (you guide): richer data, smaller N
- Unmoderated (tool-based): faster, larger N, less depth
- Remote vs. in-person: remote is more convenient, in-person catches body language

---

### A/B Testing

**What:** Randomly showing different versions to users and measuring outcomes.

**When to use:**
- Develop and Deploy stages
- When you have a clear metric to optimize
- When you have enough traffic for statistical significance

**When NOT to use:**
- When you don't have instrumentation in place
- When traffic is too low (need ~1,000+ per variant minimum)
- When you're testing fundamentally different concepts (too many variables)
- When the change is qualitative, not quantitative

**Sample size:** Depends on baseline conversion and minimum detectable effect.
Use a sample size calculator.

**Time:** 1-4 weeks running (depends on traffic)

**Output:** Statistical comparison of variants, confidence intervals,
segment-level analysis

---

### Competitive Analysis

**What:** Systematic review of how competitors and adjacent products solve
similar problems.

**When to use:**
- Discover and Design stages
- When entering a market or feature space with existing solutions
- When you need to understand user expectations from similar products

**When NOT to use:**
- As a substitute for user research (competitors might all be wrong)
- When the problem space is genuinely novel

**Sample size:** 3-5 direct competitors + 2-3 adjacent/cross-industry

**Time:** 1-2 weeks

**Output:** Feature matrix, pattern analysis, opportunity gaps

---

### Diary Studies

**What:** Participants record their experiences over time (days to weeks).

**When to use:**
- Discover stage -- understanding behaviors over time
- When the behavior is spread across days/weeks (not a single session)
- When context and triggers matter (what prompts the behavior?)

**When NOT to use:**
- When you need immediate answers
- When participant commitment is unreliable
- When the behavior is too infrequent to capture

**Sample size:** 10-15 participants over 1-4 weeks

**Time:** 2-6 weeks (setup + collection + analysis)

**Output:** Behavioral patterns over time, trigger maps, journey documentation

---

### Intercept Surveys

**What:** Short surveys shown to users during or after a specific interaction.

**When to use:**
- Deploy stage -- measuring satisfaction with a specific experience
- When you need in-context feedback (not recalled weeks later)
- When you need quick quantitative signal

**When NOT to use:**
- When the survey would disrupt a critical flow
- When you need depth (use interviews)
- When you need to understand behavior (use analytics)

**Sample size:** 100+ responses for reliable metrics

**Time:** 1-2 weeks collection

**Output:** Satisfaction scores, specific friction points, segmented feedback

**Tips:**
- Maximum 3-5 questions
- Trigger at the right moment (after task completion, not during)
- Always include one open-ended question for unexpected findings

---

## Viability Filter

Before recommending a method, check:

| Constraint | Methods eliminated |
|------------|-------------------|
| No prototype or product | Usability testing, A/B testing, beta testing, heat maps |
| No analytics instrumentation | A/B testing, analytics review, heat maps |
| No access to target users | Interviews, surveys, usability testing, diary studies |
| Very few users (< 100) | A/B testing, quantitative surveys |
| Budget < 1 week | Ethnography, diary studies, large surveys |
| Remote-only | Contextual inquiry (in-person), in-person usability |

After filtering, recommend the 1-2 methods with the best fit-to-effort ratio
for the splash zone. Remember Teresa Torres' principle: "One step done well
is better than many steps done poorly."
