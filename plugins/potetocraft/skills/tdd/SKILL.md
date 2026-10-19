---
name: tdd
description: Write a failing test first, make it pass, then clean up. Use when the user asks for test-driven development, a red test first, or a regression test, and when a bug sits next to an existing test file that makes a quick local test easy.
---

# TDD

Turn the behavior you want into a test that runs. It must fail now and pass once the change is in.

## Decide first

Go ahead when the user asked for test-first work, a red test, or a regression test. Also go ahead when the bug sits in code that already has a nearby test file you can extend cheaply.

Do not write a new test, and tell the user why, if the only test you could write would:
- need a test harness the project does not have yet
- need the full stack, production-only state, or large unrelated fixtures
- mostly verify mocks, rely on sleeps and timing, or restate the implementation line by line

Skip it too when nobody can say exactly how to trigger the bug. In all of these cases, use the cheapest honest check you have, such as a small script, a command that shows the bug, or the app itself. No test beats a misleading one.

## The cycle, by example

Say a CSV splitter breaks `"Smith, Jr.",42` into three fields instead of two.

1. **Pin the gap.** Expected `["Smith, Jr.", "42"]`. Actual `["\"Smith", " Jr.\"", "42"]`. That one line is the smallest input that shows it.
2. **Find the home.** Add the case to the splitter's existing test file, the narrowest one that covers this code.
3. **Write the assertion.** Call the public split function and compare the returned list. Do not assert on internal helpers or on how many times something was called. See [test-behavior-not-implementation](../poteto-mode/references/principles/test-behavior-not-implementation.md).
4. **Watch it fail.** Run it. It should fail with the three field result, not with an import error or a typo. If it goes green, or breaks for an unrelated reason, fix the test before touching the splitter.
5. **Fix minimally.** Change the splitter just enough to respect quotes, without breaking the cases its other callers rely on.
6. **Watch it pass.** Rerun the test, then the tests around it.
7. **Tidy.** With everything green, clean up names or duplication you introduced. Rerun after each edit. Stop when it reads clearly, and do not expand into unrelated code.

## Hard rules

- Intermittent bug? Take the randomness or timing out of the test, and say which signal it now pins.
- Spot related cases? Mention them in the reply. This test lands alone first.
- Each test covers the one behavior it names. Extra coverage belongs in its own test.
- When code and test disagree about correct behavior, the code changes. The expectation stays.
- An existing assertion gets looser only if the intended behavior really changed. Explain the change when it does.

**Reply.** Which test or check you used, its failure before the change with the command and output, its pass after, and any other tests you ran. If you skipped the test, explain why and name the check you used instead.
