# Attack the Premise

**Apply when** a second fix resting on the same belief has failed the same check as the first.

Scenario. A flaky upload test fails. You raise the timeout, and it still fails. You add a retry, and it still fails. Both fixes assumed "the server is slow." Two misses in a row say more about that assumption than about either fix.

Stop fixing. Put the belief on trial instead.

**The charge.** Write the belief in one sentence. In the scenario, "uploads fail because the server responds slowly."

**The evidence.** Pick a measurement that would read differently if the sentence were false. Here, log the server's response time on every failing run. Then sort the failures by what they share, such as file type, machine, or time of day. A cluster often tells you more than an average. Keep the check as a script so it can run again, per [build-the-lever](build-the-lever.md).

**The verdict.**
- **Something you can take away caused it.** Take it away instead of writing code that copes with it, per [laziness-protocol](laziness-protocol.md).
- **The belief was wrong.** The failing runs share something it never mentioned. Find that.
- **The belief was right.** The fixes so far were aimed at a consequence. Trace one step further back, per [fix-root-causes](fix-root-causes.md).

Before any third attempt, the report should show the belief in writing and the observation that confirmed or broke it.
