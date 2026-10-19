# Attack the Premise

**Apply when** a second fix resting on the same belief has failed the same check as the first.

Scenario. A flaky upload test fails. You raise the timeout, and it still fails. You add a retry, and it still fails. Both fixes assumed "the server is slow." Two misses in a row say more about that assumption than about either fix.

So stop fixing and test the assumption:
1. State it in one sentence, the thing every attempt took for granted.
2. Choose an observation whose outcome depends on whether the sentence is true. In the scenario, log the server response time on each failing run.
3. Look at the pattern of failures, not just their size. Do they cluster on one file type, one machine, one time of day?
4. Save the check as a script so you can run it again, per [build-the-lever](build-the-lever.md).

Then follow the evidence:
- **The belief is false.** Ask what the failing cases have in common that the belief never accounted for.
- **The belief holds.** Your fixes treated a symptom. Keep tracing back, per [fix-root-causes](fix-root-causes.md).
- **The cause is a condition you can remove.** Remove it rather than adding code that works around it, per [laziness-protocol](laziness-protocol.md).

Before any third attempt, the report should show the belief in writing and the observation that confirmed or broke it.
