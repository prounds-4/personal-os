# The model

The schema is the system. Everything an agent can do reliably, it can do because the graph is typed.

## Types

Every note carries a `type:` in frontmatter.

| Type | What it is | Body sections |
|---|---|---|
| **Person** | A first-class entity. Attaches to anything. | `## Overview`, `## Open`, `## History`, `## Personal Notes` (human-only) |
| **Organization** | A first-class entity. | `## Overview`, `## History` (no `## Open`) |
| **Event** | A meeting, call, or milestone. | `## Context`, `## Notes`, `## Transcript` |
| **Project** | Work with an endpoint. Carries `status`. | `## Overview`, `## History`, `## Open` (active only), `## Sub-Projects` (umbrellas only) |
| **Responsibility** | A long-running area with no finish line. | `## What I'm driving toward`, plus how it's going |
| **Plan** | A rhythm doc: annual, quarterly, or weekly. | `## The week ahead`, `## Plan`, `## Review` |
| **Topic** | A subject you hang notes off. | Free |
| **Note** | The default. Subtyped: `quote`, `journal`, `daily-log`, `essay`, `reference`. | Free |

## Typed relations, not a generic bag

Relationships are typed, directional frontmatter links:

```yaml
# On a Person
type: Person
organizations: ["[[Acme Corp]]"]      # work affiliations, current first
last_met: 2026-07-14
last_enriched: 2026-07-15

# On a Project
type: Project
responsibility: "[[Growing the business]]"
status: active
organizations: ["[[Acme Corp]]"]
people: ["[[Jane Doe]]"]
events: ["[[2026-07-14 Kickoff]]"]

# On an Event
type: Event
date: 2026-07-14
people: ["[[Jane Doe]]"]
organizations: ["[[Acme Corp]]"]
projects: ["[[Acme integration]]"]
```

Why this matters more than it looks: a generic `related:` field forces an agent to read prose and infer what a link means. Typed fields let it answer "who did I meet with yesterday, and what do I know about their company" as a graph traversal, with no interpretation and no guessing.

It also gives enrichment a worklist for free. The overnight routine does not need a queue to maintain. It reads the `people:` / `organizations:` / `projects:` links on yesterday's meeting notes, unions that with `git diff`, and that is the list. Ground truth, derived fresh every run, impossible to desynchronize.

## Section ownership

Every section is either human-owned or agent-owned, and the contract is written down.

| Section | Owner |
|---|---|
| `## Overview` | Agent. Updated only on a material change. |
| `## Open` | Agent. Refreshed to current live threads. |
| `## History` | Agent. Reconciled and re-distilled, never appended. |
| `## Personal Notes` | **Human. Never touched.** |
| A Plan's `## Plan` | **Human.** The agent appends `## Review` and nothing else. |
| Annual/quarterly goals | **Human sets and closes them.** The agent appends dated progress notes only. |

The asymmetry is deliberate. The agent owns the record-keeping; you own the judgment. An agent that could rewrite your goals is not an assistant, it is a co-author you did not hire.

## Reconciliation rules

- Fold a new interaction into the existing `## History` item for the current month. Do not add a paragraph per meeting.
- When `## History` exceeds ~7 items, re-distill the whole section to 5-7, weighted toward the recent.
- Update `## Overview` only on a material change: a new role, a new company, a change in how you know them. Routine contact does not touch it.
- **Organizations get an inclusion gate.** Before folding anything into an org's history, ask: is this a material org-level development (funding, leadership change, strategic shift, a deal)? A person's meeting that merely mentioned the org never touches the org. Without this gate, every org record fills with noise.
- `last_met` moves only for an actual meeting. Email is an interaction but not a meeting.

## Plans

Plans are written rhythm documents linked `parent` up the chain: Weekly → Quarterly → Annual.

The durable "what I'm driving toward" lives on Responsibilities. The doing lives in your task manager. The plan docs are where you think, and where the agent reports back.

Resist the urge to build a goal-propagation machine with block IDs and status emoji. I built one. It was fragile, it rotted, and I deleted it. Plain prose and a `parent` link is enough.
