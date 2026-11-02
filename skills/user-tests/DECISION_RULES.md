# DECISION_RULES.md — User Test Decision Logic

Use this file when findings from a test round need to be translated into a product or strategy decision. It defines the rules for how test evidence should be interpreted and acted on.

---

## When to act on a finding

### Act immediately if
- 4 or more participants encountered the same critical failure (could not complete a core task, lost trust, or expressed confusion about the core value proposition)
- A finding contradicts a core product assumption
- A finding reveals a safety, privacy, or trust issue

### Act in the next sprint if
- 2 to 3 participants showed the same friction pattern
- A task had a success rate below 50% across sessions
- Multiple participants expressed the same unmet expectation

### Monitor and retest if
- A pattern appeared in only 1 session
- Findings are based primarily on stated preference, not observed behavior
- The participant who flagged the issue was clearly outside the core user profile

### Deprioritize if
- The issue only appeared in edge-case participant profiles
- The finding conflicts with stronger behavioral evidence from other participants
- The issue does not connect to a current product priority

---

## How to weight evidence

Use this hierarchy when evidence conflicts:

1. Behavioral evidence — what users actually did under realistic conditions
2. Verbal evidence during tasks — what users said while doing the task
3. Immediate recall — what users remembered or described right after the task
4. Stated preference in debrief — what users said they would like or prefer
5. Speculative preference — what users imagined they would do in other situations

Do not let a single strong opinion override consistent behavioral evidence.

---

## Confidence thresholds for product decisions

| Confidence level | Evidence basis | Recommended action |
|-----------------|---------------|-------------------|
| High (4+ sessions) | Consistent observed behavior | Act on it |
| Medium (2–3 sessions) | Repeated pattern | Plan a fix, retest to confirm |
| Low (1 session) | Single observation | Flag and monitor in next round |
| Hypothesis | Inferred, not tested | Add to next test scope |

---

## Decision documentation

When making a product decision based on test findings, document:

1. **Finding** — what was observed, in how many sessions, at what confidence level
2. **Decision** — what will change and why
3. **Alternative considered** — what was not chosen and why
4. **Validation plan** — how the change will be tested in the next round
5. **Owner** — who is responsible for the change
6. **Date** — when the decision was made

This creates a traceable record that prevents the same questions from being relitigated in future test rounds.

---

## familymind-specific decision rules

### If users don't understand what familymind does within 30 seconds of first contact
→ The value proposition framing needs work. Do not proceed with conversion testing until comprehension is resolved.

### If users understand but don't feel the personal relevance
→ The emotional framing or use cases shown are not close enough to lived reality. Adjust before next round.

### If users trust the product concept but don't trust the AI specifically
→ Prioritize trust-building elements: data transparency, control mechanisms, examples of AI behavior. Do not expand AI features until trust baseline is established.

### If both partners need to be won over but only one was involved in testing
→ The test is incomplete for shared-responsibility features. Add partner participants to the next round before shipping.

### If onboarding drives interest but low activation intent
→ The gap is between concept appeal and perceived effort. Reduce friction in the first 3 minutes of use before scaling acquisition.
