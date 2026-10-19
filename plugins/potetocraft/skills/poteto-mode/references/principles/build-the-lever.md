# Build the Lever

**Apply when** the work is anything beyond a couple of obvious edits, including migrations, analyses, and checks.

If a job has more than a handful of repetitions, write a small program that does it or checks it. Then run the program.

Why a tool beats hand work:
- It does the same thing on unit 1 and unit 300.
- Running it again is free, so you can rerun after every fix.
- A reviewer can read twenty lines of script. Nobody can audit three hundred hand edits without redoing them.

How to build one:
1. Handle unit one manually and write down each step.
2. Turn those steps into a script, query, generator, or codemod.
3. Run it on that same unit and diff its result against your hand version.
4. Make it safe to rerun, per [make-operations-idempotent](make-operations-idempotent.md).
5. Keep it as small as the job allows, per [laziness-protocol](laziness-protocol.md).

One script that covers every unit beats a crowd of subagents each editing by hand. If you do split the work across subagents, give them one shared recipe file that holds the steps, the check, and the paths they must leave alone. They read it. They do not change it.

Leave the tool next to the work and name it in the report so the user can run it too. Claiming this principle with no script, query, codemod, or recipe file to show means it was not applied.

Related: [encode-lessons-in-structure](encode-lessons-in-structure.md) for rules that keep coming back, [prove-it-works](prove-it-works.md) for checks.
