# Explain the Number

**Apply when** you are about to trust, report, or act on a number you measured, such as a speedup, a regression, a latency, a throughput, or an eval score.

A number you cannot explain is not yet a result.
Ask why it is not twice as good. Name the resource or code path that limits it, such as a core, a lock, the disk, the network, or the load generator.
Find the limiter from a profile or system counters taken during the run, then map it to source code. A guess from reading code does not count.
List what else the number could be measuring and rule each one out with evidence. Usual suspects are errors, skipped or cached work, code that never ran, one side left on default settings, noise, and a change too small to matter end to end.
For an eval score, check that every run actually did the task and that the gap holds across trials.
Record the run count, the spread, and the limiter next to the number.
For a performance number, follow the full procedure in [the measurement checklist](../measurement-checklist.md).

You skipped this when the number has no run count, no spread, or no named limiter.
You skipped it when the claimed saving is larger than the total time the changed code took.
This differs from [prove-it-works](prove-it-works.md), which checks that an output is real.
