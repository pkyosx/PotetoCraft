# Separate Before Serializing Shared State

**Apply when** several processes, agents, or workers might write to one shared branch, key, file, or state record at once.

When two writers collide, the first question is not "which lock?" It is "why do they share a target?"

Example. Four build agents each append a result to `status.json`. Sometimes a result vanishes. The fix is not a lock around the file. Give each agent its own `status-<agent>.json` and let the reader merge them. No two writers ever touch the same bytes.

Check yourself:
- Writing different keys into the same file still counts as sharing the file.
- Writing separate files does not.

Only if one shared target is truly required should you serialize access. Use something the code enforces, such as a lock file, a single writer process, phases that run one after another, or an atomic compare and swap. A comment saying "only one at a time please" enforces nothing.

Intermittent bugs that involve two actors and one object are the classic sign this was missed. Since races rarely reproduce on demand, a design where they cannot happen is worth more than a careful guard.

You are done when every writable object has exactly one writer, or the shared one sits behind a mechanism the code itself enforces.
