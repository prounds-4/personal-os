---
name: end-day
description: End-of-day close-out ritual. Reviews today's email and meetings, recaps the day into the daily note, updates records for everyone touched by meeting or email, fills the day's trackers, reconciles tasks, then commits and pushes so the overnight Night Shift runs on a closed-out day. Manually invoked.
argument-hint: "[YYYY-MM-DD]"
---

# End Day: Evening Close-Out

You are {YOUR_NAME}'s assistant closing out the day: QA that nothing was dropped, talk through what happened and what remains, update records, and leave the vault committed so the Night Shift runs clean tonight. Read `CLAUDE.md` first (Style, Date Discipline). Be candid.

## Step 1. Date

`export TZ={YOUR_TIMEZONE}`, then `DATE = $ARGUMENTS or $(date +%Y-%m-%d)` (shell output, not memory). Never set `last_met` or write History entries with a date later than DATE.

**Times and dates in note content must be local.** Mail and calendar return UTC; convert before writing.

## Step 2. Gather the day

- **Email, thoroughly.** Scan today's mail, sent and received. A huge amount of real work happens over email and never touches a meeting note or a task: deliverables sent, replies that resolved something, commitments made or fulfilled, decisions, intros. Pull all of it. Flag threads still awaiting a reply. Treat email as a primary source for "what got done today."
- Today's meetings: Event notes with `date: DATE`.
- Files created or changed today: `git diff` / `git status`.
- Tasks completed today, plus open, overdue, and due tomorrow.
- Today's daily note under `Dailies/`. The Night Shift wrote the morning brief into it; your recap goes into its Evening Recap section. If missing, create it from `Templates/Daily Note.md`.

## Step 3. Verify what actually happened

A meeting note existing is not proof the meeting happened. A note with an empty body is a no-show or cancellation. Only treat a meeting as occurred if it has real content or the human confirms it. Do not log interactions or bump `last_met` for no-shows.

## Step 4. Pull meeting content

For each **confirmed** meeting dated DATE, fill its `## Transcript` or `## Summary` section from your notetaker. Idempotent: skip any note already populated so re-running is safe.

1. **Match** by date and participants, and/or title. If no confident match, leave the note and say so. Do not guess.
2. **Pull, verbatim first.** Fall back to an AI summary if verbatim is unavailable, and label it as such.
3. **Write it in**, cleaned to the style rules, preserving substance verbatim. Do not summarize, editorialize, or invent.
4. **Action items: yours only.** Notetaker summaries list action items for every attendee. Do NOT reproduce that block wholesale. Render `### My Action Items` containing ONLY items clearly assigned to {YOUR_NAME}. If none, say so. Other attendees' tasks must never appear as a checklist a later pass could misread as yours.

## Step 5. Record updates

Reconcile each touched record to the standard format (see CLAUDE.md). Fold today in; do NOT append a per-event line.

For each person and organization in today's confirmed **meetings**:

- `last_met: DATE` on each person (orgs do not carry `last_met`).
- Fold the meeting into `## History`: update the current month's `**YYYY-MM**` item with the day's substance. If History exceeds 7 items, re-distill to 5-7. Granular detail stays in the meeting note.
- **Organizations, inclusion gate:** only fold in a material org-level development. A meeting that merely referenced the org does not touch the org.

For each person or org you had a substantive **email** exchange with today:

- Fold it into the current month's `## History` item too. Email is an interaction but not a meeting: do NOT bump `last_met`.

For everyone touched:

- Update `## Overview` only on a material change. For people, refresh `## Open` to current live threads (drop resolved ones; an unanswered thread belongs here). **Organizations have no `## Open`.**
- NEVER touch `## Personal Notes`. Obey the style rules. Set `last_enriched: DATE`.

## Step 6. Tasks

- **The task manager is READ-ONLY.** Surface open action items from today's meetings and email **in the recap** for triage. Only items owned by {YOUR_NAME}; never surface other attendees' commitments. Do NOT create, complete, or modify any task.
- Report what was completed today and what is due tomorrow.

## Step 7. Trackers

If you keep daily trackers, read today's row. If it is missing or has empty cells, **ask** the questions and fill it. Fill only cells the human answers; if they decline one, leave it blank. **Never overwrite a cell that already has a value** (they may have filled it by hand). Ask compactly, in one grouped question, not one interrogation per field.

## Step 8. Write the recap

Write into today's daily note's Evening Recap section. Pull from **all** of Step 2: meetings, email, files, tasks. Not just meetings.

Keep it slim, mirroring the morning brief. Density over length. Exactly these two sections, wikilinks for every person, org, and project:

- **Done.** A handful of one-line outcomes from every source, then one honest line on how the day went. Include email-driven work; it is often half the day.
- **Carrying to tomorrow.** Open loops as one-line bullets: action items, threads awaiting a reply, tasks due tomorrow.

No third section, no per-item paragraphs. If a line restates something the human already knows, cut it.

## Step 9. Commit and push

Always: `git add -A && git commit -m "agent(end-day): close out DATE" && git push origin main`. This is what lets tonight's Night Shift pull a closed-out day. Retry a failed push up to 3x, then report.

## Step 10. Report

Brief: recap written, meeting content pulled (which, verbatim vs summary), record updates (who), tasks surfaced, tracker status, and confirm committed and pushed.
