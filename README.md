# ai-product-workflows

This repository is the knowledge base for familymind's AI agents. It contains the skills, templates, checklists, and brand context that AI agents should read before starting any task. Always load the relevant files before generating output — skipping context is the primary cause of generic, off-brand results.

---

## How AI agents should use this repo

### Step 1 — load brand context first

Always start with `brand/BRAND_CONTEXT.md` for any task that involves external-facing communication, messaging, or content. This is the single source of truth for company identity, voice, and positioning.

### Step 2 — load the domain skill file

Each folder contains a `SKILL.md` that defines the rules, priorities, scope, and output behavior for that domain. Read it before starting any task in that domain.

### Step 3 — load companion files as needed

Most domain folders contain companion files:
- `ASSET_TEMPLATES.md` — default output structures by asset type
- `REVIEW_CHECKLISTS.md` — quality criteria for reviewing and approving outputs
- `DECISION_RULES.md` — logic for translating findings into decisions (user-tests)

### Do not skip context loading

Agents that produce generic outputs do so because they skipped the brand and skill context. Loading the relevant files is not optional — it is the difference between a publish-ready output and a placeholder.

---

## Repository structure

```
ai-product-workflows/
├── README.md                              ← you are here
│
├── brand/
│   └── BRAND_CONTEXT.md                  ← load first for any external task
│
├── marketing/
│   ├── SKILL.md                          ← marketing strategy, voice, channel rules
│   ├── ASSET_TEMPLATES.md                ← templates per asset type
│   └── REVIEW_CHECKLISTS.md              ← quality criteria per channel
│
├── content-creation/
│   └── SKILL.md                          ← drafting, formatting, repurposing rules
│
├── linkedin/
│   └── SKILL.md                          ← Rosa's personal LinkedIn founder profile
│
├── sales/
│   └── SKILL.md                          ← B2B2C sales, partner outreach, objections
│
├── finance/
│   ├── SKILL.md                          ← finance guardrail, source hierarchy, live facts
│   ├── REVIEW_CHECKLISTS.md              ← finance output QA
│   └── ASSET_TEMPLATES.md                ← reusable finance communication templates
│
├── user-tests/
│   ├── SKILL.md                          ← user testing principles and rules
│   ├── ASSET_TEMPLATES.md                ← test plans, guides, readout templates
│   ├── REVIEW_CHECKLISTS.md              ← asset review before sessions and sharing
│   └── DECISION_RULES.md                 ← how to translate findings into decisions
│
├── competitive-intelligence/
│   └── SKILL.md                          ← competitor research, landscape analysis, differentiation
│
└── product/
    └── SKILL.md                          ← product documentation (in development)
```

---

## What each folder does

### brand/
The single source of truth for familymind's identity. Load before any external-facing task. Contains: company overview, core positioning, messaging pillars, brand name rules (always lowercase: familymind), founder context, target audiences, brand voice, and what familymind is not.

### marketing/
Primary instruction set for marketing asset creation across all channels. Covers brand voice, strategic goals, target audiences, channel-specific guardrails (LinkedIn founder, LinkedIn company, newsletter, blog, webinars), quality standards, and the 6-pillar messaging framework. Companion files add asset structures and review checklists.

### content-creation/
Practical execution layer for content work. Covers how to read an incoming brief, drafting principles, format rules by channel, bilingual content rules (DE/EN), repurposing logic, and pre-delivery review. Use alongside `marketing/SKILL.md`.

### linkedin/
Dedicated guardrail for Rosa's personal LinkedIn profile. Covers founder voice, six content themes, what the profile is and is not for, post structure guidelines, tone calibration, and output format for post requests. Distinct from the company page guardrail in marketing.

### sales/
Governs B2B2C sales communication and partner outreach. Covers the employer value proposition (wellbeing, equity, retention), audience-specific messaging for HR leads, DEI leads, and C-suite, core messaging framework, objection handling, approved claims, and what to avoid. Consultative and mission-aligned by default.

### finance/
Governs all finance-related outputs with a strict source hierarchy (live facts → financial model → investor docs → legal docs → grant docs → legacy). Contains current live finance facts (60k EUR secured, 12.5k EUR cash, founder-owned, license costs covered by revenue, no salaries paid). Companion files provide QA checklists and reusable response templates. Critical: always check the live finance facts block before any finance output.

