# Feature

You own the design. Delegate code-writing when it helps, and review every result.

1. Name the data shape first. Pick the structure that holds it (`../references/principles/model-the-domain.md`): a state machine over loose booleans, a table over a chain of branches, a typed model over repeated shape assumptions.
2. Read the affected code with the **explain** skill (`../../explain/SKILL.md`) so the change fits what exists.
3. If the code crosses a function boundary, run the **design** skill (`../../design/SKILL.md`) before you implement.
4. Split the work into verifiable units (`../references/principles/sequence-verifiable-units.md`). Note which units are independent and which share files or state. Shared writes run one at a time.
5. Delegate each unit with a specific brief: file paths, the data shape, success criteria, and the absolute path to `../SKILL.md`.
6. Review each diff yourself. Check it against the brief and the principles you applied.
7. Verify each unit on the real surface before starting the next (`../references/principles/prove-it-works.md`). An inconclusive or wrong-surface result is not a pass; flag it.
8. Run the hand-off playbook (`hand-off.md`).

**Reply:** what you built, the data shape, the choices you made and why, how you verified each unit, and open decisions. Use a table for design alternatives.
