# Copy and Content Design Reference

Deep-dive reference for UX copy audits, content strategy, and microcopy
decisions. Use this when copy is the primary focus of the task.

For the core principles (always applied), see Step 6 in the main SKILL.md.

---

## 1. Terminology Governance

### The Term Introduction Arc

New product terms follow a 3-phase arc across the experience:

```
Phase 1: INTRODUCE    Phase 2: REINFORCE    Phase 3: ASSUME
─────────────────     ─────────────────     ─────────────────
First screen/section  Next 1-2 screens      Rest of experience
Define explicitly     Use with light         Use freely — the
("A Duo is...")       context ("Your Duo     user now owns the
                      guides members...")     mental model
```

**Rules:**
- Never use a product term in Phase 3 position if it hasn't been through
  Phase 1 and 2 first.
- If a user can jump directly to a section (via navigation, deep link, or
  anchor), that section needs at least Phase 2 context — don't assume they
  read everything above.
- The FAQ is NOT Phase 1. It's a fallback. If the term needs an FAQ to be
  understood, the introduction failed.

### Term Audit Checklist

When auditing terminology across a page or product:

1. **List every term** used for the core concept(s)
2. **Count occurrences** of each variant
3. **Map where each first appears** — is it introduced or dropped cold?
4. **Check casing** — is it consistent? Does the casing match the intent?
   - Proper noun ("Duo") = warm, product-like, name-like
   - ALL CAPS ("DUO") = acronym feel, technical, cold
   - Lowercase ("duo") = generic, not a product name
5. **Check the decision moment** — does the CTA use the same term the page
   has been building? A new term at CTA is a conversion killer.
6. **Check the close** — does the footer/final section echo the hero? The
   peak-end rule means the last term matters as much as the first.

### Common Terminology Mistakes

| Mistake | Example | Fix |
|---------|---------|-----|
| Synonym overload | "agent", "bot", "assistant", "guide", "Duo" for the same thing | Pick one primary term |
| Cold introduction | "Your DUO guides..." (first mention, no definition) | Add Phase 1 before using |
| Term switch at CTA | Hero says "Duo", CTA says "Copilot" | Use the hero term at CTA |
| Internal jargon leaking | "RAG-powered knowledge base" on marketing page | "Trained on your content" |
| Inconsistent casing | "DUO" in copy, "Duo" in UI, "duo" in URL | Standardize everywhere |

---

## 2. Persuasion Frameworks for Marketing Pages

### PAS (Problem — Agitate — Solution)

Best for: landing pages, email sequences, ad copy.

1. **Problem**: Name the pain the user already feels. Use "you" language.
   "You create content once, but it never adapts."
2. **Agitate**: Make the cost of inaction tangible. Quantify if possible.
   "Every month, 85% of your students stop engaging after week 2."
3. **Solution**: Show how the product resolves the pain.
   "Your Duo adapts to each member's pace, keeping them engaged 24/7."

### AIDA (Attention — Interest — Desire — Action)

Best for: structured sales pages, one-pagers, product tours.

1. **Attention**: Stop the scroll. Bold claim, surprising stat, or direct question.
2. **Interest**: Expand with specifics. How does this work? What's different?
3. **Desire**: Social proof, outcomes, emotional connection. "Imagine if..."
4. **Action**: Clear, single CTA. Remove all friction.

### Before/After/Bridge (BAB)

Best for: short copy (ads, social posts, email subject lines).

1. **Before**: Current painful state.
2. **After**: Desired outcome.
3. **Bridge**: The product connects the two.

---

## 3. LP Copy Hierarchy

Landing page copy follows a specific rhythm. Each section serves a function
in the decision journey.

### Decision Journey Map

```
ORIENTATION     →  CREDIBILITY    →  EVALUATION    →  COMMITMENT
"What is this?"    "Can I trust     "Is it worth      "Let me try it"
                    this?"           the effort?"
```

### Section-by-Section Copy Rules

