# Explain the Number

**Apply when** a measured number is about to drive a decision, a report, or your own belief, such as a speedup, a regression, a latency, a throughput, or an eval score.

A number you cannot explain is not yet a result.
Ask why it is not twice as good. Name the resource or code path that limits it, for example one saturated core, lock contention, disk or network throughput, or a client that cannot send load fast enough.
Find the limiter from a profile or system counters taken during the run, then map it to source code. A guess from reading code does not count.
Write down every other thing the number might reflect, and use evidence to eliminate each. Check first for failed requests, work that was cached or skipped, paths that did not execute, one side left on default settings, noise, and a change too small to matter end to end.
For an eval score, check that every run actually did the task and that the gap holds across trials.
Write how many runs, how widely they varied, and what bounds the result beside the number.
For a performance number, follow the full procedure in [the measurement checklist](../measurement-checklist.md).

You skipped this when the number is missing how many runs, how much they varied, or what bounds it.
You skipped it when the claimed saving is larger than the total time the changed code took.
This differs from [prove-it-works](prove-it-works.md), which confirms an output actually exists and is correct.
