# Guardrails

Autonomy is only safe when the boundaries are written down in a file the agent reads every session. These are the rules that earned their place, most of them the hard way.

## The agent never edits its own configuration

Nothing under `.claude/` is writable by a routine: not the routines, not the skills, not the operating manual.

A system that can rewrite its own constraints has no constraints. If a routine concludes it should change, it says so in the brief and a human decides. This costs a round trip and buys the entire safety model.

## Human-only sections are never touched

`## Personal Notes` on any record belongs to you alone. So does the `## Plan` section of a weekly plan, and the wording, target, and status of any goal.

State it in the file itself, not just the manual:

```markdown
## Personal Notes
<!-- Human-only. Claude Code never modifies this section. -->
```

The comment is for the agent, and it works. Belt and suspenders: the rule lives in the operating manual *and* at the point of use.

## Integrations default to read-only

The task manager is read-only. The agent reports what is done and due, and surfaces open loops for triage. It never creates, completes, or modifies a task.

This rule exists because an early run created a task nobody asked for. That is a small harm with a large lesson: an agent with write access to your commitments is deciding what you owe people. You decide what becomes a task.

The same default applies to anything outward-facing. Read freely; write only where the contract is explicit.

## Date discipline

Date errors are the most common failure mode in a system like this, by a wide margin.

- **Inject today's date every turn** and treat it as ground truth.
- **A date later than today is scheduled, not past.** Never write it in past tense, never log it as an interaction, never set `last_met` to it.
- **Timezone applies to note content, not just the shell.** Calendar and mail APIs return UTC. An email stamped `2026-06-19T03:45:00Z` was sent on 06-18 at 8:45pm in a UTC-7 zone. Log it on 06-18. Convert before writing.
- **Prefer shell output over memory.** `date +%Y-%m-%d`, not recall.
- **A file's own frontmatter date beats its filename and beats your memory.**
- When-it-happened fields (`last_met`, `last_enriched`) must be in the past. If unknown, leave them blank rather than guessing.

## Never invent facts

Only record what a source supports. On a graph that you will later trust and cite, a plausible fabrication is far more expensive than a gap. Gaps are visible; fabrications are not.

A corollary worth stealing: **an agent may never cite its own prior output as a source.** Otherwise errors laminate. Every figure traces to a real document or it does not go in.

## Cap the blast radius

- Cap entities enriched per run. If there are more, log the overflow; the next run's diff catches them.
- If one commit would touch more than ~25 files, split it by step.
- On any step error: commit what is done, note the failure in the brief, continue to the next step. Never abort the whole run, and never leave the vault in a half-written state.

## Git as undo

Every agent action is a commit, pushed. This is not bookkeeping; it is the entire risk model.

The failure mode of an autonomous system writing to your notes is not that it will occasionally be wrong. It is that being wrong could be unrecoverable. Version control turns an unrecoverable risk into an annoyance you fix with `git revert`.

It also makes the agent's work reviewable. `git log` is the audit trail, and `git diff` is how the next run knows what changed.

## No autonomous loops

Two scheduled routines. No agent registers new schedules, spawns crons, or creates recurring work for itself.

Every automation is a thing that can rot, run up cost, and produce output nobody reads. The number should stay small enough that you would notice if one broke.
