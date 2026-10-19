# Redesign from First Principles

**Apply when** a new requirement has to fit into a design that was built without it.

Do not attach the requirement to the side of the current design.
Ask what you would build if this requirement had been known on day one.
Read every affected file first, so you know the current design and why it is shaped that way.
Sketch the design that treats the requirement as a founding assumption.
Carry the change through every place it touches. Types, docs, examples, tests, and stated rationale all move together.
Design the end state in full, then ship it in small verified pieces per [sequence-verifiable-units](sequence-verifiable-units.md).

You bolted it on when the new requirement lives in a special case, an extra flag, or a branch that the rest of the design does not know about.
You followed this when a reader could not tell which requirement came last.
This differs from [attack-the-premise](attack-the-premise.md), which questions a fact the design assumes. Here the facts are fine and the design must grow.
