# Make it yours

This is my system with my name filed off. Nothing here is sacred except the three design commitments in [the philosophy](01-philosophy.md). Take the shape, throw out the specifics.

## What to change first

1. **[CLAUDE.md](../CLAUDE.md).** Fill every `{PLACEHOLDER}`. The "About you" section matters more than it looks: it is the difference between an assistant that resolves a name instantly and one that guesses. Keep it current.
2. **Your timezone.** The routines export `TZ` because cloud runners default to UTC and that makes "today" wrong for any run after late afternoon. Set it, and remember the conversion rule applies to note *content*, not just the shell.
3. **Your style rules.** Write down how you want prose to sound, once. Mine bans em-dashes, emoji, and a list of AI-tell words. Yours will differ; the point is that it is written down and every agent reads it.
4. **Your types.** Mine are Person, Organization, Event, Project, Responsibility, Plan, Topic, Note. If you do not run a personal CRM, delete half of them. The schema should describe your life, not mine.

## Swapping the integrations

The routines assume a calendar, mail, and a task manager. All three are swappable, and any of them can be dropped.

| Assumption | If you don't have it |
|---|---|
| Calendar | Drop meeting prep. The rest of the loop works; enrichment just runs off `git diff` instead of meeting links. |
| Mail | Drop the email sweep in enrichment and end-day. You lose "always-current history," since a lot of relationship activity is email-only. |
| Task manager | Drop the task steps. Keep the read-only default if you wire in something else. |
| Meeting notetaker | Drop the transcript step. Write notes by hand into `## Notes`. |

Keep the read-only default no matter what you connect.

## What I'd keep even in a much smaller system

If you build nothing else, build these:

- **Typed frontmatter links.** Without them there is no graph, just files.
- **Human-only sections, marked in the file.** Without them you will not trust the agent, and an agent you do not trust is worse than none.
- **Git.** Every action a commit.
- **Reconcile, don't append.** The rule that decides whether your records are worth reading in a year.
- **One file the agent reads first.** Call it CLAUDE.md, AGENTS.md, whatever. A system without a constitution drifts.

## What I'd skip

Things I built and deleted:

- **A goal-propagation machine.** Block IDs, status emoji, `Supports [[goal]]` tags, checkboxes propagating up a hierarchy. It was fragile, it rotted, and maintaining it became its own job. Plain prose and a `parent` link does the same work.
- **A stored "current state" file.** It rots immediately and rotted state gets cited as truth. Compute state on demand.
- **Fifteen skills and a pile of routines.** I cut mine to two routines and two skills and the system got better. Every automation is a thing that can break silently.
- **A stored enrichment queue.** Derive the worklist from ground truth (`git diff` plus links). A queue is one more thing to desynchronize.

## Cost and cadence

The overnight run is the expensive one, and it should be: it is doing the work you would otherwise do. Cap the entities per run, cap the brief's length, and let the next night's diff catch the overflow.

The constraint I aim for: the system should always have more queued work than available compute. If your agent is idle, you are under-delegating.

## A warning

This system reads your calendar, your mail, and your notes, and writes to a repo. That is a lot of access. Two rules make it survivable:

1. **Keep your vault private.** Only the template should ever be public. Everything in this repo is genericized on purpose.
2. **Read the diffs.** Not every one, forever. But for the first few weeks, read what the agent wrote before you trust it. The whole model depends on the contracts being right, and you only find out they are wrong by looking.
