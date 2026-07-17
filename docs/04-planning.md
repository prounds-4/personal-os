# The planning cadence

Run yourself like a corporation. You set the strategy; the agent is the back office.

That sentence is the whole model, and the split it implies is strict: **you author the targets, the agent reports on them.** An agent that can rewrite your goals is not an assistant.

## Two axes

Most planning systems fail because they try to make one structure do two jobs. This vault splits them.

**Plans** are time-boxed. Annual, quarterly, weekly. They have periods and they end.

**Responsibilities** are not. They are the standing areas of your life with no finish line: your career, your health, your family, your money, your home. You do not "complete" your marriage. You track how it is going.

The durable "what I'm driving toward" lives on the Responsibility. The time-boxed push lives on the Plan. Conflating them is why so many people's goal systems collapse: they write "be a better father" as a Q3 goal, fail to check it off in December, and conclude the system is broken. It wasn't a goal. It was an area.

## The chain

```
Annual Plan          the year's targets            you write these
    ↑ parent
Quarterly Plan       incrementalizes the annual    you write these
    ↑ parent
Weekly Plan          the most actionable things    you write these
```

Each plan links `parent` up the chain. That is the entire propagation mechanism.

I want to be emphatic about this because I built the alternative and it was a disaster: **no block IDs, no status emoji, no `Supports [[goal]]` tags, no checkboxes cascading up a hierarchy.** I had all of it. It was fragile, it rotted the moment I skipped a week, and maintaining the machine became a bigger job than the work it tracked. I deleted the whole thing and the system got better.

A `parent` link and plain prose does the same work and cannot break.

### Annual

`## Goals` and `## Intentions`. Goals are the year's targets. Intentions are the things that aren't targets but should shape the year anyway. Written by hand, in January, by you.

### Quarterly

Same shape, plus `parent`. Quarterly goals *incrementalize* the annual ones: they're the 90-day slice that makes the year's number reachable. Written by hand.

### Weekly

Three sections, and the ownership split is the point:

```markdown
## The week ahead
<!-- Prepped for you: meetings and commitments by day. Factual only. -->

## Plan
<!-- You write this: the most actionable things this week. Goal-linked or not. -->

## Review
<!-- Filled at the week's close: progress vs. quarterly + annual targets. -->
```

The agent fills **The week ahead** from your calendar. The agent appends **Review** at the week's close. **Plan is yours and stays blank until you write it.** A prepped page with a blank plan is the correct output of a Sunday routine; a plan the agent seeded for you is theater.

Note "goal-linked or not." Not everything worth doing this week ladders up to an annual goal, and forcing every task to justify itself against a target is how planning systems become bureaucracy.

## Responsibilities

A Responsibility carries a `metric`: the honest answer to "how do I know this is going well?"

```yaml
type: Responsibility
status: active
metric: Live, on-thesis opportunities advancing
people: ["[[Jane Doe]]"]
organizations: ["[[Acme Corp]]"]
```

Not a number necessarily. A statement of what "healthy" looks like. If the metric is still a blank placeholder, the weekly review says "no target set" rather than inventing traction, which is a small rule that prevents a large lie.

Mine are roughly: career, consulting, family, finances, health, home, and the knowledge system itself. Seven or eight is about the ceiling. If you have fifteen areas of life, you have none.

## The weekly review

Sunday, before you wake. It runs Sunday and never Monday, because Sunday is still inside the ending ISO week and the date math has to close the current week while prepping the next.

It has exactly two jobs:

1. **Report progress** against quarterly and annual targets. Reporting is the part humans hate and the part a back office exists for.
2. **Prep next week's template** so you draft into a clean page.

It does not set strategy, write your plan, invent tasks, or write you a pep talk.

### Tiering keeps it readable

An unfiltered weekly report is a wall of text you stop reading by week three, and then the whole ritual is dead.

- **Spine.** The two or three goals that are the year's real arc. Reported every week, even when the line is just "holding."
- **Exception.** Everything else, reported only when it moved or is drifting (roughly three weeks of no movement).
- **Monthly sweep.** On the first review of a calendar month, drop the filter. Every goal and Responsibility gets an explicit line so nothing hides for a whole month.

The report is one honest sentence per item: on track, at risk, or drifting, and why.

### Progress flows up, judgment doesn't

When something is *definitively* an advance on a specific goal, the agent appends a dated progress note under it:

```markdown
- **Progress (2026-07-14):** <what advanced, one or two sentences>.
```

That is the *only* thing it writes to a goal doc. It never changes a goal's target, wording, status, or checkbox. If a goal looks completed or dead, it flags it in the review and **you** close it by hand.

The threshold matters: when in doubt, don't propagate. A wrong progress note upstream is worse than a missing one, because you'll trust it later.

## One page per week

The review is a `## Review` section appended to that week's plan. Never a separate recap note.

This sounds like a formatting preference. It isn't. The moment reviews live in their own notes, the plan and its outcome drift apart and you have two half-records of the same week. One page: what you meant to do, and what happened. That's the artifact worth keeping.
