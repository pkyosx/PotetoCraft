# Bug fix

Picture the reviewer pointing at any line of your diff and asking "what run showed this was needed?" Every line should have an answer. A change you made on a hunch is still a test of that hunch. Once the test is over, take it out.

1. Get the bug in front of you on the surface where the user hit it (UI, CLI, API, or a test). If you cannot reach that surface, get as close as you can and tell the user exactly what is in the way.
2. When it refuses to show up, change the setup until it does. Shrink the input, recreate the triggering conditions on purpose, or print more of the state on each run.
3. If a cheap local test can capture it, write that test now and watch it fail (`../../tdd/SKILL.md`).
4. List what could be causing it. Prefer the run that splits the list in half over the run that tests one idea. When you cannot tell what a value is, print it instead of guessing.
5. Find the first point where things went wrong (`../references/principles/fix-root-causes.md`). Then decide if the state that reached that point is allowed. Allowed means the code there must learn to handle it. Not allowed means a guard would only hide it, so fix whatever produced it.
6. Plan the smallest change your evidence backs. If it crosses a function boundary, use the **design** skill (`../../design/SKILL.md`). The edit may go to a delegate, as Subagents in `../SKILL.md` describes.
7. Go back to the surface from step 1 and run the same reproduction. Only that run passing counts as fixed. A passing unit test shows one branch behaves. It does not show the user's bug is gone. If the run was on another surface or the result is ambiguous, call the fix unproven.
8. Revert your own edits from this session that came from causes you ruled out, by editing those lines back, not with `git checkout` or `git reset`. Leave alone any change you did not make.
9. Run the hand-off playbook (`hand-off.md`).

**Reply:** the reproduction output from before and after the change, copied as it ran, then what the user saw, where it first went wrong, and what you changed.
