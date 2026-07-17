# Overnight Flags

Append-only log of scheduled routine runs. Never rotate or truncate.

The agent's own audit trail: what ran, what it touched, what it skipped and why. You will not read this most days. You will read it the day something goes wrong.

---

<!--
Format, one block per run:

## YYYY-MM-DD HH:MM

- **Prepped:** N meetings. [[Event]], [[Event]].
- **Enriched:** N entities. [[Person]] (what changed), [[Organization]] (what changed).
- **Skipped:** what and why (no confident match, over the cap, ambiguous source).
- **Errors:** what failed, what was committed anyway.
-->
