# Build the Lever

**Apply when** the work is anything beyond a couple of obvious edits, including migrations, analyses, and checks.

If a job has more than a handful of repetitions, write a small program that does it or checks it. Then run the program.

Scenario. Forty test files still import a helper from its old path. Editing them by hand takes an hour and leaves a reviewer forty diffs to trust. A twenty line codemod takes fifteen minutes, and the reviewer reads the codemod instead. When a 41st file turns up next week, you run it again.

How to build one:
1. Fix the first unit by hand, noting every step you take.
2. Encode those steps as a script, query, generator, or codemod. Keep it as small as the job allows, per [laziness-protocol](laziness-protocol.md).
3. Make sure a second run changes nothing, per [make-operations-idempotent](make-operations-idempotent.md).
4. Point it at the unit you did by hand and diff the two results. Any difference is a bug in the script.
5. Run it on everything else.

Fanning the job out to subagents who each edit by hand is the weaker choice when one script could cover it all. If the work truly must be split, write one recipe file for every subagent with the steps, the check, and the paths that are off limits. Subagents read it and never edit it.

Leave the tool next to the work and name it in the report so the user can run it too. Claiming this principle with no script, query, codemod, or recipe file to show means it was not applied.

Related: [encode-lessons-in-structure](encode-lessons-in-structure.md) for rules that keep coming back, [prove-it-works](prove-it-works.md) for checks.
