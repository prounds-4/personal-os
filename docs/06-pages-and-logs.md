# Pages and logs

Two parts of the vault that look like housekeeping and are actually load-bearing.

## Pages: the generic layer

Not everything is a person, a meeting, or a project. Most of what you know isn't.

`Pages/` is where the rest lives: the subjects you hang notes off, the reference material, the essays, the working docs. It exists so the typed CRM stays clean. The moment you start filing an essay as a "Project" because those are the only types you have, the schema is lying to you.

The layout that settled for me:

| Path | What it holds |
|---|---|
| `Pages/Meta/Responsibilities` | The standing areas of life. See [planning](04-planning.md). |
| `Pages/Project Docs/<Project>/` | Per-project working docs: research, drafts, analysis. Distinct from the `CRM/Projects` record. |
| `Pages/Reference/` | Things you look up: quotes, articles, profiles. |
| `Pages/Reflective/` | Things you wrote: essays, journal, talks. |

**Project Docs vs. the Project record** is the distinction people miss. The CRM `Project` note is the *record*: status, links, overview, history. The `Project Docs` folder is the *work*: the messy drafts and analysis. Keeping them apart means the record stays a readable summary instead of drowning in artifacts, and the agent knows which one to update.

### The `pages` field

Typed relations cover the CRM (`people`, `organizations`, `projects`, `events`). `pages` is the escape hatch: the general link to anything else, used when no typed relation fits.

A weekly plan carries `pages` pointing at the Responsibilities it touched. An essay carries `pages` pointing at the topics it's about.

Every schema needs an escape hatch, or people bend the typed fields to fit and the graph quietly stops meaning anything. The trick is that `pages` is *explicitly* the generic one, so the typed fields stay honest. It is the exception that protects the rule.

## Logs: tracking behavior

`Logs/` holds the recurring trackers: one markdown table, one row per day, appended at the bottom.

This is the smallest part of the system and the one most likely to change you.

### The scorecard

One row per day, one column per thing you're watching. Mine tracks wake time, whether I trained, a handful of "better than yesterday?" categories scored `y` / `s` / `n`, and a couple of yes/no facts.

Two mechanics make it work, and both are about trust:

**The agent asks; it never guesses.** At close-out it reads today's row, and if cells are empty it asks you. It does not infer that you probably worked out. A scorecard with invented data is worse than an empty one, because you'll believe it in six months when you're looking for a trend.

**It never overwrites a filled cell.** You may have written it by hand. Your value always wins.

Ask compactly, once, as a grouped question. Six separate interrogations at 9pm is how you get someone to stop running the ritual.

### The principle rotation

The mechanism I like most in the whole vault, because it's three lines of frontmatter doing the work of an app.

```yaml
type: Note
subtype: principles
rotation_start_week: "2026-W01"
rotation:
  - "{Principle 1}"
  - "{Principle 2}"
  - "{Principle 3}"
  # ... and so on
```

The current week's principle is *computed*: take the ISO week, subtract the start week, modulo the rotation length. No scheduler, no state file, no app. Just arithmetic over two fields, so it can never drift or need syncing.

At close-out the agent works out this week's principle, asks how it showed up (lived it / mixed / didn't think about it / worked against it), takes one sentence, and appends it under the week.

Write your principles down once. Let a deterministic rotation put one in front of you each week. Answer honestly for sixty seconds. That's the whole practice, and it is more than most people ever do with the values they claim.

### Why logs belong in the vault

Everything else here argues that tasks live in your task manager and content lives in files. So why keep trackers in markdown?

Because these are the numbers you want in ten years, and every app that has ever held them is gone or wants a subscription. A markdown table in your own git repo will open in 2046. The scorecard is the clearest case in the entire system for **file over app**: it is small, it is yours, it is boring, and it will outlive every product that would offer to hold it for you.
