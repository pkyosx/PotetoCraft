# Guard the Context Window

**Apply when** big command output, long files, rereads, or a plan with many parallel tasks start to crowd your context.

Your context is a budget. Spending it on raw output makes later reasoning worse, loses detail when the history is compressed, and can halt the session.

Habits that keep it lean:
- **Search, then read a slice.** Use grep or a symbol search to find the lines, then open only that range.
- **Trim command output.** Pipe through `tail`, `grep`, or a line limit. Write the full output to a scratch file so you can search it later.
- **Take notes once.** After reading a big file, write down the facts you need so you never open it again.
- **Delegate bulky reading.** Give a subagent one narrow question and ask for a few lines back. [The poteto-mode skill](../../SKILL.md) explains spawning under its Subagents heading.
- **Plan in chunks.** Size each phase so it fits, and write the next phase's plan while room remains.

What belongs in the main thread is decisions, file paths, and short summaries. A full test log or a generated file pasted there is the mistake this principle exists to stop.
