# Atomic Research Framework

Complete reference for organizing research knowledge using Daniel Pidcock's
Atomic Research framework. Use this reference in the Synthesize phase (Step 9).

---

## Why Atomic Research?

Traditional research lives in reports. Reports capture a moment in time, then
become outdated. Nobody reads them six months later. When a new team member
asks "what do we know about X?", the answer is buried in a PDF from 2023.

Atomic Research solves this by breaking knowledge into small, connected,
reusable pieces -- atoms. Like atoms in chemistry, they can be recombined
into new structures as understanding evolves.

**Key insight:** "Because what we discovered is linked to, but not reliant on,
how we discovered it." Facts survive even when the experiment that generated
them becomes irrelevant.

---

## The Four Atom Levels

### Level 1: Experiments

**What:** The research activity itself -- where the knowledge came from.

**Format:** "We did [method] with [participants] on [date] about [topic]."

**Examples:**
- "5 user interviews with first-time creators, Jan 2026"
- "Analytics review of checkout funnel, Q4 2025"
- "Usability test of new onboarding flow with 8 participants, Mar 2026"
- "Competitive analysis of 5 analytics tools, Feb 2026"
- "Something the CEO heard at a conference" (yes, even this counts)

**Rules:**
- Every atom chain starts with an experiment
- An experiment can generate many facts
- Record enough detail to assess credibility later

---

### Level 2: Facts

**What:** Raw findings with no interpretation. What the data says or what the
person said -- not what you think it means.

**Format:** "[Specific observation] as reported/observed in [Experiment]."

**Examples:**
- "4 out of 5 users tried to find analytics before creating their first post"
- "Average checkout completion time is 4.2 minutes (up from 3.1 last quarter)"
- "User P3 said: 'I wanted to see if it's worth my time before I started creating'"
- "3 out of 5 competitors show sample data during onboarding"

