# Lead judgment

How the lead decides which findings reach the user.

## Verify first

Open the cited code for every finding. If the line does not say what the finding claims, drop it. If the failure path cannot be reached, drop it. Reviewers see a slice. You can read the whole call chain.

## Common false positives

- **Filler.** A reviewer with nothing serious to say inflates nits. If every finding is a nit, the code is probably fine. Say so.
- **Hypothetical input.** "What if this is null?" counts only if a caller can pass null. Check validation upstream and the types.
- **Early abstraction.** A request to extract an interface or helper counts only if the code must change in a second way soon.
- **Taste.** "I would do it differently" without a concrete harm is not a finding.
- **Missing context.** Findings about code the change did not touch, or about a pattern the rest of the repo uses on purpose.

## Signs a finding is real

- It names a concrete path, not a possibility.
- Two reviewers with different lenses reached it separately.
- It shows a gap in your own picture of the code.
- You read it and think "yes, that would happen."

Give security and correctness findings extra care before you drop one. Dropping a real bug costs more than checking a false one.

## Ranking

Rank by cost to users if it ships. A blocker breaks behavior, loses data, opens a security hole, or breaks a caller. A should-fix adds real cost later. A nit is optional. When unsure between two ranks, pick the higher one and say why.
