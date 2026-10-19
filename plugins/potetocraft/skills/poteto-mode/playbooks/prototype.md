# Prototype

You own the decision, not the code. A prototype is a throwaway instrument. It settles an empirical question so you do not have to ask the user one. The real build follows the Feature playbook.

1. State the one question the prototype answers (which layout, which approach, how fast, what the output looks like). No question means no prototype.
2. Pick a scratch directory the session already provides, or one the user names. Keep it apart from production source.
3. Build the smallest thing that answers the question. Use only tools already in the project or on the machine. Skip tests, abstractions, and polish.
4. When comparing options, build each variant and label it so they can be compared side by side.
5. Observe the result directly. Run it, print the output, time it, or capture a screenshot.
6. Decide from the observation. Leave the scratch directory in place.
7. Run the hand-off playbook (`hand-off.md`).

**Reply:** the question, the variants tried, what you observed, what you recommend, and the scratch path. State clearly that the prototype code is not meant to ship.
