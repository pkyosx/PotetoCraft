# Perf issue

A fix you cannot point to a number for is a guess. Source code tells you where time might go. Only a run tells you where it does.

1. Write the sentence you want to be able to send at the end, number and unit included.
2. Measure the path the user actually waits on to get a baseline. Check it against `../references/measurement-checklist.md`.
3. Find out what holds the baseline where it is (`../references/principles/explain-the-number.md`). Do not plan a fix until you can name it.
4. Look at the hot work in three passes, cheapest first, and stop as soon as the target is reached. **Remove.** Work whose result nobody reads, and work done twice. **Move.** Work that can wait, leave the critical path, or run alongside other work. **Shrink.** Fewer items per call, or a cheaper way to do each one.
5. Base the plan on what you measured. Use the **design** skill (`../../design/SKILL.md`) if the fix reaches beyond one function.
6. Change one thing at a time. Measure after each change, interleaved with baseline runs. Keep a change only if the number moves.
7. Check the final number against the measurement checklist again. If it is inconclusive, say so.
8. Run the hand-off playbook (`hand-off.md`).

**Reply:** where the raw runs are saved and what limited the number, then the before and after values with units, run counts, and the difference.
