# Perf issue

You own the numbers. Every fix ties to a measurement. Reading the source is not a substitute for measuring.

1. Draft the sentence you hope to report at the end, exactly as you would phrase it.
2. Capture a baseline on the real path the user waits on. Vet it with `../references/measurement-checklist.md`.
3. Explain the baseline number (`../references/principles/explain-the-number.md`). Name what limits it before you plan a fix.
4. Try the cheapest ideas first. Skip work whose result nothing uses. Avoid repeating work. Do less of it. Do it later or off the critical path. Do it concurrently. Make it cheaper. Stop once the target is met.
5. Plan the fix from the measurement. When the fix reaches past one function, use the **design** skill (`../../design/SKILL.md`).
6. Apply one change at a time. Measure after each, alternating with the baseline, and keep only changes that move the number.
7. Vet the final number with the measurement checklist. An inconclusive result is reported as inconclusive.
8. Run the hand-off playbook (`hand-off.md`).

**Reply:** the baseline, the result, the delta with units and run count, the limiter, and where the raw measurements are saved.
