# The personal CRM

Run your network like a CRM. Not because relationships are transactions, but because your memory of them is worse than you think, and a system that remembers for you makes you a better friend, not a colder one.

This is the part of the vault that pays for itself fastest.

## The premise

You meet hundreds of people. You remember the last conversation with maybe twenty of them. The rest decay into "we talked about something, a while back," which is exactly the state that makes you hedge, re-ask questions you already asked, and miss the follow-up you promised.

Salespeople solved this thirty years ago and everyone else decided it was beneath them. It isn't. The difference is that a sales CRM exists to extract; yours exists to show up prepared.

## Three record types, one job each

**Person.** The entity everything else attaches to. Frontmatter carries the facts (`role`, `organizations`, `location`, `linkedin`, `first_met`, `last_met`, `last_enriched`). The body carries the relationship:

- `## Overview`. Who they are and how you know them. Changes rarely. A new job changes it; a coffee does not.
- `## Open`. Live threads and the next move. This is the section you read before a call.
- `## History`. The distilled arc, not a transcript.
- `## Personal Notes`. Yours. The agent never touches it. This is where the human observations live: what they care about, what they're worried about, the thing you'd never let a machine write.

**Organization.** Same idea, fewer sections: `## Overview` and `## History` only. **No `## Open`.** Live threads belong to a person or a project, never to a company. An org record with an Open section becomes a junk drawer.

**Event.** A meeting, call, or milestone. This is the atom of the whole system, and the reason the CRM stays current without effort.

## Meetings are the fuel

Here is the mechanism that makes the CRM self-maintaining, and it is the single best idea in the vault.

Every meeting becomes an Event note, titled `YYYY-MM-DD <Title>`, with typed links to the people, organizations, and projects it touched:

```yaml
type: Event
date: 2026-07-14
people: ["[[Jane Doe]]", "[[Sam Roe]]"]
organizations: ["[[Acme Corp]]"]
projects: ["[[Acme integration]]"]
```

Those links are not decoration. They are the **worklist**. Tonight's enrichment run reads the links on today's meetings and knows exactly which records to update. No queue to maintain, no "mark for review" checkbox, nothing to fall out of sync. The act of recording a meeting *is* the act of scheduling the CRM update.

That is why the schema matters more than the prose. Link the meeting properly and the system maintains itself. Skip the links and it goes blind.

## The inclusion gate

Without a filter, every org record fills with noise until nobody reads it.

Before folding anything into an organization's history, ask: **is this a material org-level development?** Funding, a leadership change, a strategic shift, a deal, a change in your relationship with them. A meeting with someone who merely mentioned their employer is not an org development. It stays on the person and the meeting note.

Same instinct, different rule, for people: `## Overview` changes only on a material change. Routine contact never touches it.

The gate is what keeps a five-year-old record readable.

## Reconcile, never append

The naive design appends a line per interaction. Do that for a year and every record is a changelog with no readers.

Instead: fold today into the current month's history item. When history passes about seven items, re-distill the whole section back to five or seven, weighted toward the recent. The granular detail already lives in the meeting note; it does not get copied up.

A person's record should read like a portrait, not a ledger.

## last_met earns its precision

`last_met` moves only for an actual meeting. Email is an interaction, but it is not a meeting, and conflating them destroys the one query that matters: *who have I lost touch with?*

Sort your people by `last_met` and you have a reconnect list that is honest. Let email bump it and you get a list that says you're close with everyone you've ever cc'd.

A meeting note existing is also not proof a meeting happened. An empty note is a no-show. The close-out ritual verifies before it logs, because a CRM that records meetings that never occurred is worse than no CRM.

## What this buys you

Before any call, the agent can answer: who is this, how do I know them, what's open, when did we last talk, what did we say. That briefing used to cost you fifteen minutes of scrolling through email and usually didn't happen.

Now it's written into the meeting note before you wake up.
