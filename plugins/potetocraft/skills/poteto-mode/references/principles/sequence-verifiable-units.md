# Sequence Verifiable Units

**Apply when** the work has many steps, such as a sweep, a migration, or a run of similar edits, and when you plan how to present it for review.

Think of a long job as a chain of small bets. You settle each bet before you place the next one.

For every unit:
1. Confirm the starting point is good. Run the check once before you touch anything, so later results compare against reality.
2. Make one change.
3. Run the check and record the result.
4. Move on only if it passed.

Do not batch units to save time. If ten renames go in together and the build fails, you now search ten places. If they go in one at a time, the failing one names itself. This holds even when a codemod makes the edits. A cheap check is still worth running.

The same idea shapes what you hand to reviewers. In the report, suggest a split into commits or PRs where each piece builds on the last and could be reviewed alone. Some orders that work well:
- a test that shows the bug, then the change that fixes it
- deleting the old path, then reorganizing what is left
- a measurement, then the optimization it justifies
- the empty skeleton, then the behavior that fills it

You followed this when each unit has a recorded check and outcome. To keep checks honest, see [prove-it-works](prove-it-works.md). To make them cheap, see [build-the-lever](build-the-lever.md).
