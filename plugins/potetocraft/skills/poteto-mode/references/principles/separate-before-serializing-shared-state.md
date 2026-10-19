# Separate Before Serializing Shared State

**Apply when** several processes, agents, or workers might write to one shared branch, key, file, or state record at once.

When two writers collide, the first question is not "which lock?" It is "why do they share a target?"

Example. Four build agents each append a result to `status.json`. Sometimes a result vanishes. The fix is not a lock around the file. Give each agent its own `status-<agent>.json` and let the reader merge them. No two writers ever touch the same bytes.

A quick test for whether writers are still sharing. Could one of them corrupt, truncate, or overwrite what another just wrote? Two agents updating different fields of one JSON file fail that test, because each one rewrites the whole file. Two agents with a file each cannot hurt each other.

Some targets must stay single, such as one release branch or one counter. Only then serialize, and let the code do it. A single process that owns all writes, an atomic compare and swap, phases that never overlap, or a lock file all work. A comment saying "only one at a time please" enforces nothing.

Intermittent bugs that involve two actors and one object are the classic sign this was missed. Since races rarely reproduce on demand, a design where they cannot happen is worth more than a careful guard.

You are done when every writable object has exactly one writer, or the shared one sits behind a mechanism the code itself enforces.
