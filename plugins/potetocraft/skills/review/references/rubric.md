# Review rubric

Checks for each lens in the review skill. Use only the lenses the change calls for. Report a problem only when you can show the path that reaches it. A vague worry is not a finding.

## Correctness

Ask these, and show the call path for any "yes":
- What does it do with nothing, with one item, at the limit, with a huge input, with odd characters such as emoji or a byte order mark?
- When a call fails, does the error surface, travel up, or vanish silently?
- Can two things race? Can a callback hold an old value, or keep a reference after its owner is gone?
- Run it twice, or kill it halfway and run it again. Same result? If that depends on leftovers, the change lacks a reconcile step.
- If several workers touch one piece of data, is ordering enforced by code or only by a convention?

Example of the bar. "`user.email` may be undefined" becomes a finding only when you name the caller that passes a user without one.

## Blast radius

Finding direct callers takes one search. The real work is finding what a search misses:
- **Dependencies.** Read the source of each library call at the version the project pins, including any local patches.
- **Timing.** Startup order, teardown, retries, background jobs, and the order async work settles in.
- **Data that travels.** An API's JSON, a database column, a file format, a queue message, a config key, a feature flag, or a separate program, perhaps in another language, that parses the same output.
- **Distance.** Follow effects two or three hops out, not just one.

For every risk, give an honest likelihood and cost. An empty search result is a valid answer, so say what you searched. Never invent callers or APIs that you did not find.

## Design and premise

- Is the root cause fixed, or is a symptom muted? Watch for a guard over a broken invariant, a retry over a broken contract, or a cast over a modeling mistake.
- Does the fix live in the module that owns the problem? A patch in the caller may really belong in the callee's contract.
- Would someone who knew this requirement from the start have written it this way? If not, it was bolted on.
- Does it introduce a second way to do something, or keep an old path alive that nobody outside uses?
- Does correctness depend on someone remembering a rule that a type, check, or test could enforce?
- Is there a framing that would shrink the change or make it unneeded? See [attack-the-premise](../../poteto-mode/references/principles/attack-the-premise.md).

## Code quality

Prefer changes that delete complexity over ones that move it. Look for a reshaping that removes whole branches, flags, modes, or layers and keeps behavior. Then flag:
- a special case for one caller wedged into a shared flow, which is a design issue rather than style
- a wrapper or helper that only forwards and hides nothing
- loose types, optional fields that are never absent, and casts where one boundary type would do, since input should be validated where it enters and trusted after
- logic placed in the wrong layer, or a new helper that duplicates one that exists
- a file this change pushes past roughly 1000 lines with no clear reason
- independent work done in sequence for no reason, or related writes that can be left half done

Do not request an abstraction for a single caller. Some duplication is cheaper than a wrong abstraction.

## Tests

See [test-behavior-not-implementation](../../poteto-mode/references/principles/test-behavior-not-implementation.md).
- Assertions target what callers or users observe, not private calls, call order, or mock wiring.
- Break the behavior on purpose in your head. The test should fail. Restructure the internals. It should still pass.
- A bug fix comes with a test that fails without the fix.
- A change at an integration boundary is exercised end to end at least once.
- Assertions read the real value, not a timestamp or cached copy standing in for it.

## Comments

A comment should stay only if it records one of these:
- a reason the code cannot show, such as a quirk of an external API or protocol
- a warning about a trap tests will not catch, such as a required call order
- a consequence beyond the code, such as a public contract, a license header, or a link to the spec or issue behind a constraint

Flag the rest, including narration of the next line, section banners, commented-out code, change logs, and long apologies for a workaround.

- If a comment explains something surprising in our own code, fix the code instead. Name the symbol to rename, split, or retype.
- A suppression that turns off a correctness or safety lint or type rule is itself a finding. Name the code that should change.
- Treat "do not remove" and "important" comments as claims to check. If one holds and concerns our own code, suggest a type, test, or check that enforces it.
