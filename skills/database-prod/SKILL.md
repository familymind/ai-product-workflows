---
name: database-prod
description: >-
  Reference for the production Postgres database at familymind. Use this skill to understand the schema, table relations, and naming conventions.
---

# Production Postgres (direct-query) — deep reference

familymind's production AWS Postgres (schema `core`) is connected to PostHog as a **direct-query**
source: queries run **live against production**, in **native PostgreSQL**, isolated from the
ClickHouse event store. This is the authoritative store for "how many" and "current state."

## Connect

`execute-sql` with the connection id set:

```
call execute-sql {
  "query": "SELECT count(*) FROM chats",
  "truncate": true,
  "connectionId": "019f221b-fa6b-0000-9acb-63d6c33592dc"
}
```

Cached id above. If it errors as unknown (source recreated), rediscover: `external-data-sources-list {}`
-> take `id` where `prefix = "Production Database"` and `source_type = Postgres`. Reference tables
by bare name (`chats`, not `core.chats`).

## Syntax rules (verified, these bite)

- **Native PostgreSQL, not HogQL.** `count(*)` works, `count()` fails. Use `NOW()`, `::date`,
  `ILIKE`, `->>` / `->` for JSON.
- **`FILTER (WHERE ...)` is silently dropped.** It does not error; it returns the *unfiltered*
  count for each column (verified: a member split returned 2376/2376/2376 instead of 1223/1153).
  Always use `sum(CASE WHEN cond THEN 1 ELSE 0 END)`. If every branch equals the total, suspect a
  dropped construct and re-express with CASE.
- **Live production load.** Aggregate in SQL, bound the large tables (`activities`, `events`,
  `chat_messages`) by a timestamp, avoid `SELECT *` dumps.

## Privacy and safety (hard rules)

- Read-only connection (`read_only_user`). Never attempt or suggest writes through it.
- **NEVER select `users.password`** — bcrypt hashes, still reachable as of last check. No
  analytics reason to touch it.
- **Do not query** `member_auth_*`, `member_email_verification_tokens`,
  `member_integration_apple_tokens`, `member_integration_google_tokens`, `integration_ics_tokens`,
  `memories`. Secrets, excluded from sync.
- Prefer counts/aggregates. When inspecting rows, select only needed columns; never dump names,
  emails, or free text into output.

## Core data model

- **`families`** = tenant. Almost everything joins on `family_id`.
- **`members`** = people on a family roster.
- **`users`** = authenticated accounts (email/password or Apple/Google).

Member vs user is the distinction that matters most:

- `members.user_id IS NOT NULL` -> signed-up; join `members.user_id = users.id`.
- `members.user_id IS NULL` (usually `status = 'PENDING'`) -> **added to a family but never
  created an account**. This is the "never joined" cohort.

Count real accounts via `users`; count roster people via `members`; measure invite->signup by
comparing members with a non-null `user_id` to the total.

## Key table relations (navigation map)

```
families (id)
  ├─< members (family_id)            members.user_id ─> users (id)         [nullable = not signed up]
  ├─< chats (family_id)              chats.created_by ─> members (id); chats.skill_key = AI skill
  │     └─< chat_messages (chat_id)  chat_messages.sender_id ─> members (id); sender_role = USER|assistant
  ├─< task_lists (family_id)
  │     └─< tasks (task_list_id)     tasks.family_id; assigned_to/assigned_by/completed_by ─> members (id)
  │                                  tasks.sub_task_of_id ─> tasks (id)
  ├─< events (family_id)             calendar; events.recurrence_id ─> recurrences (id)
  ├─< family_knowledge (family_id)   family_knowledge.chat_id ─> chats (id)
  ├─< subscription_records (family_id)  subscription_records.member_id ─> members (id)
  └─< activities (family_id)         activities.member_id ─> members (id); entity_id ─> polymorphic by entity_type
```

`created_by` / `updated_by` reference `members.id`, except the system actor
`00000000-0000-0000-0000-000000000001` (exclude when measuring human behaviour).

