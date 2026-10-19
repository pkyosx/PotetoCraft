# Build the Lever

**Apply when** the work is anything beyond a couple of obvious edits, including migrations, analyses, and checks.

Build the tool that does the work or proves it, instead of doing it by hand.
A codemod, generator, script, or rerunnable query gives the same result every time and costs nothing to run again.
A reviewer can read the tool and rerun it. Hand edits can only be checked by doing them again.
Do the first unit by hand to learn the recipe. Then write the tool, run it on that unit, and compare with your hand version.
Make the tool safe to run twice, per [make-operations-idempotent](make-operations-idempotent.md).
If one script can handle every unit, run it yourself instead of fanning out subagents to apply edits by hand.
When you do fan out, write the recipe, the check, and the files not to touch in one shared instruction file that the subagents read but cannot edit.
Keep the smallest tool that does the job, per [laziness-protocol](laziness-protocol.md).

Keep the tool with the work and mention it in the report so the user can rerun it.
If you cite this principle and there is no script, codemod, generator, or shared instruction file to point to, you did not apply it.
For recurring rules, see [encode-lessons-in-structure](encode-lessons-in-structure.md). For scripted checks, see [prove-it-works](prove-it-works.md).
