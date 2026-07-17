---
name: scan-calendar
description: Scan the calendar for meetings that don't yet have a note and create and prep them, with attendees, organizations, and relevant projects linked, and a written Context briefing. Catches meetings added after the overnight Night Shift ran. Manually invoked. Optional date or range argument (defaults to today).
argument-hint: "[YYYY-MM-DD | today | this-week]"
---

# Scan Calendar: Create and Prep Missing Meeting Notes

You find calendar meetings that have no note yet and create prepped Event notes for them. Same engine as the Night Shift's meeting step, run on demand. Read `CLAUDE.md` (Date Discipline). Idempotent: never create a duplicate.

## Step 1. Range

Default to today. If `$ARGUMENTS` is a date, use it; `this-week` = today through Sunday. Compute dates with `date`, not memory. Calendar events on a future date are SCHEDULED, never "occurred": prep them as plans, do not log interactions or set `last_met`.

## Step 2. Pull events

List calendar events for the range. Keep real meetings: has attendees, not an all-day blocker or personal hold.

## Step 3. Skip what exists

For each event, build the title `YYYY-MM-DD <Event Title>` and search the vault. If a matching note exists, skip it. Only create the missing ones.

## Step 4. Create and prep each missing meeting

Create an Event note from `Templates/Event.md`. Frontmatter:

- `type: Event`, `date: <event date>`, `source: agent`
- The typed relations: `people:` = each attendee resolved to their `[[Person]]` note, `organizations:` = their `[[Organization]]`, `projects:` = any clearly relevant `[[Project]]`. If an attendee has no Person note, add them as plain text and note it.

**Headings are H2, never H1.** The filename is the title, so do not add a title heading; the body starts at `## Context`.

Write Context **short and tight**: one or two sentences of state-of-play (where things stand and the one thing you are walking in to do), then up to three one-line objectives. Hard cap ~60 words of prose. Cut anything the reader already knows: no people profiles, no background recap. Leave Notes and Transcript empty.

## Step 5. Report

List the meetings created with their prep highlights, and any attendees with no Person note (candidates for a new record). Do not commit unless asked. This is an interactive skill; leave the new notes for review.
