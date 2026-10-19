# Explain the Number

**Apply when** a measured number is about to drive a decision, a report, or your own belief, such as a speedup, a regression, a latency, a throughput, or an eval score.

A number worth trusting arrives with its story attached. It reads like "startup 4.2 s over 9 runs, spread 0.3 s, bound by reading the plugin index from disk." To write that sentence honestly you need two things.

**Rule out the boring explanations first.** Before believing the interesting story, make each dull one fail a check:
- Is the gap bigger than the spread between repeated runs of the same side?
- Were both sides run with the same build, flags, and settings?
- Does the changed code take a big enough share of what the user waits for to matter?
- Did every run do the whole job, without errors or early exits?
- Did one side get a free ride from a cache, a skipped step, or a branch that never ran?

For an eval score, also confirm each run attempted the real task and that the gap repeats across trials.

**Then name what holds it where it is.** Point to the one thing that stops it from being better. That might be a single busy thread, a slow disk, a mutex everyone waits on, or the tool that generates the input. Get this from data recorded while the run happened, such as a profiler trace or system counters, and connect it to a place in the code. Reading the source and guessing is not evidence.

One quick sanity bound. Code that ran for 50 ms cannot save you 80 ms by getting faster. A claimed saving above the changed code's own cost means something else changed.

Performance work follows [the measurement checklist](../measurement-checklist.md). Whether the output exists and is correct at all belongs to [prove-it-works](prove-it-works.md).
