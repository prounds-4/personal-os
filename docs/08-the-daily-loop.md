# The daily loop

Four moving parts. Two run on a schedule, two you invoke. You touch none of the plumbing.

```
  pre-dawn          during the day           evening              Sunday
  ────────          ──────────────           ───────              ──────
  Night Shift  →    meetings land as    →    end-day        →     Weekly Review
                    linked notes
  prep meetings     (the links are the       recap the day        close the week
  enrich entities    fuel for tonight's      update records       report vs. targets
  write the brief    enrichment)             commit + push        prep next template
  refresh memory
```

## Night Shift (scheduled, weekday pre-dawn)

Runs before you wake so the output is waiting. Steps, in order, committing after each:

1. **Prep today's meetings.** Pull the calendar. For each real meeting, create an Event note from the template with attendees resolved to `[[Person]]` links, their `[[Organization]]`, and any relevant `[[Project]]`. Idempotent: skip anything that already exists. Write a tight Context section, one or two sentences of state-of-play plus a few objectives. Cut anything the reader already knows.
2. **Enrich.** Derive the worklist from ground truth: `git diff` since the last run, plus the typed links on yesterday's meetings, plus people and orgs from yesterday's substantive email. Reconcile each touched record. Cap the run so a bad night cannot rewrite the whole vault.
3. **Write the morning brief** into today's daily note. Hard caps: two sections (Yesterday, at most two bullets of what materially happened; Today, one line per meeting plus what actually matters), ~100 words total. Density over length.
4. **Regenerate agent memory.** Rebuild the "what's going on" file that every session reads: active work, who's hot, recent shifts. Overwrite whole.

The caps are the point. An unconstrained brief becomes a wall of text you stop reading in a week, and then the whole system is theater.

## During the day

Nothing to do. Meetings land as notes linked to the people, organizations, and projects they touch. Those links are what tonight's enrichment runs on. The only discipline required is linking, and the templates do most of that for you.

## end-day (manual, evening)

The close-out ritual, and the highest-value habit in the system. It exists so the overnight run starts from a closed-out day.

1. **Gather the day** from every source: mail (sent and received, where much of the real work lives), meetings, `git diff`, tasks.
2. **Verify what actually happened.** A meeting note existing is not proof the meeting occurred. An empty note is a no-show. Do not log interactions for meetings that did not happen.
3. **Pull meeting content** from your notetaker, cleaned to your style rules, verbatim where possible. Render only *your* action items; other attendees' commitments must never end up in your queue.
4. **Update records** for everyone touched by meeting or email, reconciled, not appended.
5. **Fill the day's trackers** by asking, not guessing. Never overwrite a cell the human already filled.
6. **Write the recap** into the daily note: what got done, what's carrying to tomorrow. Same caps as the brief.
7. **Commit and push.** This is what lets tonight's Night Shift pull a closed-out day.

## Weekly Review (scheduled, Sunday pre-dawn)

Sunday is still inside the ending ISO week, so the math closes the current week and preps the next one. It must run Sunday, never Monday.

The model it operates inside: **you run yourself like a corporation. You set the strategy; the agent is the back office.** It has exactly two jobs:

1. **Report progress** against quarterly and annual targets. Reporting is the part humans find hard and the part a back office is for. It produces the management report; it does not edit the goals.
2. **Prep next week's template** so you draft into a clean page. It fills the calendar section. It leaves the plan blank, because that is yours to write.

It does not set strategy, write your plan, invent tasks, or author framing. It surfaces facts and leaves the thinking to you.

The report is tiered so it stays readable: the two or three goals that are the year's real arc get reported every week even when the line is "holding." Everything else is reported by exception, only when it moved or is drifting. Once a month, drop the filter and sweep everything so nothing hides.

## Why the loop closes

Each part feeds the next. end-day commits a closed-out day, so Night Shift enriches from real ground truth, so the brief is accurate, so you trust it enough to run end-day again. Break one link and the whole thing degrades into notes nobody reads.

The loop is the product. The individual prompts are just how it is spelled.
