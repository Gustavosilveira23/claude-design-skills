# Interview & Research Instrument Guide

Detailed guidance for generating research instruments: interview scripts,
survey structures, and usability test plans. Use this reference in the
Interview phase (Step 8).

---

## Interview Scripts: "Excavate the Story"

Teresa Torres' technique prioritizes chronological behavioral evidence over
opinions and hypotheticals. The goal: understand what users ACTUALLY DID.

### Why This Technique Works

People are terrible at predicting their own future behavior ("I would
definitely use that!") but reasonable at recounting specific past events.
By focusing on the last time they did something, you get:

- Real behaviors, not aspirational answers
- Specific details and context
- Emotional reactions tied to concrete moments
- Workarounds and coping mechanisms they might not think to mention

### The Core Pattern

```
1. "Tell me about the last time you [did X]..."
2. "What happened first?"
3. "Then what happened?"
4. "What did you do next?"
5. (Keep following the timeline until the story is complete)
```

Resist the urge to jump ahead. Let the story unfold chronologically. The
details you didn't think to ask about are often the most valuable.

### Follow-Up Probes

When you hit something interesting, go deeper:

| Situation | Probe |
|-----------|-------|
| They mention a pain point | "What did you do when that happened?" |
| They describe a workaround | "How did you figure out that approach?" |
| They express emotion | "What was that like for you?" |
| They skip a step | "Walk me back -- what happened between X and Y?" |
| They give a vague answer | "Can you give me a specific example?" |
| They state an opinion | "Tell me about a time when that was the case." |
| They mention another tool | "Show me how you use that." (if possible) |

### Questions to AVOID

| Bad question | Why | Better alternative |
|-------------|-----|-------------------|
| "Would you use this feature?" | Hypothetical -- no predictive value | "Tell me about the last time you needed to [do the thing this feature enables]" |
| "Do you like this?" | Opinion -- not behavior | "Walk me through what you just did. What worked? What didn't?" |
| "Why did you do that?" | Triggers post-hoc rationalization | "What led you to do that?" or "What were you thinking at that moment?" |
| "Don't you think X is better?" | Leading | "How does X compare to Y in your experience?" |
| "How often do you...?" | People can't accurately self-report frequency | "When was the last time? And before that?" (triangulate frequency from specifics) |
| Two questions at once | Confusing, one gets dropped | Ask one at a time, wait for the full answer |

---

## Interview Script Template

### Pre-interview setup
- Confirm recording consent
- Explain format: "I'll ask questions, there are no wrong answers, I'm here to learn from your experience"
- Set time expectation

### Section 1: Context (2-3 min)
Goal: understand who this person is and their relationship to the problem space.

```
- "Tell me a bit about your role / what you do day to day."
- "How does [problem domain] fit into your work/life?"
- "What tools/processes do you currently use for [relevant activity]?"
```

### Section 2: Story excavation (15-20 min)
Goal: detailed chronological account of relevant experiences.

```
- "Think about the last time you [did the thing related to your research question].
  Walk me through what happened from the beginning."

Follow the story:
- "What happened first?"
- "Then what did you do?"
- "What were you thinking at that point?"
- "How did that turn out?"

Probe pain points:
- "You mentioned [X] was frustrating. What did you do about it?"
- "What would have made that easier?"

Probe workarounds:
- "Is that how you usually handle it, or was this different?"
- "What have you tried before?"
```

### Section 3: Broader context (5-7 min)
Goal: understand patterns beyond the single story.

```
- "Is that experience typical? What varies?"
- "What's the best experience you've had with [domain]? What made it good?"
- "What's the worst? What made it bad?"
- "If you could change one thing about how [domain] works, what would it be?"
```

### Section 4: Wrap-up (2-3 min)
```
- "Is there anything I didn't ask that you think is important?"
- "Anyone else you'd recommend I talk to about this?"
- Thank them. Explain next steps if applicable.
```

---

## Single-Interview Snapshot Template

After each interview, create a quick snapshot for synthesis. Do this
immediately while details are fresh.

```
INTERVIEW SNAPSHOT
Participant: [ID or pseudonym, not real name]
Date: [date]
Context: [role, experience level, relevant demographics]

KEY QUOTES (verbatim):
1. "[exact words]" -- context: [what prompted this]
2. "[exact words]" -- context: [what prompted this]
3. "[exact words]" -- context: [what prompted this]

BEHAVIORS OBSERVED:
1. [What they actually did, not what they said they'd do]
2. [Workarounds, unexpected approaches]

PAIN POINTS:
1. [Specific friction, with context]
2. [Specific friction, with context]

SURPRISES:
- [Anything you didn't expect to hear]

PRELIMINARY ATOMS (to refine in synthesis):
- FACT: [raw observation, no interpretation]
- FACT: [raw observation, no interpretation]
```

---

## Survey Structure Builder

### When to use surveys

Surveys quantify and segment. They answer "how many?" and "which group?"
-- not "why?"

If you don't know what questions to ask, do interviews first.

### Structure

**1. Screening questions (1-3)**
Filter out respondents who aren't in your target audience.
```
"How often do you [relevant behavior]?"
- Daily
- Weekly
- Monthly
- Rarely
- Never → screen out
```

**2. Segmentation questions (2-4)**
Classify respondents for later analysis.
```
Role, company size, experience level, usage frequency
```

**3. Core questions (5-10)**
Aligned to your evidence needs from Step 4.

| Evidence need | Question type |
|--------------|---------------|
| Prevalence of a problem | "Have you experienced [X] in the last month?" (yes/no + frequency) |
| Severity ranking | "Rank these challenges from most to least impactful" |
| Satisfaction | Likert scale: "How satisfied are you with [X]?" (1-7) |
| Preference | "Which approach would you prefer?" (with visuals if possible) |
| Open exploration | "What is the biggest challenge you face with [domain]?" (open-ended, limit to 1-2) |

**4. Open-ended catch-all (1)**
```
"Is there anything else you'd like to share about [topic]?"
```

### Survey anti-patterns
- More than 15 minutes (completion drops sharply)
- All open-ended questions (analysis nightmare)
- Double-barreled questions ("How satisfied are you with speed and reliability?")
- Leading scales ("How much do you love our product?")
- No screening (garbage in, garbage out)

---

## Usability Test Script Template

### Setup
```
"Thank you for participating. I'm going to ask you to complete some tasks
using [product/prototype]. There are no wrong answers -- we're testing the
product, not you. Please think aloud as you work -- tell me what you're
looking at, what you're thinking, what you expect to happen."
```

### Task format
```
TASK [N]: [Goal-oriented description, not step-by-step instructions]

Scenario: "Imagine you [context]. You want to [goal]."

Success criteria:
- [ ] Completed the task
- [ ] Completed without errors
- [ ] Completed within [time threshold]

Observe:
- Where they click first
- Where they hesitate
- What they say while thinking aloud
- Whether they use the expected path

Post-task:
- "How easy or difficult was that?" (1-7 scale)
- "What did you expect to happen when you clicked [X]?"
- "Was anything confusing?"
```

### Important rules
- Write TASKS, not instructions. "Find the cheapest flight to Paris" not "Click on search, type Paris, sort by price."
- Randomize task order across participants to avoid learning effects
- Have a backup task if they get completely stuck
- Don't help unless they're truly stuck (and note that it happened)

### Post-test questions
```
- "Overall, how would you describe your experience?"
- "What was the easiest part? The hardest?"
- "How does this compare to [competitor/current tool]?"
- "Would you use this? Why or why not?" (take with a grain of salt -- behavior > opinion)
```

---

## Common Interview Mistakes

| Mistake | Consequence | Fix |
|---------|------------|-----|
| Asking about future behavior | Get aspirational answers, not real data | Ask about past behavior: "last time you..." |
| Talking more than listening | Miss the insights in what users say | 80/20 rule: they talk 80%, you 20% |
| Confirming your hypothesis | Validation theater | Write down what would DISPROVE your hypothesis, then look for that |
| Not recording | Lose verbatim quotes, misremember | Always record (with consent). Notes alone miss nuance |
| Interviewing only power users | Survivorship bias | Include churned users, new users, edge cases |
| Skipping synthesis | Raw notes rot. Insights emerge from comparison | Create snapshots immediately, synthesize within 48 hours |
| Group interviews as research | Social dynamics distort answers | Use 1-on-1 for research. Focus groups are for idea generation only |
