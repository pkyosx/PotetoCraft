# Model the Domain

**Apply when** you write stateful logic, or when code branches heavily or repeats the same assumption about a shape across files.

Put the real rules of the domain into a data structure instead of spreading them across conditionals.
The right structure makes invalid states impossible to write and removes branches.
Choosing it now is cheap. Recovering it later looks like a refactor and gets postponed.
Use a state machine instead of several booleans that must agree.
Use a typed model instead of loose parameters.
Use a lookup table, registry, or tagged union instead of matching branches in many files.
Organize a module around one body of domain knowledge, not around steps like load, check, transform, and save.
When nothing obvious fits, write down what must never happen and how the data is read, then pick the structure that encodes exactly that.
Do not force it. If the current code is clear, local, and unlikely to grow, leave it plain.

You skipped this when a new feature adds one more branch to an existing if/else chain, or a new flag that has to be kept consistent with an older one by hand.
You followed it when the new case is a new entry in a structure, not a new branch in the code.