**Rules:**
- Facts are OBJECTIVE -- no interpretation, no "because", no "which means"
- Preserve verbatim quotes when from interviews
- Include specific numbers when from quantitative sources
- One fact = one discrete observation (don't bundle multiple findings)
- A fact can support multiple insights (it means different things in different contexts)

**Test:** Could two reasonable people agree this is what the data shows?
If yes, it's a fact. If they might interpret it differently, you've already
moved to insight territory.

---

### Level 3: Insights

**What:** Patterns and interpretations that emerge from connecting multiple facts.

**Format:** "[Interpretation/pattern] based on [Fact A], [Fact B], [Fact C]."

**Examples:**
- "Users need evidence of potential value before committing to content creation"
  (based on: 4/5 tried analytics first + "worth my time" quote + competitors show sample data)
- "The checkout flow has degraded since the redesign"
  (based on: completion time increase + error rate increase + 3 support tickets about confusion)

**Rules:**
- An insight MUST be supported by at least 1 fact (preferably 2+)
- An insight can be supported by facts from DIFFERENT experiments (this is
  where atomic research gets powerful)
- Multiple insights can come from the same set of facts
- Insights should be specific enough to act on, general enough to apply broadly
- Label the confidence level (see scoring below)

**Test:** Can you point to specific facts that support this? If not, it's an
assumption, not an insight.

---

### Level 4: Recommendations

**What:** Actionable next steps based on insights.

**Format:** "We should [action] because [Insight X] suggests [expected outcome]."

**Examples:**
- "Show sample/demo analytics during onboarding before requiring first post creation"
  (because: users need value evidence before committing)
- "Revert the checkout layout to the previous version and iterate from there"
  (because: the redesign degraded completion metrics)

**Rules:**
- A recommendation MUST trace back to an insight, which traces to facts
- If the chain breaks at any point, the recommendation is an opinion, not evidence-based
- Multiple insights can support the same recommendation (stronger)
- A single insight can generate multiple alternative recommendations
- Always include the expected outcome -- what should change if this is right?

---

## How Atoms Connect

The relationships between atoms are non-linear. This is the power of the system.

```
Experiment A ──> Fact 1 ──┐
                          ├──> Insight X ──┐
Experiment B ──> Fact 2 ──┘               ├──> Recommendation 1
                                          │
Experiment A ──> Fact 3 ──┐               │
                          ├──> Insight Y ──┘
Experiment C ──> Fact 4 ──┘
                          
Experiment B ──> Fact 5 ──┐
                          ├──> Insight Z ──> Recommendation 2
Experiment C ──> Fact 6 ──┘
```

Key properties:
- One experiment generates multiple facts
- One fact can feed into multiple insights
- Facts from different experiments can reinforce the same insight
- Multiple insights can converge on one recommendation
- Evidence ACCUMULATES over time -- new experiments add facts that
  strengthen or weaken existing insights

---

## Confidence Scoring

Not all insights are equally well-supported. Score confidence based on the
evidence chain.

| Evidence | Confidence | What it means |
|----------|-----------|---------------|
| 1 fact from 1 source | LOW | A signal. Worth noting. Not enough to act on for big decisions. |
| 2-3 facts from 1 source | MEDIUM | A pattern within one study. Good enough for small splash zone decisions. |
| 3+ facts from 2+ sources | HIGH | Converging evidence. Strong enough for large splash zone decisions. |
| Facts that CONTRADICT the insight | CONTESTED | The evidence disagrees. Investigate before acting. |

**When presenting insights, always include the confidence level:**

```
INSIGHT: Users need value evidence before committing.
Confidence: HIGH
Supporting facts:
- [Fact 1] from [Experiment A]
- [Fact 2] from [Experiment A]
- [Fact 3] from [Experiment B]
```

---

## Synthesis Workflow

How to go from raw data to structured atoms.

### Step 1: Extract facts (per interview/session)

Immediately after each session, pull out facts:
- Specific behaviors observed
- Verbatim quotes (with context)
- Quantitative data points
- Anything surprising

Use the Single-Interview Snapshot template from interview-guide.md.

### Step 2: Look for patterns (across sessions)

After 3-5 sessions:
- Lay out all facts visually (physical notes, digital board, or list)
- Group facts that seem related
- Look for: things that repeat, things that contradict, things that surprise

### Step 3: Formulate insights

For each cluster of related facts:
- What does this pattern mean?
- Why might this be happening?
- What would change if this is true?

Write the insight as a declarative statement, not a question.
Good: "Users need value evidence before committing."
Bad: "Do users need to see value first?"

### Step 4: Generate recommendations

For each high-confidence insight:
- What should we do about this?
- What are the alternatives?
- What's the expected outcome?
- What would we measure to know if we're right?

### Step 5: Verify the chains

For every recommendation, trace backwards:
- Recommendation <- supported by which insights?
- Each insight <- supported by which facts?
- Each fact <- from which experiment?

If any link is missing, flag it. An unsupported recommendation is an
assumption wearing an evidence costume.

---

## Dealing With Contradictions

When facts contradict each other:

1. **Check the source:** Are both experiments equally credible? Different
   methods, different populations, or different contexts might explain the
   disagreement.
2. **Don't force resolution:** It's OK to have a CONTESTED insight. Present
   both sides: "Some evidence suggests X, but other evidence suggests Y."
3. **Use it as a research question:** Contradictions are the most interesting
   findings. They point to something you don't yet understand.
4. **Consider segments:** Maybe both are true -- for different user types,
   contexts, or stages of the journey.

---

## Maintaining a Research Repository

Over time, atoms accumulate into a knowledge base. Practical tips:

- **Tag atoms by topic:** user onboarding, checkout, pricing, retention, etc.
- **Review periodically:** Insights based on old facts may no longer be valid
  as the product changes
- **Mark deprecated atoms:** Don't delete old facts, but mark them if the
  product has changed significantly
- **Connect to decisions:** Link recommendations to the decisions they informed
  and the outcomes that resulted
- **Make it searchable:** When someone asks "what do we know about X?", the
  answer should be findable in minutes, not days

---

## Integration With Opportunity Solution Tree

Teresa Torres' Opportunity Solution Tree maps naturally to atomic research:

| OST concept | Atomic equivalent |
|------------|-------------------|
| Outcome | The decision being researched |
| Opportunity | Insight (a user need or pain point identified from evidence) |
| Solution | Recommendation (a proposed way to address the opportunity) |
| Assumption | Low-confidence insight that needs more evidence |
| Experiment | Experiment (the research activity to test an assumption) |

The atoms provide the evidence backbone for the tree. Every opportunity should
be an insight with supporting facts. Every assumption should have a planned
experiment to resolve it.

---

## Anti-Patterns

- **Insight without facts:** "Users want a simpler experience." Where's the
  evidence? This is an assumption.
- **Recommendation without insight:** "Let's add dark mode." Based on what
  user need? This is a feature request, not a research finding.
- **Facts as insights:** "4 out of 5 users clicked the wrong button." That's
  a fact. The insight is WHY -- "Users expect the primary action to be on the
  right side of the modal."
- **Confirmation bias:** Only extracting facts that support your hypothesis.
  Actively look for disconfirming evidence.
- **Synthesis by AI alone:** AI can help structure atoms, but the interpretation
  step (fact -> insight) requires human judgment. Always flag AI-assisted
  synthesis for human review.

---

## Templates

### Experiment atom
```
EXPERIMENT: [Method] with [participants/source]
Date: [when]
Context: [what prompted this research]
Decision it informs: [the decision from Step 1]
```

### Fact atom
```
FACT: [objective observation]
Source: [Experiment reference]
Verbatim: "[exact quote if from interview]"
```

### Insight atom
```
INSIGHT: [interpretation/pattern]
Confidence: [LOW / MEDIUM / HIGH / CONTESTED]
Supporting facts:
- [Fact 1] from [Experiment A]
- [Fact 2] from [Experiment B]
Contradicting facts (if any):
- [Fact X] from [Experiment C]
```

### Recommendation atom
```
RECOMMENDATION: [actionable next step]
Supporting insights:
- [Insight 1] (confidence: HIGH)
- [Insight 2] (confidence: MEDIUM)
Expected outcome: [what should change if this is right]
How to measure: [metric or observation]
```
