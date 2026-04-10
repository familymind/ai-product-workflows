# SKILL.md — familymind Competitive Intelligence

## Purpose

This skill governs all competitive analysis work for familymind.

It ensures that competitor research is structured, repeatable, and directly useful — feeding into positioning, messaging, fundraising narratives, and product decisions. It prevents wasted analysis that never connects back to a decision.

Every output produced under this skill must answer one question: what does this mean for familymind?

---

## Scope

Use this skill for:
- competitor profiling (new entrant or known player)
- periodic competitive landscape updates
- positioning gap analysis
- messaging differentiation checks
- investor questions about the competitive landscape
- feature comparison tables
- win/loss analysis
- market category framing
- identifying white space familymind can own
- updating the Competitors.xlsx tracker

Do not use this skill for general market research with no competitive angle, user research, or internal product decisions where competitor data is not the input.

---

## Source hierarchy

Use sources in this order.

### Tier 0 — live tracker

The primary source of truth is `Competitors.xlsx`, last shared March 2026 in Microsoft Teams.

Before doing any fresh research, check whether the competitor is already in the tracker and when it was last updated. If the entry is less than 90 days old, use it as the base and only flag what may have changed.

### Tier 1 — direct product observation

App store listings, product websites, onboarding flows, and feature pages. These are the highest-signal primary sources. Prefer direct observation over secondary reporting.

### Tier 2 — press and funding signals

TechCrunch, Crunchbase, LinkedIn announcements, and founder interviews. Use for funding status, team size, and strategic direction. Do not treat these as feature truth — product reality often diverges from press positioning.

### Tier 3 — user reviews and community

App store reviews, Reddit threads, ProductHunt comments. High signal for actual user frustration and unmet needs. Treat as qualitative data, not representative samples.

### Tier 4 — industry reports and analyst coverage

KPMG, McKinsey, Bertelsmann Stiftung family tech reports. Useful for market framing, not for specific competitor claims.

---

## Competitive landscape: familymind's context

### The category problem

familymind operates in a category that doesn't have a clean name yet. Competitors come from multiple adjacent categories. When assessing a competitor, always identify which of these buckets they sit in — because each has a different threat profile.

**Bucket A — Family organizer / coordination apps**
Tools like Cozi, OurHome, FamilyWall. These solve logistics (shared calendar, shopping lists, chore charts). They do not address mental load redistribution or AI-assisted shared responsibility. They are the most direct category overlap but have a fundamentally weaker value proposition.

**Bucket B — AI productivity / life management tools**
Tools like Notion AI, Structured, Motion. These are personal productivity tools that families sometimes co-opt. They are powerful but designed for individuals, not households. They lack the dual-user shared responsibility model.

**Bucket C — Parenting / family wellbeing apps**
Tools like Elmind, Kinfow, Tinybeans. These address parenting but from a child-development or memory-capture angle. Not mental load. Not dual-career partnership design.

**Bucket D — B2B2C employer-side tools**
HR platforms adding family support modules (e.g. Voiio, Fürstenberg Institut in the DACH market). These are entering the employer benefit space where familymind is building its B2B sales track. These are the highest strategic threat for the B2B channel.

**Bucket E — Childcare and backup care marketplaces**
On-demand childcare networks and staffing platforms: Care.com, UrbanSitter, Komae, Babysitter.com, Yoanna, femville, Sunday-like services. These solve a specific coordination problem (who cares for the child right now?) but do not address the broader mental load or shared-responsibility design problem. The strategic risk is adjacent: if these platforms add AI coordination or household management features, they enter familymind territory from a large user base.

**Bucket F — Emerging AI family assistants**
Any new entrant explicitly positioning around AI + family + mental load. This bucket is currently sparse but is the most likely space for a well-funded direct competitor to appear. Monitor closely.

---

## Research protocol

When researching a competitor, follow this sequence:

1. **Identify the bucket** — which of the five categories above does this competitor primarily sit in?
2. **Profile the basics** — founding year, funding status, team size estimate, primary market (DACH, US, global), pricing model, primary user (individual vs. household), app platforms
3. **Map the feature surface** — what does the product actually do? Be specific. Do not rely on marketing language.
4. **Assess the positioning** — what problem do they claim to solve? What emotion do they market to? What does their homepage hero say?
5. **Find the gap** — what do users complain about in reviews? What does the product not do?
6. **Draw the familymind implication** — where does familymind differentiate? Where is there genuine overlap risk? Is this a threat, a validation, or irrelevant?

---

## Differentiation anchors

These are familymind's core differentiators. Use them as the lens for every competitive assessment. A competitor is only a real threat if they close one of these gaps.

- **Shared responsibility by design** — familymind is built for two adults managing a household together, not one person organizing their family. This is not a feature. It is the fundamental design premise.
- **Mental load as the problem statement** — familymind names the invisible cognitive burden explicitly. Most competitors either ignore it or frame it as a productivity problem. familymind frames it as a fairness and relationship problem.
- **AI as a family-level assistant** — not a personal assistant used by parents, but a system that serves the household unit. This is architecturally and conceptually different.
- **Dual-career and German-speaking market depth** — familymind has cultural and linguistic specificity in the DACH market that international tools lack. This is a moat for the German-language employer benefit track.

---

## Output rules

**Competitor profiles** must include: bucket classification, funding status, primary user model, top 3 features, top 3 weaknesses (from user evidence), familymind differentiation summary (max 3 sentences).

**Landscape summaries** (for investor use) must: name the categories, not individual tools; lead with the white space familymind owns; end with a statement of why no current player is solving the same problem in the same way.

**Messaging differentiation checks** must: take a specific familymind claim and stress-test whether any competitor can make the same claim truthfully. If yes, flag it as a weak differentiator. If no, confirm it as ownable.

**Feature comparisons** must: use direct observation, not marketing copy; mark any unverified claims as [unverified]; never claim a feature advantage that hasn't been tested.

---

## What to avoid

Do not exaggerate competitor weakness to make familymind look better. Investors and partners will fact-check this. Accuracy builds credibility.

Do not treat market size from competitor fundraising narratives as validated data. Competitors overstate TAM in their own materials.

Do not conflate "many competitors exist" with "crowded market." The number of competitors is less important than whether any of them have solved the same problem for the same user. So far, none have.

Do not produce a competitor analysis without a clear "so what for familymind" section. Analysis without implication is wasted work.

---

## Maintenance

The competitive landscape should be reviewed at minimum quarterly. When a competitor raises funding, launches a major feature, or enters the DACH market, trigger an immediate update regardless of the quarterly schedule.

Updates go first into `Competitors.xlsx`, then into any pitch deck or positioning document that references specific competitors.
