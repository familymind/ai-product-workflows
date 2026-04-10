# SKILL.md — familymind Product

## Purpose

This skill governs AI agent behavior for all product-related tasks at familymind.

It ensures that product outputs — specs, feature briefs, onboarding designs, AI behavior descriptions, and documentation — are grounded in the actual product vision, the human coach framework that underpins the AI design, and the current product reality as of April 2026.

---

## Scope

Use this skill for:
- feature briefs and product requirement documents
- AI agent behavior design and proactive suggestion logic
- onboarding journey design and content
- user story templates
- feedback analysis and clustering
- roadmap communication
- beta user onboarding documentation
- product decision support using user research findings

Do not use this skill for: marketing copy (use `marketing/SKILL.md`), user test asset creation (use `user-tests/SKILL.md`), or investor-facing product narratives (use `finance/SKILL.md` + `brand/BRAND_CONTEXT.md`).

---

## Core product identity

familymind is not a task manager. It is a coordination and care work system for families.

The product is designed for two adults managing a household together. Every feature should be evaluated against three questions:

1. Does this reduce mental load?
2. Does this support shared responsibility between partners?
3. Does this feel trustworthy and simple to use in a busy family context?

If a feature only works for the primary user and does not change the distribution of coordination work, it does not advance the core product mission.

---

## The human coach framework

familymind's AI is designed to mirror what a skilled human family coach would do. This is the conceptual backbone of the product. Every AI interaction, suggestion, and intervention should map to one of these four stages:

### Stage 1 — Baseline & Clarity
Help the family understand where their stress, friction, and time loss actually comes from.
- Family analysis of stress sources
- Making mental load visible through shared task lists
- Identifying family priorities
- Individual stress and mental health assessment

### Stage 2 — Toolbox
Equip the family with practical tools and methods they can use immediately.
- Time management methods and routines
- Fair task distribution and role assignments
- Communication strategies for family check-ins
- Healthy routines for nutrition, exercise, and sleep

### Stage 3 — Implementation & Practice
Support actual habit formation in daily life, not just planning.
- Weekly mini-experiments with new tools and rituals
- Digital aids for organization and automation
- Contingency plans for unexpected events (sick child, late meeting, school call)

### Stage 4 — Family Vision
Help the family define and work toward a shared long-term goal.
- Defining long-term family goals
- Balancing work, family, and personal time
- Reviewing and celebrating successes
- Strengthening individual self-efficacy

The AI should meet families where they are in this arc. Do not push Stage 4 content at a family stuck in Stage 1 problems.

---

## Proactive Agent design

The Proactive Agent is the core AI system in familymind. It monitors context continuously and generates timely, relevant suggestions without the user having to ask.

### Input sources

The agent draws from the following context data:
- Recent chat messages from the user and other family members
- Emotional state of each family member (via emotion slider and reported feelings)
- Voice input
- Recent activity and completed task history
- Family memory and stored information
- Calendar events and tasks due today
- Environmental data: location, time, date, weather
- Bio data from smart watches and cycle trackers (where connected)
- Relationship dynamics between family members
- Socratic dialog history (prior conversations that reveal preferences and patterns)

### Abilities

The agent can:
- Manage calendar events (add, update)
- Manage tasks (create, update, complete, delegate)
- Search the web for relevant information
- Manage family information and profiles
- Invite or notify family members

### Smart actions the agent can take

- Add or update events and tasks
- Create new conversation threads
- Add shared lists
- Add or update family information
- Invite family members to shared items
- Send proactive suggestions to the user or their partner

### Trigger scenarios

The agent should be especially proactive in these situations:

| Trigger | What the agent should do |
|---------|--------------------------|
| Child is sick | Surface emergency childcare options, notify partner, reschedule conflicting commitments |
| Daycare or school closed | Alert both partners, suggest coverage plan |
| Doctor or therapy appointment | Remind in advance, add preparation tasks, follow up after |
| One partner's emotion slider set to "dead" or extreme stress | Generate a workload-sharing suggestion for the partner, offer emotional support content |
| One partner reporting the other is doing everything | Surface a task redistribution prompt |
| Family relocating | Generate a comprehensive moving checklist and timeline |
| Seasonal events | Proactively surface relevant planning (Christmas gifts, school year start, summer childcare) |
| Weekly recurring tasks | Remind at consistent intervals for meals, groceries, laundry, trash |
| Overlapping appointments | Alert both partners and suggest resolution |
| Task cascades (a task creates related tasks) | Surface the related tasks before the user has to think of them |
| Caregiver change | Notify affected family members and update the schedule |

### Decision logic

Before generating a suggestion, the agent checks:
1. Is something blocking this task or event from being completed?
2. Does this need preparation in advance?
3. Are there overlapping events that need resolution?
4. Are there related tasks or events that should be surfaced together?

If yes to any of these → generate a proactive suggestion. Direct to user or partner depending on context.

### Possible outputs

- Generated planning ideas
- Emotional support messages
- Task redistribution prompts ("You've taken on everything this week — should we shift some of this?")
- Bonding suggestions
- Follow-up reminders
- Task completion confirmations
- Feedback requests on completed tasks
- Autofinish suggestions for recurring patterns
- Related task additions
- Prioritization recommendations

### Agent goals

- Increase retention in the first 2 weeks by making value visible immediately
- Make proactive AI the central reason to return to the app
- Serve the family goal: lift the load

### Agent success metrics

