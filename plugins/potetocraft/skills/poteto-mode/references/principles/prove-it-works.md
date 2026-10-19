# Prove It Works

**Apply when** you have finished a task and are about to call it done.

Check the real result directly. Do not rely on a proxy, a self-report, or the fact that it compiles.
Run the feature, read the actual value, and look at the actual diff.
Check that a process is alive by asking the process, not by reading a file it once wrote.
Read the live value, not a cached copy or a value derived from it.
When a check fails, suspect the way you observed before you suspect the system.
The strongest proof is a small script that repeats the comparison and prints the result. Write it, run it, and keep its output.
Keep the script and its output in the session's scratch directory, or with the work when it is large, and point to them in the report.

You skipped this when the report says "should work" or "tests pass" without showing which check ran and what it printed.
You followed it when a reviewer can rerun your check and see the same thing.
For numbers, also apply [explain-the-number](explain-the-number.md).