| Section | Copy job | Rules |
|---------|----------|-------|
| **Hero headline** | Answer "what is this?" in < 10 words | Benefit-first, no jargon. If you need a subtitle to explain the headline, the headline is too clever. |
| **Hero description** | Connect benefit to mechanism | Introduce the product name here. "Build a [Product] — [what it is] — that [what it does]." |
| **Hero CTA** | One primary, one secondary max | Primary = conversion action. Secondary = learn more (scroll). Microcopy below to reduce anxiety ("15 min. No commitment.") |
| **Problem** | Name the pain in the user's words | 3 pain points max. Use "you" language. Don't describe the market — describe the person's Tuesday. |
| **Solution/Features** | Translate features into outcomes | "30+ interactive components" → "Learning experiences that stick, not just text replies." Lead with what changes for the user. |
| **Social proof** | Validate the promise | ALWAYS before the final CTA, not after. Real names + photos + specific results. "Creator" is not social proof — "Maria, Fitness Coach, 2x retention" is. |
| **FAQ** | Handle objections, not repeat the pitch | If a FAQ answer just rephrases the hero, delete it. Good FAQs address fears: "Does the AI replace me?", "Do I need technical skills?" |
| **Final CTA** | Close with the SAME term as the hero | No new concepts. Echo the hero language. Reduce to one CTA + one line of reassurance. |

### Above-the-Fold Checklist

Within 5 seconds of landing, the visitor must understand:
- [ ] What this is (product/service category)
- [ ] Who it's for (do I belong here?)
- [ ] What I get (outcome, not feature)
- [ ] What to do next (one clear CTA)

If any of these require scrolling, the hero needs work.

---

## 4. Copy Audit Workflow

Step-by-step process for auditing copy on any page or flow.

### Step 1: Term Map

Create a table of every term used for each core concept. Include:
- Section where it appears
- Exact text
- Whether it's the first mention
- Casing used

### Step 2: Journey Read

Read the page top-to-bottom as a first-time visitor. Note:
- Where do you first understand the product name?
- Where do you first understand what it does?
- Is there a moment of confusion? Mark it.
- Does the CTA feel like a natural next step, or a surprise?

### Step 3: Component Scan

For each UI component, check:
- Buttons: verb + outcome?
- Errors: what + why + what now?
- Empty states: why + what to do?
- Placeholders: example, not label?
- Tooltips: present where needed?

### Step 4: Consistency Check

- Same product = same term everywhere?
- Same action = same button label everywhere?
- Tone consistent across sections?
- Casing consistent across surfaces?

### Step 5: Report

Use the CLEAR Scorecard "C" sub-criteria for structured reporting.
Include specific locations (section + file + line) and proposed rewrites.

---

## 5. Voice & Tone Situations

Tone varies by context. Voice stays constant. Here's how tone shifts:

| Situation | Tone | Example |
|-----------|------|---------|
| **Error / failure** | Calm, clear, no blame | "That email isn't registered. Check the spelling or create a new account." |
| **Success / completion** | Brief, confirming | "Done. Your changes are saved." |
| **Onboarding** | Encouraging, one step at a time | "Great start. Next, add your first content source." |
| **Waiting / loading** | Informative, not apologetic | "Generating your report..." (not "Please wait...") |
| **Destructive action** | Serious, specific consequences | "This will permanently delete 12 projects. This cannot be undone." |
| **Empty state** | Helpful, inviting action | "No courses yet. Create your first one to get started." |
| **Upsell / upgrade** | Value-first, not pushy | "Conversation history is available on the Pro plan." |
| **Legal / compliance** | Plain language, no legalese | "We use cookies to remember your preferences." |

---

## 6. Common Copy Mistakes

### In Product UIs
- **Label as placeholder**: "Enter your email" disappears on focus — use
  a visible label above the field instead
- **Vague CTAs**: "Submit", "Continue", "OK" — name the outcome
- **Double negatives in toggles**: "Disable notifications: Off" — impossible
  to parse. Use positive framing: "Notifications: On"
- **Robot tone**: "An error has occurred" — write like a human: "Something
  went wrong. Try again, or contact support."

### In Landing Pages
- **Feature-first headlines**: "AI-powered RAG with 40+ connectors" — leads
  with mechanism, not benefit. Flip it: "Your knowledge, available to every
  member, 24/7"
- **Multiple CTAs competing**: 3 buttons above the fold — choose one primary
  action per section
- **Social proof without specifics**: "Loved by creators" — who? How many?
  What result? Anonymous testimonials are invisible.
- **Clever over clear**: "Unleash the power of knowledge synergy" — nobody
  knows what this means. Say what it does.

---

## 7. Microcopy Patterns

Reusable patterns for common interface moments.

### Authentication
```
Login:    "Log in" (two words as verb)
Signup:   "Create account" (not "Sign up" if you need name/email/password)
Reset:    "Reset password" → "Check your email for a reset link."
Error:    "Incorrect email or password." (never reveal which one is wrong)
```

