# Fix Root Causes

**Apply when** you debug.

Scenario. A CLI crashes with "cannot read property 'theme'" after an upgrade. Defaulting `theme` where it crashed would stop the crash. The real question is why the settings object lacks `theme`. Maybe the upgrade's migration skipped old files. That migration is where the fix goes.

**Smells of a symptom patch.** A new null check, a retry, a `catch` that logs and moves on, a value forced into range, or state quietly reset. Each can be right, but each can also bury the fault. A patch that needs a long comment to defend it is almost always in the wrong place.

**Getting to the cause:**
- Make it fail on demand before you edit anything.
- Look at the real error text and the real values. Add logging or a breakpoint instead of reasoning from memory.
- Walk the bad value backward, caller by caller, until you hit code that went wrong given correct inputs.
- Decide whether the triggering state is allowed. Allowed means the code that crashed must handle it. Not allowed means you fix whatever produced it.
- If the failure shows up only after a restart, check what persists between runs first, such as settings files, cache folders, lock files, or saved sessions.

**After the fix.** Search the codebase for the same mistake and fix every copy. If the cause was hard to find, suggest one cheap signal, such as a log line or an assertion, that would have pointed straight at it.

You followed this when you can name the first wrong step and show the reproduction failing before your change and passing after it, per [prove-it-works](prove-it-works.md).
