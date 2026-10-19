# Encode Lessons in Structure

**Apply when** you catch yourself writing the same instruction a second time, or you see the same correction come up again.

A repeated instruction is a sign that a rule belongs in structure, not in more text.
Turn the rule into something that runs. A lint rule, a test, a type, a runtime check, a schema, a script, or a metadata flag all work.
Structure catches the mistake every time. Text only works when someone reads it and remembers.
Put the structure in the project, next to the code it protects. Do not write it into the user's home configuration.
When you add the structural fix, remove the instruction it replaces. Keeping both splits the source of truth.
If the lesson needs judgment and cannot run as a check, make the instruction prominent and add an example of the failure it prevents.

You broke this when a review comment repeats a point that a lint or test could enforce.
You followed it when the same mistake now fails a check before anyone has to point it out.
This differs from [build-the-lever](build-the-lever.md), which builds tools for the task at hand. This one guards against a mistake that keeps coming back.
