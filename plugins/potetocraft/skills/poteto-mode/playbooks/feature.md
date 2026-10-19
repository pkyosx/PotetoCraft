# Feature

Delegates may type the code. The design is yours, and so is checking every line they return.

1. Read the surrounding code with the **explain** skill (`../../explain/SKILL.md`) so what you add fits what is already there.
2. Settle the data before the logic (`../references/principles/model-the-domain.md`). Ask what shape would make the bad cases impossible to write. An order with `status: "draft" | "paid" | "shipped"` cannot be both draft and shipped, while three booleans can.
3. Use the **design** skill (`../../design/SKILL.md`) before coding if the change reaches beyond one function.
4. Split the work into pieces that can each be checked on their own (`../references/principles/sequence-verifiable-units.md`). Note which pieces share files or state. Pieces that write to the same place run one after another.
5. Write each delegate a precise brief. Include file paths, the data shape, how you will judge success, and the absolute path to `../SKILL.md`.
6. Compare every diff that comes back with its brief and with the principles you applied.
7. Before starting the next piece, try the current one where a user would meet it (`../references/principles/prove-it-works.md`). A result that is unclear, or that came from a different surface, is unproven, and you say so.
8. Run the hand-off playbook (`hand-off.md`).

**Reply:** the open decisions first, then what a user can now do, the data shape behind it, how each piece was checked, and the reason for each choice. When designs competed, compare them in a table.
