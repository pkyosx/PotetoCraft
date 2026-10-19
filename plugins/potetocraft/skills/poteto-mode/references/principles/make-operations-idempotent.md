# Make Operations Idempotent

**Apply when** you design a command, a lifecycle step, or a processing loop that may crash, restart, or retry.

An operation should reach the same correct end state no matter how many times it runs or where the last run stopped.
Read the current state, compare it with the goal, and apply only the difference.
A step written this way is safe to repeat, because a repeat finds nothing left to do.
Anything a run leaves behind, such as a lock, a temp file, a half-written record, or a claimed job, must be recognizable as stale by the next run.
Judge staleness with evidence that holds wherever the last run stopped, not only in the common case.
Write to a temporary path and rename into place. Compare outputs by content, not by timestamp or order.

Ask three questions. What happens if this runs twice in a row? What happens if the last run crashed at any point? Does every rerun end in the same state?
If an answer is "it depends on what was left behind", add a step that reconciles the current state with the goal.
You followed this when you ran it twice, and once after an interrupted run, and the end state matched.
