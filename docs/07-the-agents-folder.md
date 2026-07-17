# The agents folder

A section of the vault written for the machine, not for you.

`Agents/` is documentation whose only reader is an LLM. Once you accept that an agent is a first-class user of your knowledge base, it follows that it needs its own docs, and that those docs belong in the vault under version control rather than in some app's settings pane.

## Agent Memory: a derived cache

Every session starts cold. The fix most people reach for is a "memory" file they hand-write and hand-update, which rots within a month.

The fix here: **memory is derived, never authored.**

```markdown
---
type: Note
last_updated: 2026-07-16
---

> **This file is a derived cache.** It is regenerated from the vault by the
> overnight routine. Do not hand-edit. To change what the agent "remembers,"
> update the underlying files (people, projects, plans, meetings) and let the
> nightly run rebuild this summary.

# Current State
## Active work
...
```

The overnight routine rebuilds the whole file each night from the graph: what's active, who you've dealt with in the last two weeks, what shifted, this week's arc. Under about 800 words, wikilinked, overwritten whole.

The banner is not decoration. It is the contract, and it points at the deepest rule in the system: **there is exactly one source of truth, and it is the vault.** Memory is a *view* over it.

This matters because the alternative is seductive and broken. The moment you hand-edit the memory file, you have two versions of reality: what the vault says and what the memory says. They diverge immediately, the agent starts citing the stale one, and you cannot tell which is which. A derived cache cannot drift, because it is thrown away and rebuilt every night.

It is the same lesson as ["state rots"](01-philosophy.md), applied to the agent's own head. If you can compute it, compute it. A stored summary is a liability with a shelf life.

## Why a memory file at all

If the vault is the truth, why cache anything?

Because context is finite and traversal is expensive. Every session would otherwise burn its opening minutes rediscovering the same facts: what's live, who matters, what happened last week. The nightly rebuild pays that cost once, off-hours, and every session that day reads the answer instead of deriving it.

It is a cache in the ordinary engineering sense: correctness lives in the source, speed lives in the cache, and the cache is invalidated on a schedule you control.

## Overnight flags

An append-only log of what the routines did: which files changed, which records were enriched, what got skipped and why.

Append-only, never rotated, never truncated. It is the agent's own audit trail, and it costs nothing to keep.

You will not read this most days. You will read it on the day something goes wrong, and on that day it is the difference between "the agent did something weird last Tuesday" and knowing exactly what ran, what it touched, and where it stopped.

## The pattern worth stealing

Give the agent its own folder. Put three things in it:

1. **A derived state file** that answers "what's going on," rebuilt on a schedule, never hand-edited, with the banner saying so.
2. **An append-only run log** so you can audit what happened.
3. **Nothing the agent can't rebuild.** If losing the folder would cost you anything, something in it belonged in the vault proper.

That last rule is the test. `Agents/` should be entirely disposable. Delete it and tonight's run recreates it. If you flinch at deleting it, you've been hand-editing, and the drift has already started.
