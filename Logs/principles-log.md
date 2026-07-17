---
type: Note
subtype: principles
rotation_start_week: "2026-W01"
rotation:
  - "{Principle 1}"
  - "{Principle 2}"
  - "{Principle 3}"
  - "{Principle 4}"
  - "{Principle 5}"
  - "{Principle 6}"
  - "{Principle 7}"
  - "{Principle 8}"
---

> [!info]
> This week's principle is **computed**, not scheduled: take the current ISO week,
> subtract `rotation_start_week`, modulo the length of `rotation`. No scheduler, no
> state file, nothing to sync or drift. Two fields and arithmetic.
>
> At close-out the agent works out this week's principle, asks how it showed up
> (lived it / mixed / didn't think about it / worked against it), takes one sentence,
> and appends it under that week's heading.
>
> List the principles you actually hold. Eight to sixteen works; the rotation just
> needs to be long enough that one doesn't come around so often you stop seeing it.

---

<!--
Format:

## 2026-W01. {Principle}

- **Lived it.** One sentence on how it showed up.
-->
