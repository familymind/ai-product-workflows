# familymind plugin

Packages familymind's `ai-product-workflows` knowledge base as auto-triggering skills for Claude Cowork and Claude Code. Once installed, the right skill loads on its own based on what you ask — no need to point at files manually.

## What's inside

Eight skills, each with a trigger-optimized description:

| Skill | Triggers on |
|-------|-------------|
| `marketing` | Company/brand marketing assets: company page, Instagram, newsletter, blog, landing pages, campaigns, messaging frameworks |
| `content-creation` | Drafting, formatting, repurposing, bilingual DE/EN execution |
| `linkedin` | Rosa's personal LinkedIn founder posts (founder-voice source of truth) |
| `sales` | B2B2C and partner outreach, pitches, objection handling, the ambassador/angel track |
| `finance` | Investor answers, fundraising, runway, cap table, grants, deck finance — source of truth for live finance facts |
| `competitive-intelligence` | Competitor profiles, landscape, differentiation checks, feature comparisons |
| `user-tests` | Test plans, moderator guides, readouts, decision rules |
| `product` | Feature briefs, AI agent behavior, onboarding design, roadmap |

## Brand context

`brand/BRAND_CONTEXT.md` (at the plugin root) is the shared source of truth for company identity, positioning, and voice. Skills instruct Claude to load it before any external-facing task.

## Single sources of truth (to avoid drift)

- **Live finance facts** — `skills/finance/SKILL.md`, Tier 0. Nothing else should restate the numbers.
- **Rosa's founder voice** — `skills/linkedin/SKILL.md`. `marketing` and `content-creation` defer to it.
- **Company identity / positioning** — `brand/BRAND_CONTEXT.md`.

## Install

In Cowork or Claude Code, install the `familymind.plugin` file. Skills then auto-trigger; reference them explicitly as `familymind:<skill>` if needed (e.g. `familymind:finance`).

## Maintenance

- Keep each `SKILL.md` `Last reviewed:` header current when you edit it.
- Update live finance facts only in `skills/finance/SKILL.md` Tier 0.
- This plugin is generated from the `ai-product-workflows` repo; keep the two in sync.
