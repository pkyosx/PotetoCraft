# Fix Root Causes

**Apply when** you debug.

Scenario. A CLI crashes with "cannot read property 'theme'" after an upgrade. Defaulting `theme` where it crashed would stop the crash. The real question is why the settings object lacks `theme`. Maybe the upgrade's migration skipped old files. That migration is where the fix goes.

**Is your fix a muffler?** Ask what your change does to the evidence. If it makes the error disappear without explaining it, the fault is still there and will surface somewhere else. Typical mufflers include a value forced back into range, state reset when it looks odd, a `catch` that logs and moves on, a retry, or a new null check. Any of them can be correct. Each needs a reason that names the cause. When defending the patch takes a long comment, the patch is in the wrong place.

**Getting to the cause:**
- Make it fail on demand before you edit anything.
- Look at the real error text and the real values. Add logging or a breakpoint instead of reasoning from memory.
- Walk the bad value backward, caller by caller, until you hit code that went wrong given correct inputs.
- Decide whether the triggering state is allowed. Allowed means the code that crashed must handle it. Not allowed means you fix whatever produced it.
- A bug that needs a restart to appear points at something that survives the restart. Look first at what the program saved last time, such as a session store, a database file, a pid or lock file, or anything under its cache folder.

**After the fix.** The same mistake likely sits elsewhere, so search for it and fix each copy. When the hunt was long, propose one cheap, permanent signal, such as an assertion or a log line, that would have named the cause at once.

You followed this when you can name the first wrong step and show the reproduction failing before your change and passing after it, per [prove-it-works](prove-it-works.md).
