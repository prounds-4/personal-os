# Personal OS

A personal knowledge management system with an AI agent at the helm. Plain markdown, git-versioned, [Obsidian](https://obsidian.md)-readable, and maintained by [Claude Code](https://claude.com/claude-code) instead of by you.

The premise: **you are the bottleneck, and the bottleneck is what you optimize.**

Every knowledge system I built before this one died the same way. I captured notes, linked them, reviewed them, and then a busy week hit and the graph rotted. That is the standard failure mode of PKM: the human is the maintenance worker, so the system is only as good as the human's worst week.

So I inverted the roles. The vault is plain markdown in a git repo, and agents do the maintenance. They capture, link, enrich, and review. I design the work, make the judgment calls, and consume the output. The graph stays dense because keeping it dense is no longer my job.

This repo is that system, genericized: the schema, the operating manual, the routines, and the guardrails that make handing over the keys safe.

## Why it works

Three design commitments do the heavy lifting. They are what separate this from "I pointed an LLM at my notes."

1. **Typed, schema-backed markdown.** Every note declares what it is: Person, Organization, Event, Project, Plan, Note. Relationships are typed, directional links in frontmatter, not a generic `related` bag. Agents traverse and update the graph without parsing prose.
2. **Explicit section ownership.** Every file type marks its sections as human-only or agent-managed. Your personal notes on a person are sacred. The overview and history are agent-owned. Clear write-contracts are what make autonomy safe.
3. **Git as undo.** Every agent action is a commit. A bad run is one `revert` away. That is what lets you hand over the keys without flinching.

None of this depends on you being disciplined on a given day. It depends on the contracts being specified well once.

## The daily loop

- **Overnight**, a routine preps notes for today's meetings from your calendar, enriches the people, organizations, and projects that changed yesterday, and writes a morning brief into the day's note. You wake up to a graph denser than when you went to sleep.
- **During the day**, meetings land as notes linked to the people, organizations, and projects they touch. Those links are the fuel: enrichment derives its worklist from what actually changed, not from a queue you have to maintain.
- **In the evening**, a close-out ritual recaps the day, updates the record of everyone you met or emailed, and files loose pages.
- **On Sundays**, a weekly review closes the week against your quarterly and annual targets and preps next week's plan.

Four moving parts. You touch none of the plumbing.

## What's in here

| Path | What it is |
|---|---|
| [CLAUDE.md](CLAUDE.md) | The operating manual. The model, the structure, date discipline, and the rules every agent session reads first. Start here. |
| [Templates/](Templates/) | One per record type: Person, Organization, Event, Project, Responsibility, Plan (annual/quarterly/weekly), Daily Note. |
| [Bases/](Bases/) | Obsidian [Bases](https://help.obsidian.md/bases) saved views over the graph: People, Organizations, Projects, Events. |
| [Agents/](Agents/) | Docs written for the machine. A derived memory cache, rebuilt nightly, plus an append-only run log. |
| [Logs/](Logs/) | Behavior tracking. A daily scorecard and a principle rotation computed from two frontmatter fields. |
| [.claude/routines/](.claude/routines/) | The scheduled agents. `night-shift.md` runs before dawn; `weekly-review.md` runs Sunday. |
| [.claude/skills/](.claude/skills/) | The manual rituals. `end-day` closes out the day; `scan-calendar` preps meetings on demand. |
| [docs/](docs/) | The long form. Ten chapters, starting with the philosophy. |

## The docs

1. [The philosophy](docs/01-philosophy.md). I am the bottleneck, and the three commitments that follow from it.
2. [The model](docs/02-the-model.md). Types, typed relations, and who owns which section.
3. [The personal CRM](docs/03-the-crm.md). Running your network like a CRM, and why meetings are the fuel that keeps it current.
4. [The planning cadence](docs/04-planning.md). Annual to quarterly to weekly, Responsibilities, and running yourself like a corporation.
5. [The daily note](docs/05-the-daily-note.md). One page per day, and the only page you live in.
6. [Pages and logs](docs/06-pages-and-logs.md). The generic layer, and tracking behavior in files that outlive apps.
7. [The agents folder](docs/07-the-agents-folder.md). Documentation written for the machine, and why memory must be derived.
8. [The daily loop](docs/08-the-daily-loop.md). How the four moving parts feed each other.
9. [Guardrails](docs/09-guardrails.md). The rules that earned their place, mostly the hard way.
10. [Make it yours](docs/10-make-it-yours.md). What to change, what to keep, what I built and deleted.

## Getting started

1. **Clone this into a private repo.** Your vault is your life; the template is the only part that should be public.
2. **Open it as an Obsidian vault** and open the same folder in Claude Code.
3. **Edit [CLAUDE.md](CLAUDE.md).** Fill in the placeholders: your name, your timezone, your responsibilities, the tools you actually use. This file is the system's constitution, and everything else reads it first.
4. **Connect what you have.** The routines assume a calendar, mail, and a task manager. Any of them can be swapped or dropped; see [docs/10-make-it-yours.md](docs/10-make-it-yours.md).
5. **Register the routines** as scheduled agents pointed at your repo, committing to `main`.
6. Each morning, read the brief. Each evening, run the close-out. Let the overnight run do the rest.

## Guardrails worth stealing even if you take nothing else

- **The agent never edits its own configuration.** Nothing under `.claude/` is writable by a routine. If a routine thinks it should change, it says so in the brief and you decide.
- **Human-only sections are never touched.** `## Personal Notes` on any record belongs to you alone.
- **Integrations default to read-only.** The task manager gets read, never write. An early run created a task nobody asked for; that rule exists because of it. You decide what becomes a task.
- **Date discipline is explicit.** Date errors are the most common failure mode. Convert timestamps to your local zone before writing them, never write a future date as past, and prefer shell `date` output over the model's memory.
- **Reconcile, don't append.** Records get folded and re-distilled, never grown by one line per interaction. Otherwise every file becomes a changelog nobody reads.

## The same pattern, elsewhere

Applied to a $525M construction project: [Claude of Record](https://github.com/prounds-4/claude-of-record). Applied to training: [Fitness OS](https://github.com/prounds-4/20-minute-fitness).

## License

Docs under [CC BY 4.0](LICENSE). Code and templates under MIT. See [LICENSE](LICENSE).
