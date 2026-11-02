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

# PostHog analytics

The working details for this skill are kept in the private `business-intelligence` project, in `.claude/skills/posthog-analytics/SKILL.md`. Read them there, and never copy them into this project.

Always read-only, aggregates only, no personal data and no credentials.
