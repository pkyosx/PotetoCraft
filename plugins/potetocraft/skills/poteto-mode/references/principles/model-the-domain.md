# Model the Domain

**Apply when** code holds state, grows many branches, or repeats one assumption about a data shape in several files.

Let the data carry the rules. When the shape is right, impossible cases cannot be written and many `if` statements disappear.

Example. A video player tracks `isLoading`, `isPlaying`, and `hasError` as three booleans. Nothing stops all three from being true. Replace them with one `status` field whose values are `loading`, `playing`, `paused`, and `failed`. Now the bad combination cannot exist.

Common swaps:
| Instead of | Prefer |
| --- | --- |
| booleans that must agree | one enum or a state machine |
| a long list of positional arguments | a typed record or struct |
| the same `switch` in five files | a single table or registry keyed by kind |
| modules named after steps such as parse and save | modules named after one concept they own |

If no pattern fits, list the states that must never occur and the ways the data gets read. Choose the shape that makes exactly those true.

Getting the shape right on day one is cheap. Fixing it later turns into a refactor that keeps slipping. Still, do not reshape code that is small, readable, and not growing.

The sign of success is that the next new case is one more row in a structure, not one more branch in the code.
