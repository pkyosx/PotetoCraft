# Refactoring

You own the contract. The structure changes and the behavior does not. If you find a bug or a missing feature, note it and handle it in a separate Bug fix or Feature run.

1. Pin current behavior before moving anything. Use existing tests, or write a characterization test, snapshot, or output-diff script. A passing type check or lint is not a pin.
2. Record the before evidence: the pin passing on the old code, with its output.
3. Name the target shape: modules, types, and call graph as you would build them today. Run the **design** skill (`../../design/SKILL.md`) if it crosses a function boundary.
4. Subtract first (`../references/principles/subtract-before-you-add.md`). Remove dead code and one-caller wrappers before adding the new shape.
5. Move in small steps. Keep the pin green after each one. When an API changes, move every caller and remove the old API in the same pass (`../references/principles/migrate-callers-then-delete-legacy-apis.md`). Search strings and docs for missed renames.
6. Record the after evidence: the same pin passing on the new code, plus an output diff for larger reshapes.
7. Check the result reads easier (`../references/principles/minimize-reader-load.md`). If it does not, revert it.
8. Run the hand-off playbook (`hand-off.md`).

**Reply:** what structure changed, the pin, the before and after evidence, the reader-load gain, and anything you reverted. No new behavior.
