# Bug fix

You own the fix. Keep only changes that a run proved necessary. A speculative change is an experiment, and experiments come out of the diff once they are settled.

1. Make the bug happen yourself, on the surface where the user saw it (UI, CLI, API, or a test). If that surface is out of reach, get as close as you can and tell the user precisely what stops you.
2. If it will not appear, narrow the inputs, build the trigger by hand, or add logging until it does.
3. Write a failing test when a cheap local test is possible (`../../tdd/SKILL.md`).
4. Write down the possible causes. Eliminate them with evidence from runs, choosing each time the check that rules out the most at once. Log values whenever the state is unclear.
5. Identify the earliest wrong step (`../references/principles/fix-root-causes.md`). Ask whether the state that tripped the code is legal. If it is, teaching the code to handle it is the fix. If it is not, a guard just hides it.
6. Plan the smallest change the evidence supports. When it reaches across a function boundary, use the **design** skill (`../../design/SKILL.md`). You may delegate the edit as described under Subagents in `../SKILL.md`.
7. Check again on the surface from step 1. The original reproduction must now pass. A green unit test by itself is not enough. Report a wrong-surface or unclear result as unproven.
8. Undo your own edits from this session that a ruled-out cause led to. Never discard changes you did not make.
9. Run the hand-off playbook (`hand-off.md`).

**Reply:** the symptom, the earliest wrong step, the change, and the check, with the before (failing) and after (passing) output copied as it ran.
