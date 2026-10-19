# Make Operations Idempotent

**Apply when** you design a command, a lifecycle step, or a processing loop that may crash, restart, or retry.

The goal is a step you can run again at any moment without fear. A rerun after success is a no-op. A rerun after a crash finishes the job.

Picture a script that turns a folder of photos into thumbnails. A version that says "make a thumbnail for every photo" redoes all the work and breaks on a half-written file. A better version asks which thumbnails are missing or wrong, and makes only those.

Questions to put to each step, with what a good answer looks like:

| Question | Good answer |
|---|---|
| What does it act on? | The difference between what should exist and what does now. |
| How does it know a thumbnail is done? | It checks content, such as a hash or a stored size. A timestamp or the order files arrived can mislead. |
| Can a reader ever see half a file? | No. Output is written under a temporary name and renamed into place in one move. |
| A crashed run left a lock, a partial file, or a job marked "working". What now? | Each leftover carries proof of whether its owner is gone, such as a process ID or a start time with an age limit. That proof holds no matter where the old run stopped. |

If you cannot say what a second run would do, the step needs a reconcile phase before it acts.

Done means you ran the step twice in a row, and once more after killing it partway, and all three ended in the same state.
