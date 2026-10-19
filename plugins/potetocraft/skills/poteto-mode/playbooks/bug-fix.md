# Bug fix

You own the fix. Every line you change traces to evidence from a run. A change that "might help" is a hypothesis, and it does not stay in the diff.

1. Reproduce the bug yourself on the surface where it was reported (UI, CLI, API, test). If you cannot reach that surface, drive it as far as you can, then tell the user exactly what blocks you.
2. If it does not reproduce, tighten the conditions, synthesize the trigger, or add logging until it does.
3. List candidate causes. Rule them out one at a time with runtime evidence, cutting the largest share of the problem each pass. Add logging when state is unclear.
4. Name the root cause, the first place the system went wrong (`../references/principles/fix-root-causes.md`). A guard is a fix only when the state it handles is legitimate.
5. Write a failing test first when a cheap local test path exists (`../../tdd/SKILL.md`).
6. Plan the smallest fix the evidence justifies. If it crosses a function boundary, run the **design** skill (`../../design/SKILL.md`). Delegate the edit per the Subagents section of `../SKILL.md` when that helps.
7. Verify on the same surface as step 1. The original repro now passes. A unit test alone does not prove the bug is gone. An inconclusive or wrong-surface result is not a pass; flag it.
8. Revert anything a refuted hypothesis motivated.
9. Run the hand-off playbook (`hand-off.md`).

**Reply:** what was broken, the root cause, the fix, and how you verified it, with the failing and then passing output pasted as it ran.