- Usage rate of AI features
- Acceptance rate of AI suggestions
- Task completion rate after AI suggestion
- Feeling rate improvement over time (emotion slider trend)
- Family knowledge completion rate (how fully the AI understands the family context)

---

## 14-day onboarding journey

The first two weeks are the critical window for habit formation and value demonstration. The onboarding is structured as a guided journey — one prompt per day with a specific Smart Action.

### Week 1 — Quick Wins & Clarity

**Day 1 — What makes you stressed**
Prompt: "Every family has that one thing that feels heavier than the rest. Is it mornings, mealtimes, or juggling work and home? Let's name it so we can start lightening the load together."
Smart Action: Identify your biggest stress factor

**Day 2 — Your daily rhythm**
Prompt: "Where does the day slip away — mornings, after-school chaos, or evenings? Let's spot the toughest moments."
Smart Action: Find the moments that drain the most energy

**Day 3 — Invisible work**
Prompt: "A lot of family work goes unseen: booking doctor's visits, packing snacks, remembering birthdays. Let's make that work visible so it doesn't sit on just one set of shoulders."
Smart Action: Share what you do without anyone asking

**Day 4 — Meals**
Prompt: "Planning, shopping, cooking, cleaning — it's a cycle that never ends. Which part of mealtimes feels like the biggest headache for you?"
Smart Action: Choose one mealtime routine you'd like to simplify

**Day 5 — The unexpected**
Prompt: "A sick child, a late meeting, a sudden school call — it happens. Instead of stress, let's build a simple backup plan so you always know who can step in."
Smart Action: Create an emergency plan

**Day 6 — Communication**
Prompt: "Family plans often get lost in WhatsApp chats or fridge notes. Let's find a smoother way to keep everyone in sync without the scramble."
Smart Action: Create a better way of communicating

**Day 7 — You**
Prompt: "You can't pour from an empty cup. Even 10 minutes just for yourself can change the tone of the whole day. Let's carve out a little breathing space."
Smart Action: Schedule one short break for yourself this week

### Week 2 — Balance, Bonding & Vision

**Day 8 — Your family blueprint**
Prompt: "The way we were raised shapes how we parent and manage today. Were chores shared in your childhood? Was one parent the planner? Let's reflect on how that influences your current family rhythm."
Smart Action: Tell me what shapes you

**Day 9 — Chores**
Prompt: "Laundry, dishes, tidying — it piles up. Let's see how to share them more fairly without the stress."
Smart Action: Pick one chore to delegate, rotate, or drop

**Day 10 — Admin load**
Prompt: "Bills, school apps, forms — it's a lot. Let's make it easier to handle."
Smart Action: Set up a weekly family admin hour

**Day 11 — Joy**
Prompt: "Between work and chores, joy can slip away. Let's protect time for fun that fuels connection."
Smart Action: Plan one small family ritual this week

**Day 12 — Sleep and energy**
Prompt: "Late nights and chaotic mornings drain families fast. Let's see where you could smooth things out."
Smart Action: Identify one small change to improve rest

**Day 13 — Personality**
Prompt: "Some of us thrive with structure, others prefer flexibility. Some need details, others focus on the big picture. Let's explore your personality type — and your partner's — to see how it plays into family life."
Smart Action: Identify your personality style

**Day 14 — Bigger picture**
Prompt: "Over these two weeks, you've uncovered what weighs on you — and what matters most. Now let's set a shared vision for your family."
Smart Action: Set your goal for what you want to achieve this year

---

## Phase-based product evolution

familymind is designed to remain relevant across the full arc of family life. Features should be considered in terms of which phase they serve:

- **Newborn phase** — emergency coordination, sleep tracking, handover logistics, parental leave support
- **Baby/toddler phase** — daycare logistics, meal planning, short-burst coordination
- **Kindergarten phase** — school-adjacent coordination, activity tracking, routine building (this is the current primary target)
- **Primary school phase** — homework coordination, extracurricular management, growing child autonomy
- **Growing kids 9+** — family goal setting, teen-adapted communication, parents reclaiming personal time

Features built for kindergarten-phase families are the current priority. New feature ideas should always be tagged with which phase they primarily serve.

---

## Always-on features

Regardless of phase, certain features should always be present and always feel useful:

- Emotional check-ins (emotion slider)
- Smart suggestions (proactive agent)
- Family feed (shared activity view)
- Chaos mode (emergency coordination UI)
- Celebration layer (acknowledging small wins)
- One-hand quick log (fast capture under pressure)

---

## Key product concepts

**famory** — family memory. The AI's accumulated knowledge about the family's preferences, routines, patterns, and history. The more the family uses familymind, the more the AI understands them. famory is what makes the AI feel personal rather than generic. Never expose raw famory data to users in ways that feel surveillance-like.

**Mental load visibility** — a core design principle. Any feature that makes previously invisible work visible to both partners is advancing the product mission. The standard planning app only helps the person who already knows what needs to be done. familymind transfers awareness itself.

**Shared design** — familymind is not a personal assistant that a family happens to share. It is a household-level system. Design decisions that only serve the primary user without improving shared awareness or task distribution are deprioritizing the core value.

---

## Quality standard for product outputs

Every product document should be:
- specific enough to implement without ambiguity
- user-centered — grounded in the experience of dual-career families with young children
- explicit about which phase and which user type it serves
- connected to a decision or a product question that needed answering
- free of generic startup product language
