# Migrate Callers, Then Delete Legacy APIs

**Apply when** you introduce a new internal API while callers of the old one still exist.

Move every caller to the new API and remove the old one in the same piece of work.
Do not keep a compatibility layer, a deprecated alias, or an adapter that forwards old calls to the new code.
Old and new paths living side by side double the surface and invite new callers to the wrong one.
Find every caller first. When there are many, change them with a script or codemod per [build-the-lever](build-the-lever.md).
Point the tests at what the new API promises. Remove tests that only pinned the internals of the old one.

This applies only when no outside users depend on the old API and the project can take a coordinated breaking change.
If outside users might depend on it, stop and ask the user how to handle the transition.
You followed this when a search for the old name returns nothing, and the full test suite passes.
Removing the old API is part of the code change the user asked for. It is not a cleanup of anything outside that change.
