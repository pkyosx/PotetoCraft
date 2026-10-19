# Review rubric

What to check under each lens. Use the lenses that fit the change. A finding is a concrete problem on a real path, not a worry.

## Correctness

- Edge cases. Empty input, missing values, boundaries, very large input, unusual encodings.
- Errors. Are they handled, passed up, or swallowed without a trace?
- State. Races, stale values held in closures, references that outlive their owner.
- Reruns. What happens if this runs twice, or after a crash halfway through? If the answer depends on leftover state, a reconcile step is missing.
- Shared state. If several actors touch the same data, does structure serialize access, or only a convention?
- Trace before you flag. "This could be null" is a finding only when you show the call path that makes it null.

## Blast radius

Listing callers is the easy part. A search finds them in seconds. The job is the breakage a search does not show.

- Read the source of each library the change calls, at the version the project pins, including any local patch.
- Work out when things run. Async ordering, teardown, retries, background jobs, startup order.
- Follow the data past the symbol graph. JSON an API returns, a database column, a file format, a message on a queue, a config key, a feature flag, another service or language reading the same bytes.
- Look two or three hops downstream, not only at direct callers.
- Give each risk a real likelihood and a real cost. A search that finds nothing is an answer. Say what you searched. Never invent a caller or an API.

## Design and premise

- Does the change fix the cause or hide a symptom? Guards that mask a broken invariant, retries that hide a broken contract, casts that silence a modeling error.
- Is the fix in the right module? A patch in A may belong in B's contract.
- If the requirement had been known from day one, would the code look like this? If not, it is bolted on.
- Does it add a second way to do one task, or keep an old path alive with no outside users?
- Does it rely on a rule someone must remember, where a type, check, or test could make the wrong thing fail?
- Question the premise itself. Name a framing that would make the change smaller or unnecessary, if one exists. See [attack-the-premise](../../poteto-mode/references/principles/attack-the-premise.md).

## Code quality

- Look for a restructure that removes whole branches, helpers, modes, or layers while keeping behavior. Prefer removing complexity over moving it.
- Flag one-off conditionals dropped into unrelated flows. That is a design problem, not a style nit.
- Flag wrappers and pass-through helpers that add a layer and hide nothing.
- Flag loose types, needless optional fields, and casts where a clear boundary type would do. Validate data once where it enters, then trust it.
- Flag logic in the wrong layer and new helpers that duplicate an existing one.
- Flag a file that this change grows past roughly 1000 lines without a clear reason.
- Flag independent steps run in sequence for no reason, and related updates that can be left half applied.
- Do not ask for an abstraction with only one caller. Duplication is cheaper than the wrong abstraction.

## Tests

- A test should check what a caller or user can observe. It should not check private calls, call order, or mock wiring.
- Ask whether the test would fail if the behavior broke. Ask whether it would pass after a pure internal refactor. It should do both.
- A bug fix needs a test that fails without the fix.
- A change at an integration boundary needs the full path exercised at least once.
- Check the real value, not a proxy such as a timestamp or a cached copy.
- See [test-behavior-not-implementation](../../poteto-mode/references/principles/test-behavior-not-implementation.md).

## Comments

A comment earns its place only when it says one of these:

- A non-obvious why that the code cannot express, such as a constraint from an outside system, protocol, or vendor.
- A trap warning, such as an ordering requirement that breaks in a way tests will not catch.
- A consequence visible outside the code, such as a public API contract, a license header, or a link to a spec or issue that explains a constraint.

Flag everything else. Narration of what the next line does. Banners. Commented-out code. Change history. Long excuses for a workaround.

- When a comment explains a surprise in our own code, the fix is the code. Name the symbol to rename, extract, or retype so the surprise goes away.
- A lint or type suppression that silences a correctness or safety rule is a finding. Name the code that should change instead.
- "Do not remove" and "important" comments are claims. Check the claim against the code before you accept it. If it is true and about our own code, suggest a type, test, or check that enforces it.
