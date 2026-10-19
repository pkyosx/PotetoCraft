# Foundational Thinking

**Apply when** you are about to write logic and still have to choose the core types, the data structures, or the order of scaffold work and feature work.

Settle the shape of the data before you write the code that uses it.
List how the data will be read and written, then pick structures that make the common paths simple.
Once the data is right, most of the logic becomes obvious.

Build first whatever helps every later step. Test setup, linting, shared types, and a working build are scaffold.
Remove dead code before you lay the scaffold, per [subtract-before-you-add](subtract-before-you-add.md).
Before two actors share state, ask what happens when the other one changes it at the same moment. If the answer is not "nothing", isolate it per [separate-before-serializing-shared-state](separate-before-serializing-shared-state.md).
Remove duplication in structure, not in every line. Three similar lines beat an early abstraction.
Each step should land a whole abstraction or deepen one that exists, not scatter special cases across callers.

You skipped this when the logic is full of conversions between shapes, or when a feature lands before the tests that would check it.
You followed it when the core types are written down first and each later change reads as a natural use of them.
