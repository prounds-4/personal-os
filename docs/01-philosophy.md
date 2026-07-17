# I am the bottleneck

Every knowledge system I built before this one died the same way. I captured notes, linked them, reviewed them. Then a busy week hit and the graph rotted.

That is the standard failure mode of personal knowledge management: the human is the maintenance worker, so the system is only as good as the human's worst week.

Andrej Karpathy, on the No Priors podcast, described his job as optimizing himself out of the loop. That reframed the whole problem for me. I am the bottleneck, and the bottleneck is what you optimize.

## The inversion

So I inverted the roles. My system is plain markdown files in a git repository, and AI agents do the maintenance. They capture, link, enrich, and review. I design the work, make the judgment calls, and consume the output. The graph stays dense because keeping it dense is no longer my job.

The constraint runs the other way now. The system should always have more queued work than available compute. Idle tokens are waste.

## Systems, not intentions

Intentions don't hold; systems do. So the vault is engineered, not cultivated. Three design commitments make that real.

### 1. Typed, schema-backed markdown

Every note declares what it is: person, organization, meeting, project, plan. Relationships are typed links in structured metadata, not a generic `related` bag.

This is the load-bearing choice, and it is easy to underrate. A generic "related" field forces an agent to read prose and guess at meaning. A typed `people:` field lets it traverse and update the graph mechanically, at scale, without interpretation. The schema is what turns a pile of notes into something a machine can actually operate.

### 2. Explicit section ownership

Every file type marks its sections as human-only or agent-managed. My personal notes on a person are sacred. The summary and the history are agent-owned.

Clear write-contracts are what make autonomy safe. You cannot hand over the keys to a system where the boundaries are implied. The agent needs to know precisely which bytes are its business, and the rule has to be stated in a file it reads every session, not held in your head.

### 3. Git as undo

Every agent action is a commit. A bad run is one revert away.

That is what lets me hand over the keys without flinching. The failure mode of an autonomous system writing to your notes is not that it will occasionally be wrong. It is that being wrong is unrecoverable. Version control converts an unrecoverable risk into an annoyance.

None of this depends on me being disciplined on a given day. It depends on the contracts being specified well once.

## Reconcile, don't append

The single highest-leverage rule in the system, and the one I got wrong first.

The naive design has the agent append a line every time something happens. Met someone? Append. Emailed them? Append. Six months later every record is a changelog nobody reads, and the agent is dutifully maintaining a document with no readers.

The fix is reconciliation. The agent folds today's interaction into the existing history and re-distills the section when it gets long. Granular detail stays in the meeting note where it belongs. The person's record stays a portrait, not a transcript.

This costs more tokens per run and produces a system worth reading. That trade is always worth it.

## State rots

A related lesson, learned the expensive way on a different project.

The early design kept a "current state" file: a prose summary of where things stood. It rots immediately, and rotted state gets cited as truth, which is worse than no state at all.

Live state should be computed on demand from the records, never stored as a file. If you can derive it, derive it. A stored summary is a liability with a shelf life.

## The job that's left

What remains for me is the part that should never be delegated: deciding what the work is, setting the standards, and making the calls that require judgment. The system handles memory, maintenance, and preparation. I handle direction.

Your systems determine your floor, not your ceiling. A good week no longer depends on a good day. My output scales with how much of my own work I push onto the system.

I am the bottleneck. That is the point.
