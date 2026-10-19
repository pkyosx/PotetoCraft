# Separate Before Serializing Shared State

**Apply when** concurrent actors might write to the same file, branch, key, or state object.

First ask whether the actors really need the same writable object.
Usually they are each publishing their own facts. Give each actor its own file, key, or directory, and combine the results only where they are read.
Two workers writing different fields into one shared state file still share it. Two separate state files do not.
Only when one shared target is a real requirement, enforce order with structure. Use a lock file, sequential phases, a single owner that does all writes, or an atomic compare-and-swap.
A written instruction or a team convention is not concurrency control.
Treat "we need a lock" as a sign to recheck the design, not as the default answer.

You broke this when a bug appears only sometimes and two actors touch the same object.
You followed it when each writable object has exactly one writer, or the shared one is guarded by a mechanism the code enforces.
Races are hard to reproduce, so prefer designs where they cannot happen at all.
