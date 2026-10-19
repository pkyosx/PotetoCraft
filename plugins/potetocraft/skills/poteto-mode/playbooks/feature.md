# Feature

You own the design. Others may write code for you, and you check all of it.

1. Learn the area first with the **explain** skill (`../../explain/SKILL.md`), so the new code matches what is there.
2. Decide how the data is shaped before any logic (`../references/principles/model-the-domain.md`). Prefer one status field to several flags, a lookup table to a long branch chain, and a named type to the same shape guessed in many places.
3. When the change reaches past one function, use the **design** skill (`../../design/SKILL.md`) before writing code.
4. Break the work into units you can check one by one (`../references/principles/sequence-verifiable-units.md`). Mark which units stand alone and which touch the same files or state. Units that write the same thing go in sequence.
5. Brief each delegate precisely. Give file paths, the data shape, what success looks like, and the absolute path to `../SKILL.md`.
6. Read every returned diff against its brief and against the principles you used.
7. Exercise each unit where users meet it before you start the next one (`../references/principles/prove-it-works.md`). An unclear result, or one from the wrong surface, counts as unproven. Say so.
8. Run the hand-off playbook (`hand-off.md`).

**Reply:** what now exists, its data shape, each decision with its reason, the check for each unit, and decisions still open. Put competing designs in a table.
