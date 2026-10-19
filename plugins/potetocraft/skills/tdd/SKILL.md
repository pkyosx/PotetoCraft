---
name: tdd
description: Write a failing test first, make it pass, then clean up. Use when the user asks for TDD, a failing test, or a regression test, or when a bug has an obvious, cheap local test target.
---

# TDD

Make the wanted behavior executable before you change production code. The test fails before the change and passes after it.

## When to use it

- The user asks for TDD, a failing test, or a regression test.
- A bug has an obvious, cheap test target that already exists, such as a unit or integration test file for that code path.

## When to skip it

Skip the new test and say why when any of these hold.

- No test path is obvious, and building one would mean new harness setup.
- The test would need slow end-to-end infrastructure, production-only state, or large unrelated fixtures.
- The test would mostly check mocks, depend on timing, or copy the current implementation.
- The reproduction steps are vague.

Then use the closest cheap check instead. A focused script, a command that reproduces the bug, or a run of the app. A missing test is better than a bad one.

## Red

1. State the intended behavior, the current behavior, and the smallest input that shows the gap.
2. Pick the narrowest test file the project already uses for that code path.
3. Write one focused test. It asserts what a caller or user can observe. Return values, output, stored data, visible state. Not private calls or call order. See [test-behavior-not-implementation](../poteto-mode/references/principles/test-behavior-not-implementation.md).
4. Run it. Confirm it fails, and fails for the reason you expect. If it passes, or fails for another reason, fix the test before touching production code.

## Green

5. Make the smallest production change that gives the intended behavior and keeps nearby contracts.
6. Run the test again. Confirm it passes. Run the nearby tests too.

## Refactor

7. With the test green, simplify the code you touched. Remove duplication and awkward names you introduced.
8. Run the tests after each change. Stop when the code is clear. Do not widen the scope.

## Guardrails

- Never change a test to match wrong behavior.
- Never weaken an existing assertion unless the expected behavior truly changed. Say why when it did.
- Keep the test about this behavior. No unrelated coverage.
- For a flaky bug, make the test deterministic and say what signal it locks down.
- If the bug belongs to a wider class, land the focused test first. Then mention sibling cases worth covering.

**Reply.** The test or check you used, the failure it showed before the change (with the command and output), the passing run after, and other tests you ran. If you skipped the test, say why and what you used instead.