### user-tests/
Governs user testing assets for familymind's product research. Covers test planning, moderation, participant recruitment, synthesis, and readout. Includes a DECISION_RULES.md that defines confidence thresholds and familymind-specific escalation rules. All test assets should be decision-oriented, not documentation-oriented.

### competitive-intelligence/
Governs competitor research and landscape analysis. Covers the five competitor buckets (family organizers, AI productivity, parenting apps, B2B2C employer tools, emerging AI family assistants), a tiered source hierarchy (Competitors.xlsx → direct product observation → press → user reviews → analyst reports), a structured research protocol, familymind's four core differentiation anchors, and output rules for profiles, landscape summaries, messaging checks, and feature comparisons.

### product/
Governs AI agent behavior for product-related tasks. Covers the human coach framework (4-stage arc: Baseline & Clarity → Toolbox → Implementation → Family Vision), the full Proactive Agent design (input sources, trigger scenarios, decision logic, outputs, goals, metrics), the 14-day onboarding journey (day-by-day prompts and Smart Actions for Weeks 1 and 2), phase-based product evolution (newborn through growing kids 9+), always-on features (emotion slider, chaos mode, celebration layer), and key product concepts including famory (family memory).

---

## Quick reference: which files to load

| Task | Files to load |
|------|--------------|
| Any external-facing copy | `brand/BRAND_CONTEXT.md` + domain skill |
| LinkedIn founder posts (Rosa) | `brand/BRAND_CONTEXT.md` + `linkedin/SKILL.md` |
| LinkedIn company page posts | `brand/BRAND_CONTEXT.md` + `marketing/SKILL.md` |
| Newsletter | `brand/BRAND_CONTEXT.md` + `marketing/SKILL.md` + `marketing/ASSET_TEMPLATES.md` |
| Blog post | `brand/BRAND_CONTEXT.md` + `marketing/SKILL.md` + `marketing/ASSET_TEMPLATES.md` |
| Landing page | `brand/BRAND_CONTEXT.md` + `marketing/SKILL.md` + `marketing/ASSET_TEMPLATES.md` |
| Content drafting or repurposing | `brand/BRAND_CONTEXT.md` + `content-creation/SKILL.md` + `marketing/SKILL.md` |
| Content review or scoring | `marketing/REVIEW_CHECKLISTS.md` + `marketing/SKILL.md` |
| B2B2C sales outreach | `brand/BRAND_CONTEXT.md` + `sales/SKILL.md` |
| Investor or finance communication | `finance/SKILL.md` (contains live facts) |
| Finance output review | `finance/REVIEW_CHECKLISTS.md` |
| Grant application finance section | `finance/SKILL.md` + `finance/ASSET_TEMPLATES.md` |
| User test plan or moderator guide | `user-tests/SKILL.md` + `user-tests/ASSET_TEMPLATES.md` |
| User test readout | `user-tests/SKILL.md` + `user-tests/REVIEW_CHECKLISTS.md` |
| Test finding → product decision | `user-tests/DECISION_RULES.md` |
| Competitor profile or research | `competitive-intelligence/SKILL.md` |
| Competitive landscape for investors | `brand/BRAND_CONTEXT.md` + `competitive-intelligence/SKILL.md` |
| Messaging differentiation check | `brand/BRAND_CONTEXT.md` + `competitive-intelligence/SKILL.md` |
| Product documentation or feature briefs | `brand/BRAND_CONTEXT.md` + `product/SKILL.md` |
| Proactive Agent behavior design | `product/SKILL.md` |
| Onboarding journey content | `product/SKILL.md` |

---

## Writing and editing files in this repo

AI agents are permitted to read and write to this repository. When updating or adding files:
- keep all content grounded in actual familymind context, not generic templates
- do not introduce new positioning or brand language without explicit instruction from Rosa
- flag any inconsistency between files rather than silently resolving it
- new skill files should follow the same structure as existing SKILL.md files
- update this README when the folder structure changes
- the live finance facts in `finance/SKILL.md` must be updated whenever Rosa provides new financial information
