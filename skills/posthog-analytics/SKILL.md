---
name: posthog-analytics
description: >-
  The protocol and source of truth for using PostHog at familymind. PostHog holds THREE distinct
  data domains that are constantly confused: (1) mobile product analytics from the Flutter app,
  (2) web analytics from the familymind.ai site, and (3) the production backend Postgres database
  queried live over a direct connection. Consult this skill BEFORE answering ANY PostHog question
  or writing ANY query, insight, dashboard, funnel, or SQL for familymind: DAU/MAU/retention,
  acquisition and web traffic, per-family or per-user data volumes, chats/messages/tasks/calendar
  usage, skill usage, subscriptions, activity logs, errors, or session replay. It sets
  which domain answers which question, the exact production-vs-dev and web-vs-mobile filters, the
  live-SQL connection mechanism, the schema, and the naming/governance conventions every
  contributor must follow. Use it even when the user only names one thing (a table, an event, a
  metric, a dashboard), because the first job is always routing to the right domain.
---

# familymind on PostHog: the operating protocol

PostHog is our analytics hub. It contains three separate data worlds. Ninety percent of mistakes
come from querying the wrong one or silently mixing them. Route first, then query.

## The three domains

| Domain | What it is | How it is identified | Engine / tools |
|---|---|---|---|
| **Mobile product analytics** | Behavioural events from the Flutter app | `properties.$app_namespace = 'ai.familymind'` (prod). `.dev` / `.local` are non-prod. `platform` is empty for mobile. | ClickHouse. `query-*` tools; `execute-sql` **without** `connectionId`. |
| **Web analytics** | Traffic on the familymind.ai marketing site | `properties.platform = 'web'` (no `$app_namespace`) | Web analytics product; `query-web-overview`, `query-web-stats`. |
| **Production Postgres** | Live backend state (the app's database, schema `core`) | Passed explicitly via `connectionId` | Native PostgreSQL via `execute-sql` **with** `connectionId`. |

There is no `platform = 'flutter'`. Identify mobile by `$app_namespace`, never by `platform`.

## Routing: which domain answers the question

| The question is about... | Use | Never use |
|---|---|---|
| DAU / WAU / MAU, retention, stickiness, active-user trends | Mobile product analytics (`query-trends`, `query-retention`, `query-stickiness`) | Postgres |

| Behavioural funnels (install -> signup -> onboarding -> first AI message) | Mobile product analytics (`query-funnel`) | Postgres |

| How people navigate, screen/page time, rage clicks, dead clicks, scroll, UI friction | Mobile product analytics + session replay + heatmaps | Postgres |

| Crashes, exceptions, `auth_error`, error tracking | Mobile product analytics / error tracking | Postgres |

| Website traffic, acquisition source, referrers, UTMs, top pages | Web analytics (filter `platform = 'web'`, host familymind.ai) | Mobile events |

| Per-family / per-user **data volumes**: how many chats, messages, tasks, events; how advanced a family is | **Production Postgres** | don't use product events |

| Which AI skills are used most (`skill_key`), who connected Google/Apple calendar | **Production Postgres** | product events |

| Login sessions, authoritative account/member/family counts, exact current state | **Production Postgres** | product events |

| Current subscription / premium state right now | **Production Postgres** (`subscription_records`) | product events |

| Freemium conversion **over time** (paywall views, limit reached) | Mobile product analytics, once instrumented | Postgres |

Rule of thumb: **Postgres answers "how many / what is the current state." Product analytics
answers "how / behaviour / over time." Web analytics answers "where did they come from."**

## The duplication trap (read this)

Many actions are recorded in BOTH places. `chat_created`, `task_created`,
`calendar_event_created`, `member_created`, etc. exist as product events (ClickHouse) AND as rows
in the Postgres `activities` audit log (`entity_type` + `activity_type`). They will **not** give
equal numbers: product events are subject to ad-blocking, opt-out, sampling, and the prod/dev
split, while Postgres is authoritative.

- Need the true count or per-family breakdown -> Postgres (`activities` or the entity table).
- Need behaviour over time, by cohort, with UI context, in a funnel -> product events.
- **Never reconcile the two 1:1** and never present a mixed number without saying which source.

## Non-negotiable filters and caveats

- **Production only for shared/exec analysis.** Mobile: `$app_namespace = 'ai.familymind'` and
  exclude `ai.familymind.dev` / `ai.familymind.local`. Mixing dev traffic into a KPI is a bug.
- **Exclude internal/test users** on anything shared, via the `Internal / Test users` cohort.
- **Web counts are lower bounds.** Ad blockers silently drop an estimated 10-25% of web events
  (PostHog warns about this in-app). A reverse proxy on familymind.ai is the fix. Until then,
  treat web volume as directional and do not reconcile it against backend numbers.
- **Cross-domain numbers never match exactly.** State the source on every figure.

## Working with the production Postgres database

Full schema, key-table relations, privacy rules, and query recipes are in
`database-prod.md` skill. **Read it before writing any backend SQL.** The essentials:

- Call: `execute-sql` with `"connectionId": "019f221b-fa6b-0000-9acb-63d6c33592dc"`. Without the
  id the query hits ClickHouse and cannot see these tables. If the id ever errors as unknown,
  rediscover it via `external-data-sources-list` (source with `prefix: "Production Database"`).
- It is **native PostgreSQL, not HogQL**: `count(*)` not `count()`. And the direct-query layer
  **silently drops `FILTER (WHERE ...)`** and returns wrong-but-plausible numbers, so use
  `sum(CASE WHEN ... THEN 1 ELSE 0 END)` instead.
- Read-only. Never select `users.password` (still exposes bcrypt hashes as of last check), and
  never touch the `member_auth_*` / token tables.

## Working with product and web analytics

The essentials:

- **Verify before you query.** Call `read-data-schema` to confirm an event/property/value exists;
  do not trust memory or PostHog defaults. familymind events are snake_case `verb_noun`
  (`chat_created`, `task_completed`, `onboarding_completed`, `login_completed`, `calendar_connected`).
- **Prefer typed `query-*` insights over raw SQL** so results are saveable and iterable. Reach for
  `execute-sql` (ClickHouse, no `connectionId`) only for joins/CTEs/entity search that `query-*`
  cannot express.

## Governance: keeping the hub organised

The goal is one clean, consistent analytics hub every contributor can trust. Rules:

1. **One canonical metric definition.** Each KPI (DAU, activation, retention, conversion) has one
   agreed event/filter definition. Document the filter in the insight description. Do not create a
   second "DAU" with a different filter; fix the canonical one.
2. **Insights are named and tagged.** Pattern: `[Domain] Metric — segment`, e.g.
   `[Mobile] Weekly retention — prod`. Tag by domain (`mobile`, `web`, `backend`) and add a
   one-line description stating the source and filter. An untagged, undescribed insight is debt.
3. **Dashboards are purpose-scoped, not personal.** Add insights to an existing canonical
   dashboard; do not spin up one-offs. Current canonical set:
   - `Growth & engagement overview` — WAU/DAU, installs, core actions, retention (prod/dev via
     `$app_namespace` filter).
   - `Operational Events — familymind (weekly brief companion)` — task/calendar/chat/AI volume,
     churn, deletions, auth errors (prod only).
   - `Website Acquisition (upper funnel) — familymind` — web sources, UTMs, top pages (test
     accounts excluded).
   - Retire `My App Dashboard` (the auto-created starter) once its tiles are re-homed.
4. **Every dashboard states its scope** in the description: which domain, prod vs dev, test
   exclusion. If scope is not written down, it is wrong within a week.
5. **New event? Register it consistently.** snake_case `verb_noun`, carry `$app_namespace`, and
   add it to the taxonomy note in `references/product-analytics.md` so the next contributor finds
   it.
6. **Backend vs product boundary is explicit.** If a number could come from either domain, say
   which one you used and why (see the duplication trap).

When unsure which domain a request belongs to, resolve routing first (state the domain and
filter), then query. That single habit prevents most of the mess.