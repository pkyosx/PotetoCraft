# Laziness Protocol

**Apply when** you refactor, judge the size of a diff, or feel the pull to add an abstraction, a layer, or a parameter threaded through many calls.

Solve the problem with the smallest change that fully solves it.
Prefer removing code to adding it.
Reuse what the project already has before you write something new.
Make each decision in one place and pass the result along as a plain value.
When a condition causes trouble, remove the condition instead of building something that cleans up after it.
When a script would do, write the script, not a framework.

You broke this rule when the diff adds a helper with one caller, a flag threaded through five functions, or a config option nobody asked for.
You broke it when the same choice is made in three files.
You followed it when you cannot shrink the diff further without losing part of the fix.
Lazy means less total work for everyone later, not skipped verification. Still run [prove-it-works](prove-it-works.md).
