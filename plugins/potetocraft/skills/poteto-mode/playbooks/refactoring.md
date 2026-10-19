# Refactoring

The behavior stays fixed and only the structure moves. That promise is yours to keep. A bug or a missing feature you notice goes in the notes for its own Bug fix or Feature run.

1. Lock down today's behavior before you move code. Existing tests can do it. So can a new test that records current outputs, a snapshot, or a script that diffs output. Type checks and lint do not lock behavior.
2. Run that lock on the untouched code and save the output as the before evidence.
3. Describe where the code should end up, its modules, types, and who calls whom, as if you were writing it fresh. Use the **design** skill (`../../design/SKILL.md`) when the change reaches past one function.
4. Clear space first (`../references/principles/subtract-before-you-add.md`). Take out unused code and single-caller wrappers before the new structure goes in.
5. Take small steps, and rerun the lock after each. If an API changes, move all of its callers and drop the old API during this pass (`../references/principles/migrate-callers-then-delete-legacy-apis.md`). Search string literals and docs for names you missed.
6. Run the lock on the finished code and save that output as the after evidence. For a large reshape, add an output diff.
7. Confirm a newcomer would find the result easier to read (`../references/principles/minimize-reader-load.md`). If not, undo your own edits from this run. Never discard changes you did not make.
8. Run the hand-off playbook (`hand-off.md`).

**Reply:** the structural change, the lock you used, before and after evidence, how reading got easier, and anything you backed out. No behavior changes.
