# Explain the Number

**Apply when** a measured number is about to drive a decision, a report, or your own belief, such as a speedup, a regression, a latency, a throughput, or an eval score.

A number worth trusting arrives with its story attached. It reads like "startup 4.2 s over 9 runs, spread 0.3 s, bound by reading the plugin index from disk." To write that sentence honestly you need two things.

**Rule out the boring explanations first.** Each needs a check, not a shrug:
- Some runs errored or returned early, so less work happened.
- A cache, a skipped step, or a branch that never ran made one side cheap.
- The two sides ran with different settings.
- The difference sits inside the run to run spread.
- The changed code is a tiny share of what a user actually waits for.

For an eval score, also confirm each run attempted the real task and that the gap repeats across trials.

**Then name what holds it where it is.** Point to the one thing that stops it from being better. That might be a single busy thread, a slow disk, a mutex everyone waits on, or the tool that generates the input. Get this from data recorded while the run happened, such as a profiler trace or system counters, and connect it to a place in the code. Reading the source and guessing is not evidence.

One quick sanity bound. If the saving you claim is bigger than the time the changed code ever took, something is wrong.

Performance work follows [the measurement checklist](../measurement-checklist.md). Whether the output exists and is correct at all belongs to [prove-it-works](prove-it-works.md).
