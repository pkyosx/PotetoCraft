# Outcome-Oriented Execution

**Apply when** you carry out a planned rewrite or migration that has clear phase boundaries.

Aim at the end state you can verify, not at keeping every intermediate step smooth.
Compatibility code written only to keep a midpoint stable tends to stay forever.
Say up front where temporary breakage is allowed and where it is not.
Keep fast, high-signal checks running on the areas you are actively touching.
At the end, run the full static and runtime checks and show they pass.
Breakage in the middle is fine only when it is planned, scoped, and easy to undo.

You broke this when the work ships shims, adapters, or dual code paths that exist only for the transition.
You broke it in the other direction when breakage spreads to areas the plan did not name.
You followed it when the final state has no transition code and the full check passes, per [prove-it-works](prove-it-works.md).
Use this only for planned rewrites. For ordinary changes, keep every step green per [sequence-verifiable-units](sequence-verifiable-units.md).
