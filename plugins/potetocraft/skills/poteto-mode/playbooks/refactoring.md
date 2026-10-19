# Refactoring

A user of this code should not be able to tell you were here. Every output, error, and side effect stays as it was. If you spot a real bug or a gap in features along the way, write it down and leave it for a separate Bug fix or Feature run.

1. Pick the evidence that will prove nothing changed. Good options are the existing tests, a new test that captures what the code returns today, a snapshot, or a script that diffs output. A clean type check or lint run proves the code compiles, not that it behaves the same, so it does not count.
2. Run that evidence on the code as it is now and keep the output.
3. Picture the target. If this area were written today, what modules would it have, what types, and which pieces would call which? For anything bigger than one function, work it out with the **design** skill (`../../design/SKILL.md`).
4. Remove before you rearrange (`../references/principles/subtract-before-you-add.md`). Code nothing calls and wrappers with one caller go first.
5. Move in small steps and run the evidence after each one. When an internal API changes, update every caller and remove the old API in this same run (`../references/principles/migrate-callers-then-delete-legacy-apis.md`). Old names also hide in strings and docs, so search those.
6. Run the evidence on the result and keep that output beside the first one. A large reshape also gets a diff of the two.
7. Read the result as someone new to it would (`../references/principles/minimize-reader-load.md`). If it is not easier to follow, revert the edits you made in this run by editing those lines back, not with `git checkout` or `git reset`. Leave alone any change you did not make.
8. Run the hand-off playbook (`hand-off.md`).

**Reply:** first, how a reader's job got easier. Then what moved where, which evidence proved behavior held, the two outputs side by side, and any step you reverted. State that behavior is unchanged.