## activities vs events (do not confuse)

- **`activities`** = CRUD audit log. One row per create/update/delete.
  `activity_type` (`INSERT`=create, `UPDATE`, `DELETE`), `entity_type`
  (`EVENTS, CHATS, CHAT_MESSAGES, TASKS, FAMILIES, MEMBERS, FAMILY_KNOWLEDGE, TASK_LISTS,
  MEMBER_DAILY_FEELINGS, MEMBER_PREFERENCES, RECURRENCES, INTEGRATION_*, SURVEY_RESPONSES, ...`),
  `entity_id`, `family_id`, `member_id`, `session_id`, `metadata` (JSON of the change),
  `created_at`. ~100k rows and growing; always bound by `created_at`. `EVENTS`+`INSERT` dominates
  (calendar sync) — segment it out for human-behaviour analysis.
- **`events`** = the family **calendar** (`start_date_time`, `end_date_time`, `all_day`,
  `recurrence_id`, `location`, `google_calendar_item_sync_id`). Not an activity log.

## Conventions

- **Soft deletes**: some tables carry `deleted_at` (e.g. `families`). Filter `deleted_at IS NULL`
  for live records.
- **Timestamps are UTC.** Convert for local-time reporting (German base):
  `created_at AT TIME ZONE 'Europe/Berlin'`.
- **Subscriptions span three tables**: `subscription_records` (`subscription_type` e.g.
  `CREATION`; `expires_at`), plus `subscription_record_from_apps` and
  `subscription_record_from_stores`. `families.subscription_end_date` is a denormalised shortcut.
  Verify the full `subscription_type` enum before splitting paid vs trial.