### Forms
```
Required:    Mark optional fields, not required ones (most fields are required)
Validation:  Show errors inline as the user types, not on submit
Password:    Show requirements upfront, check in real-time
Long forms:  Break into steps with progress indicator + "Step 2 of 4"
```

### Destructive Actions
```
Title:       "[Verb] [object]?" — "Delete this project?"
Body:        Specific consequence — "This will remove 12 files and 3 team members'
             access. This cannot be undone."
Confirm:     Name the action — "Delete project" (red/destructive)
Cancel:      Safe exit — "Keep project" (not just "Cancel")
```

### Empty States
```
Title:       What's missing — "No projects yet"
Body:        What to do — "Create your first project to get started."
CTA:         Action button — "Create Project"
Illustration: Optional, but helps set tone (welcoming, not broken)
```

---

## 8. AI Language Tells (De-AI Any Copy)

AI writes **abstract, uniform, and hedge-y**. Humans write **concrete, specific,
with varied rhythm**. Run this after generating or editing any copy — LP, post,
bio, email, or UI writing. The fix is almost always the same: swap an abstraction
for a fact/number/concrete noun, cut the crutch, vary sentence length.

Full source guide (structural tells + EN/PT-BR/ES word lists + fast checklist):
`Mind/3-Recursos/vicios-linguagem-ia-copy.md` in Gustavo's vault.

### Structural Tells (language-agnostic)

| Tell | Example | Fix |
|------|---------|-----|
| Em-dash as rhythm crutch | "The platform — built for X — does Y" | Period or comma; rewrite |
| Contrast reframe "not X, but Y" / "não é X, é Y" | "Not a library, it's transformation" | Max 1× per page; prefer a direct claim |
| Rule of three (3 adjectives posing as complete) | "fast, simple, and powerful" | Cut to 1-2 specifics, or give numbers |
| Avoiding "is/are" (serves as, acts as, represents) | "X serves as a layer of..." | "X is..." — direct |
| Hedging ("aims to", "busca", "feito para", "can help") | "that aims to help" | Assert it: "that helps" |
| Elegant variation (new synonym every sentence) | course → content → material → journey | Repeat the right word; clarity > variety |
| Inflated importance ("pivotal", "revolutionary", "game-changer") | "a revolutionary change" | Cut the superlative; show the result |
| Uniform sentences (all same length, mechanical) | 3 medium sentences in a row | Alternate short + long; a 3-word sentence lands |
| Auto openers | "Additionally", "Moreover", "Imagine a world where…" | Start with the concrete idea |

### Word Lists

- **EN buzzwords:** delve, unlock, elevate, seamless, robust, leverage,
  supercharge, empower, transform (your X into Y), tapestry, landscape,
  testament, boasts, intricate, vibrant, cutting-edge, revolutionize,
  "in today's fast-paced world", "it's not just X, it's Y", "take it to the
  next level". → Prefer concrete verbs (build, run, keep, see, answer), numbers,
  the real name of the thing.
- **PT-BR:** verbos-clichê (transforme, descomplique, eleve, impulsione,
  potencialize, revolucione, desbloqueie, alavanque, maximize); adjetivos-balde
  (incrível, poderoso, inovador, revolucionário, único, completo, robusto,
  intuitivo); substantivos vazios (jornada, solução, ecossistema, universo,
  potencial, experiência); conectores-muleta ("Além disso,", "Vale ressaltar,",
  "No mundo de hoje,"). → Dizer o que a coisa faz com um fato.
- **ES:** verbos-cliché (transforma, impulsa, potencia, eleva, desbloquea,
  revoluciona, descubre el poder de); adjetivos-balde (increíble, poderoso,
  innovador, revolucionario); conectores en exceso ("Además,", "Cabe destacar,",
  "En el mundo actual,"). → Afirmar con un dato.

### Fast Checklist

1. Rhythm em-dash? → remove/rewrite.
2. "not X, but Y" / "não é X, é Y"? → max 1×.
3. Buzzword from the list? → swap for a concrete verb/fact.
4. Hedge ("busca", "aims to", "feito para")? → assert directly.
5. Generic rule-of-three? → cut, or add a number.
6. Any abstraction that could be a number/real name? → swap it.
7. All sentences the same length? → vary the rhythm.

### Always Preserve

- Official brand taglines (even if they're marketing parallelism).
- Verbatim testimonial quotes (never edit).
- Real product terms and proper names.