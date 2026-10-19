# Guard the Context Window

**Apply when** your context is filling up with large outputs, long files, repeated reads, or plans for many parallel tasks.

An overfull context makes reasoning worse, loses detail when it gets compressed, and can stop the work.
Send bulk work to subagents. Give each one a narrow question and ask for a short summary back.
Keep summaries, decisions, and file paths in the main thread, not raw logs or whole files.
Read the part of a file you need, not the whole file. Search before you read.
Cap the output of commands, for example by filtering or taking only the tail, and save the full output to a scratch file you can search later.
Do not read the same large file twice. Write down what you learned the first time.
Size each phase of the work so it fits, and plan the next phase before the context is nearly full.
See the Subagents section of [the poteto-mode skill](../../SKILL.md) for how to spawn them.

You broke this when a full test log or a whole generated file sits in the main thread.
You followed it when the main thread holds only what you need to decide the next step.