- **`chats.skill_key` is NULL across current production data.** Skill identity actually lives in
  the chat `title` (with emoji, and split by language: "Ellie, the Event Elf" vs "Ellie, die
  Event-Elfe"). So "which skills are used most" cannot use `skill_key` today: either backfill and
  start populating `skill_key` (engineering), or group by a normalised `title` (strip emoji, map
  DE/EN variants to one skill). Until `skill_key` is populated, any skill-usage number needs that
  title normalisation to be correct.

## Verified columns (primary tables)

- **families**: id, name, color_code, created_at, created_by, deleted_at, updated_at, updated_by,
  family_image, is_onboarded, residence_type, place_of_living, discovery_source, subscription_end_date
- **members**: id, name, color, email, image, status, user_id, apple_id, is_admin, family_id,
  is_google, birth_date, created_at, updated_at, updated_by, is_verified, member_role,
  last_verification_email_sent
- **users**: id, email, apple_id, password (NEVER select), is_google, created_at, updated_at, is_verified
- **chats**: id, title, chat_mode, family_id, skill_key, created_at, created_by, member_ids,
  updated_at, description, last_message_at, show_description
- **chat_messages**: id, chat_id, family_id, sender_id, created_at, attachments, sender_role
  (no message body is exposed)
- **tasks**: id, family_id, task_list_id, created_by, updated_by, assigned_to, assigned_by,
  completed_by, sub_task_of_id, position, description, is_completed, due_at,
  reminder_minutes_before, recurrence_id, created_at, updated_at, assigned_at, completed_at
- **task_lists**: id, title, sort_by, family_id, created_at, created_by, updated_at, updated_by
- **events**: id, description, family_id, created_by, updated_by, member_ids, start_date_time,
  end_date_time, dt_stamp, recurrence_id, all_day, reminder_minutes_before, source,
  external_source_id, google_calendar_item_sync_id, enabled, created_at, updated_at, location,
  time_zone, url, availability, apple_mirror_event_id, external_calendar_id
- **family_knowledge**: id, family_id, subject_type, subject_key, subject_id, domain, subdomain,
  confidence, source_channel, activation_reason, is_active, superseded_by, last_observed_at,
  effective_at, expires_at, chat_id, created_by, updated_by, created_at, updated_at
- **subscription_records**: id, family_id, member_id, created_at, expires_at, subscription_type
- **activities**: id, metadata, entity_id, family_id, member_id, created_at, session_id,
  entity_type, ingested_at, activity_type, sync_to_client

Other synced tables (profile with a narrow `SELECT ... LIMIT 1` before use): family_extras,
family_iq_log, family_quest_progress, family_skills, incomplete_transactions,
integration_apple_calendar_item_syncs, integration_google_calendar_item_syncs,
integration_google_calendar_list_syncs, knowledge_jobs, member_daily_feelings, member_invitations,
member_preferences, member_referral_attempts, member_referral_codes, member_referrals,
notification_settings, promo_codes, quest_definitions, recurrences, scheduled_notifications,
sessions, signal_definitions, skill_helpers, skill_templates, subscription_record_from_apps,
subscription_record_from_stores, support_tickets, survey_responses.

## Recipes (native Postgres)

**Signed-up users vs never-joined members** (CASE, not FILTER):
```sql
SELECT
  sum(CASE WHEN user_id IS NOT NULL THEN 1 ELSE 0 END) AS members_with_account,
  sum(CASE WHEN user_id IS NULL     THEN 1 ELSE 0 END) AS members_never_joined,
  count(*)                                             AS members_total
FROM members;
```

**Per-family engagement / "how advanced is this family":**
```sql
SELECT
  f.id, f.name, f.is_onboarded,
  (SELECT count(*) FROM members m       WHERE m.family_id = f.id)                          AS members,
  (SELECT count(*) FROM chats c         WHERE c.family_id = f.id)                          AS chats,
  (SELECT count(*) FROM chat_messages x WHERE x.family_id = f.id AND x.sender_role='USER') AS user_messages,
  (SELECT count(*) FROM tasks t         WHERE t.family_id = f.id)                          AS tasks,
  (SELECT count(*) FROM events e        WHERE e.family_id = f.id)                          AS calendar_events
FROM families f
WHERE f.deleted_at IS NULL
ORDER BY user_messages DESC
LIMIT 50;
```

**Which AI skills are used most** (by chat volume). `skill_key` is null in prod, so group by
`title`; the same skill appears in DE and EN, so normalise for a clean total. Note `||` literal
concatenation fails in this engine, so keep expressions simple:
```sql
SELECT COALESCE(skill_key, title) AS skill, count(*) AS chats
FROM chats
GROUP BY skill
ORDER BY chats DESC
LIMIT 30;
```

**Families with no user message yet (the AI-discovery gap):**
```sql
SELECT count(*) AS families_no_user_message
FROM families f
WHERE f.deleted_at IS NULL
  AND NOT EXISTS (
    SELECT 1 FROM chat_messages cm
    WHERE cm.family_id = f.id AND cm.sender_role = 'USER'
  );
```

**Calendar connections** (families with at least one connected calendar). The integration tables
key on `member_id`, not `family_id`, so join through `members`:
```sql
SELECT
  (SELECT count(DISTINCT m.family_id)
     FROM integration_google_calendar_list_syncs g
     JOIN members m ON m.id = g.member_id) AS google_families,
  (SELECT count(DISTINCT m.family_id)
     FROM integration_apple_calendar_item_syncs a
     JOIN members m ON m.id = a.member_id)  AS apple_families;
```

**Human activity, last 14 days, excluding calendar-sync noise:**
```sql
SELECT entity_type, activity_type, count(*) AS n
FROM activities
WHERE created_at >= NOW() - INTERVAL '14 days'
  AND NOT (entity_type = 'EVENTS' AND activity_type = 'INSERT')
GROUP BY entity_type, activity_type
ORDER BY n DESC;
```

**Active subscriptions now:**
```sql
SELECT subscription_type, count(*) AS active
FROM subscription_records
WHERE expires_at > NOW()
GROUP BY subscription_type
ORDER BY active DESC;
```