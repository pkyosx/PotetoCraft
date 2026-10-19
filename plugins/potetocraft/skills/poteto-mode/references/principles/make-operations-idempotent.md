# Make Operations Idempotent

**Apply when** you design a command, a lifecycle step, or a processing loop that may crash, restart, or retry.

The goal is a step you can run again at any moment without fear. A rerun after success is a no-op. A rerun after a crash finishes the job.

Picture a script that turns a folder of photos into thumbnails. A version that says "make a thumbnail for every photo" redoes all the work and breaks on a half-written file. A better version asks which thumbnails are missing or wrong, and makes only those.

Build each step that way:
- Look at what exists now. Decide what should exist. Act only on the gap.
- Expect leftovers from a run that died halfway, such as a half-written output, a held lock, or a queue item marked in progress. Give each one a marker that tells the next run it is abandoned, such as an owning process ID or an age limit, and make that marker trustworthy at every point the old run could have stopped.
- Produce outputs under a temporary name and move them to the final name in one step, so a reader never sees half a file.
- Decide "already done" by checking the content, such as a hash or a field value. A file date or an arrival order can lie.

If you cannot say what a second run would do, the step needs a reconcile phase before it acts.

Done means you ran the step twice in a row, and once more after killing it partway, and all three ended in the same state.
