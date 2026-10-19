# Lead judgment

Reviewers report candidates. You decide which ones the user sees. Run each candidate through four gates, in order, and stop at the first gate it fails.

1. **True?** Open the file at the cited line. Does the code really do what the finding says? If not, drop it.
2. **Reachable?** Trace the callers. Reviewers usually saw one slice, and you can see the whole chain. A finding like "this list could be empty" survives only if some caller can hand it an empty list past the existing types and validation.
3. **In scope?** The finding must concern lines this change touched or behavior it altered. A complaint about older code, or about a convention the repo follows deliberately, is out.
4. **Harmful?** Name the concrete damage. "I would have used a class here" names none. Neither does "pull this into a helper" unless a second, different use is clearly coming.

A finding that clears all four gates gets more weight when two reviewers with different lenses found it on their own, when it describes an actual sequence of calls, or when it changes what you believed about the code.

Be slow to drop anything about security or correctness. A missed real bug costs far more than the minutes spent confirming a false alarm.

If almost everything left is cosmetic, the change is likely in good shape. Tell the user that plainly instead of padding the list.

## Ranking

Order the survivors by what it would cost users if the change shipped as is.
- **Blocker.** Wrong behavior, lost data, a security hole, or a broken caller.
- **Should fix.** No harm today, but a real cost later.
- **Nit.** Take it or leave it.

Torn between two levels? Choose the more severe one and give your reason.
