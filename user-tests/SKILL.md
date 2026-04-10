# SKILL.md — User Test Assets and Templates Guardrail

## Purpose

This skill governs how to create, update, review, and extend all user test assets for familymind.

The goal is to ensure that every user testing asset is:
- decision-oriented
- consistent across rounds
- lightweight enough to use in fast product cycles
- rigorous enough to support product, UX, and founder decisions
- comparable across tests over time

---

## Use this skill for

- user test plans
- interview scripts
- moderator guides
- task scenarios
- prototype test briefs
- recruitment messages
- screener questions
- note-taking templates
- synthesis frameworks
- insight readouts
- pattern summaries
- decision recommendations from test findings
- follow-up test briefs based on prior findings

Do not use this skill for: general product strategy that does not rely on user evidence, marketing copy, investor communications, or financial analysis.

---

## familymind user testing context

familymind is an AI Family Assistant for modern families. It addresses mental load, shared responsibility, and coordination in dual-career households.

The core user being tested is typically:
- a working parent, often a mother in a dual-career household
- a family with young children
- someone experiencing mental load, coordination stress, or unequal care work distribution

Testing priorities for familymind focus on:
- whether users understand what the product does quickly
- whether the AI feel trustworthy and useful in a family context
- whether shared-responsibility features land clearly for both partners
- whether the onboarding creates genuine intent to use, not just interest
- whether the value proposition is felt, not just understood

---

## Core testing principles

### Test to decide, not to confirm

Every test asset should be designed around a decision that needs to be made. If there is no clear decision, the test scope is too broad or the timing is wrong.

Before creating any test asset, identify:
1. What decision does this test need to inform?
2. What would we do differently depending on the findings?
3. What is the minimum we need to observe to be confident?

### Observation over opinion

Prioritize behavioral evidence over stated preference. Evidence hierarchy:

1. what users actually do under realistic conditions
2. where users get stuck, confused, or give up
3. what users say while doing the task (think-aloud)
4. what users remember or report immediately after
5. stated preference after real interaction
6. speculative preference without interaction

Do not let one strong opinion outweigh repeated behavioral evidence.

### Consistency across rounds

Use consistent structures, question types, and observation frameworks across test rounds so findings can be compared over time. When changing a test structure, note explicitly what changed and why.

### Participant quality over quantity

For early-stage familymind testing, 5 to 10 participants per round is usually enough to identify major patterns. The current sharpened target profile for recruitment (as of April 2026 alpha phase) is:

- dual-career parents (both partners working)
- 2 or more children
- children in kindergarten or early school years

This is more specific than "working parents with young children" — the dual-career + kindergarten-age combination is where the mental load problem is most acute and most clearly felt. Prioritize this profile over broader working-parent recruitment.

Whether you already know familymind or are discovering it for the first time is less important than genuine relevance to daily family life and motivation to contribute honest feedback.

---

## Output style rules

All outputs should be:
- concise
- practical
- structured for decisions, not for documentation
- free of fluff and decorative language
- specific about what was observed
- explicit about confidence level and limitations

### Preferred phrasing
- "We observed..."
- "Users frequently..."
- "In X of Y sessions..."
- "This suggests..."
- "Likely issue type: navigation / comprehension / trust / workflow / value perception"
- "Recommended next move..."

### Avoid
- generic UX jargon without evidence
- overdramatic claims from a single observation
- long theory sections
- vague positivity ("users seemed engaged")
- conclusions that exceed what the data supports

---

## Required sections for any final user test readout

Every final readout must contain:
1. Objective — what decision this test was designed to inform
2. Test setup — method, format, duration, prototype or product version
3. Participant profile — how many, key characteristics, recruitment criteria
4. Key observations — what actually happened, session by session or as a synthesized set
5. Pattern summary — which observations appeared across multiple participants
6. What this likely means — interpretation, with confidence level stated
7. Recommended next actions — specific, prioritized, decision-linked
8. Confidence / limitations — what this test can and cannot tell us
9. Open questions — what remains unresolved and needs further testing

---

## Asset naming convention

Use this naming format for consistency:

`[round]-[type]-[date].md`

Examples:
- `r1-test-plan-2026-04.md`
- `r2-moderator-guide-2026-06.md`
- `r3-readout-2026-08.md`

---

## Confidence labeling

When reporting findings, always label confidence:

- **High confidence** — observed in 4+ sessions, consistent behavior pattern
- **Medium confidence** — observed in 2 to 3 sessions, plausible pattern
- **Low confidence** — observed once or based primarily on stated preference
- **Hypothesis** — not yet tested, inferred from related observations

---

## Two-segment testing protocol

As of April 2026, familymind runs structured two-segment tests for new product versions. This protocol must be followed for any test that involves both existing and new users.

### The two segments

**Segment A — Existing users (familiar with old app)**
Core question: "Is the new app better?"
Focus areas: migration experience, what feels improved or worse, feature understanding vs expectations, missing features.
Sample: 5–8 participants.

**Segment B — New users (no prior familymind experience)**
Core question: "Does this make sense at all?"
Focus areas: first-time understanding, activation (do they "get it"?), perceived value, habit formation.
Sample: 8–10 participants.

Critical rule: **never combine analysis or reporting across segments.** Findings from Segment A and Segment B must always be reported separately. Side-by-side summaries are allowed only when explicitly comparing segment differences, not as a default.

### Research structure (2 weeks per participant)

**Week 1 — Onboarding & First Value ("Do they get it quickly?")**
- Day 1–2: observe onboarding
- Day 3–7: first real usage — track setup completion, family invites sent, use of at least one core feature

**Week 2 — Real-life usage ("Does it stick?")**
- Track returns, trust signals, perceived reduction in mental load

### Feedback channels

1. Behavioral data: logins, feature usage, drop-offs, invites sent
2. In-the-moment micro-feedback: single-question nudges ("Was this helpful?")
3. Deep feedback: one 30-minute interview per participant at end of Week 2
4. Discord community: quick feedback channel for participants during the test period

### Segment-specific success metrics

**New users (Segment B):**
- % completing onboarding
- % using at least one key feature
- % returning after Day 3

**Existing users (Segment A):**
- % reporting "better than before"
- % switching fully to new app
- Count of complaints about removed features

### Segment-specific interview focus

**New users:** When did it click? What confused you? What did you expect this app to do? Probe: value moments, blockers to return.

**Existing users:** What feels worse than before? What did you miss immediately? What is clearly better? Probe: migration pain points, feature parity gaps.

### Operational notes

- Current alpha/beta test start date: 15 April 2026, duration 2 weeks
- All test data is deleted after the test period
- Participants must provide their email and their partner's email upfront so both can be added to the tester group
- Test instructions: https://familymind.ai/how-to-beta-test/
- Stagger participant start dates if needed to manage interview load
- Ensure device and platform mix reflects the real target user base

---

## Escalation rule

If a user test reveals a finding that suggests a core product assumption is wrong, escalate immediately to the founder rather than waiting for the full readout. Do not bury critical findings inside a long document.
