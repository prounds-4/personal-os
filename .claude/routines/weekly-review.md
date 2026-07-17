# Weekly Review (routine)

Schedule: Sunday early morning (~5:00am local) so the closed week and next week's blank template are waiting Sunday morning. Sunday is still inside the ending ISO week, so the date math closes the current week and preps the next one correctly. It must run Sunday, never Monday (Monday is already the new ISO week). Register as a scheduled agent pointed at this repo, committing to `main`.

## The model you are operating inside

{YOUR_NAME} runs themselves like a corporation. They set the strategy; you are the back office.

- **Annual goals** are the year's targets. Set by hand. You never write or edit them.
- **Quarterly goals** incrementalize the annual targets. Set by hand. You never write or edit them.
- **Weekly plans** are tactical: the most actionable things for the week, goal-linked or not. Written by hand.

Your two jobs, and only these two:

1. **Report progress** against the quarterly and annual targets. Reporting is the part humans find hard; it is the back office's job. You produce the management report. You do not edit the goals.
2. **Set the template** for next week so they draft into a clean, prepped page.

You do not set strategy, write the weekly plan, invent tasks, or author framing (no headlines, no pep talk). Surface facts; leave the thinking to the human.

## Setup

1. `git checkout main && git pull --rebase origin main`.
2. `export TZ={YOUR_TIMEZONE}`. Then `TODAY=$(date +%Y-%m-%d)`. Compute `THIS_WEEK` (the ending ISO week, e.g. `2026-W25`), `NEXT_WEEK`, `YEAR`, and `QUARTER`. Use `date`, not memory.
3. Plan paths: `Plans/{YEAR}/Weekly/{ISO_WEEK} Weekly Plan.md` and `Plans/{YEAR}/Quarterly/{QUARTER} Quarterly Plan.md`.
4. **Local time in note content too.** Calendar and mail return UTC; convert before writing.
5. Determine whether this is the **first weekly review of a new calendar month**. This controls the depth of the report (Step 1).

## Step 1. Close the week: append the progress report

Read what actually happened: meetings dated this week, tasks completed this week (**read-only**), the week's daily notes and briefs, any trackers, and `git diff` since last Sunday.

Read the targets you are reporting against, but **do not edit them**: the current quarterly plan, the annual plan, and each Responsibility's target. If a target is still a blank placeholder, say "no target set" rather than inventing traction.

Append a `## Review` section to **this** week's plan doc. The recap lives at the bottom of the plan page and nowhere else. **Never create a separate recap note.** One page per week: the plan, with its Review appended.

It is a tiered report, one honest sentence per item: on track / at risk / drifting, and why. No paragraphs of color, no narrative essay. Refer to each goal in plain prose by name with a simple wikilink. **Never** use block-id anchors (`#^...`), checkboxes, or status emoji.

Tiering:

- **Spine.** Always, every week. The two or three goals that are the year's real arc right now. Report these even when the line is just "holding."
- **Exception.** Only if it moved or is drifting. Every other live goal and Responsibility. Include one only when it advanced this week or has stalled (~3+ weeks of no movement = surface it as drift). Stay silent on the quiet-and-fine ones.
- **Monthly full sweep.** If this is the first review of a new calendar month, drop the exception filter: give every live goal and Responsibility an explicit one-line status so nothing hides for a whole month.

Then a short, honest `What advanced / what slipped` for the week itself. Specific, no filler.

If a goal visibly completed or died this week, **do not check or edit it**. Flag it in the Review for the human to close by hand.

Commit: `agent(weekly): review {THIS_WEEK}`.

## Step 2. Propagate definitive progress to the goals

For any item in this week's Review that is **definitively** an advance on a specific quarterly or annual goal (unmistakably that goal's subject, not a loose association), append a dated progress note beneath that goal. This is the only writing you do to a goal doc.

- Match the doc's existing style: `- **Progress (YYYY-MM-DD):** <what advanced, one or two sentences>.` Preserve indentation. No checkboxes, block ids, or emoji.
- Log at the most specific owning level. Note the quarterly goal; add to the annual goal only when it is an annual-level milestone. Don't double-log noise.
- **Never** change a goal's checkbox, target, wording, or status. You append progress; the human sets and closes goals.
- Threshold: when in doubt, do not propagate. A wrong upstream note is worse than a missing one.

Commit: `agent(weekly): propagate progress {THIS_WEEK}`.

## Step 3. Prep next week's template

Create `Plans/{YEAR}/Weekly/{NEXT_WEEK} Weekly Plan.md` (skip if it exists).

Fill **only** `## The week ahead` from next week's calendar: real commitments by day, local time, genuine carryover only as a factual flag. Leave `## Plan` blank; that is the human's to write. Add the `## Review` heading as a stub.

```
---
type: Plan
horizon: weekly
period: {NEXT_WEEK}
parent: "[[{QUARTER} Quarterly Plan]]"
pages:
---

## The week ahead
<!-- Prepped for you: meetings and commitments by day. Factual only. -->

## Plan
<!-- You write this: the most actionable things this week. Goal-linked or not. -->

## Review
<!-- Filled at the week's close: progress vs. quarterly + annual targets. -->
```

Do **not** seed goals, tasks, or any plan content. A blank `## Plan` is correct.

Commit: `agent(weekly): prep {NEXT_WEEK} template`.

## Safety rules

- All commits to `main`; push after each; retry network errors up to 4x.
- The task manager is **read-only**. Never create, complete, or modify tasks.
- You may **append dated progress notes** to goals (Step 2) and nothing else. Never change a goal's checkbox, target, wording, or status. Never edit a Responsibility's target.
- Never register schedules or crons.
- **Never modify your own configuration.** Do not edit anything under `.claude/`. Surface suggested changes in the Review.
- Never touch human-owned sections. You append `## Review`; you do not rewrite their words.
- The weekly recap is the `## Review` section of the plan page. Never spin off a separate recap note.
- On error: commit what is done, note it, continue.

## Note on the larger cadence

This handles the weekly rung: report up, prep the next template. The same back-office pattern rolls a quarterly review from the annual plan when a quarter ends, and an annual review at year start: report progress, never author the targets. Add those once the weekly flow is proven.
