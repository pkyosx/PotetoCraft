# Prove It Works

**Apply when** you have finished a task and are about to call it done.

"Done" is a claim about the world. Back it with something you observed in the world, not with a signal that usually tracks it.

Weak evidence and what to do instead:
- **It compiles.** Execute it and watch the behavior you changed.
- **The log says it started.** Query the running service, for example hit its health endpoint.
- **A status file says ready.** Ask the process itself. A file can outlive the thing that wrote it.
- **The cache shows the new value.** Read from the source of truth.
- **I expect the diff is right.** Open the diff and read it.

When an observation disagrees with your expectation, first check how you observed. A wrong port, a stale build, or the wrong environment is more common than a broken system.

The best proof is a short script that performs the comparison and prints pass or fail. Run it and keep what it printed. Store both in the session's scratch directory, or beside the work if they are large, and link them in the report.

A report that says "should work" with no command and no output has not proved anything. A reviewer should be able to rerun your check and see the same result. When the result is a number, also apply [explain-the-number](explain-the-number.md).
