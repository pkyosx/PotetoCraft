# Fix Root Causes

**Apply when** you debug.

Fix the place where the system first went wrong, not the place where the problem showed up.
Reproduce the failure before you change anything.
Ask why at each step until the answer is a wrong decision in the code, not a consequence of an earlier one.
When stuck, add instrumentation. Read the real error and the real state instead of guessing.
Ask whether the state that triggered the failure is legitimate. If it is, the code that broke on it needs to handle it. If it should never exist, find what produced it.
Guards, retries, swallowed errors, clamped values, and discarded state are the usual ways a bug gets hidden instead of fixed.
When something breaks only after a restart, look at persisted state first, such as config, caches, lock files, and saved state.
Look for the same fault elsewhere and fix every instance.
If a workaround needs a long comment to justify it, fix the code instead.
If the key fact took a long dig to find, propose a cheap signal that would have shown it right away.

You followed this when you can name the first wrong step and show the failing reproduction pass after the fix, per [prove-it-works](prove-it-works.md).
