# Prototype

Run this when an experiment can answer something you would otherwise ask the user. What you deliver is an answer. The scratch code that produced it is evidence, and it is never merged. If the answer leads to real work, that work starts over under the Feature playbook.

1. Write down what you are trying to learn, as a question with a few possible answers. "Does the table stay readable at 500 rows?" or "Is approach A or B under 200 ms?" If you cannot phrase it that way, there is nothing to prototype.
2. Use a scratch directory the session already provides, or one the user names. It stays outside production source.
3. Write only what the question needs. No tests, no abstractions, no polish. Use tools already in the project or on the machine.
4. If two or more approaches compete, give each its own clearly named folder or entry point so the results line up.
5. Look at the real output. Run it, print it, time it, or take a screenshot.
6. Let what you saw pick the answer. The scratch directory stays where it is.
7. Run the hand-off playbook (`hand-off.md`).

**Reply:** your recommendation first, then the question it answers, what you saw for each approach, the scratch path, and a plain note that none of this code ships.
