# Sequence Verifiable Units

**Apply when** the work has many steps, such as a sweep, a migration, or a run of similar edits, and when you plan how to present it for review.

Split the job into short steps. Each step finishes at a point you can verify.
Do not start the next unit until the current one passes.
Each unit has three parts. Start from a known good state, make one change, run the check.
Start from a clean baseline so every check measures against the real starting point.
When a script does the edits, the check per unit is nearly free. Run it anyway.
A break found at the unit that caused it is easy to locate. A break found after a batch is buried under later work.

In the report, propose how to split the work into commits or PRs so the order proves the result.
A common order is the failing test first, then the fix. Others are removal before reshaping, a baseline before the treatment, and scaffold before the feature.
Each proposed unit should stand on its own, and the sequence should read as an argument.

You followed this when every unit has a recorded check and its result. See [prove-it-works](prove-it-works.md) for keeping the checks real and [build-the-lever](build-the-lever.md) for making them cheap.
