# Exhaust the Design Space

**Apply when** the codebase has nothing to copy for a new interface behavior or a structural choice you must make.

With no local precedent, your first idea is just the first one you had. Generate rivals before you commit.

Steps:
1. Write down what "good" means here before you see any option. Speed of use, error recovery, code size, whatever fits.
2. Make two or three sketches that differ in approach. A dropdown versus a search box versus inline chips is a real spread. Three shades of dropdown is not.
3. Keep them throwaway. A static HTML page, a stub component, or a fifty line script is plenty.
4. You may write them yourself or give each sketch to a subagent. [The poteto-mode skill](../../SKILL.md) explains spawning under its Subagents heading.
5. Score every sketch against the criteria from step 1, side by side.
6. Choose one and record why each loser lost.

This pays off most when the answer depends on how something feels in use, not only on whether its logic is correct.

The report should show the sketches, the criteria, and the reasoning. If the choice comes down to product taste, bring it to the user, per [ask-only-what-only-the-human-can-answer](ask-only-what-only-the-human-can-answer.md).
