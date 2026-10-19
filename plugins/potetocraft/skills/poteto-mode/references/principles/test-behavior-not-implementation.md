# Test Behavior, Not Implementation

**Apply when** you write, change, or decide whether to keep a test.

A test is a claim about what the code does for the people and systems that use it.
Behavior is what those users can observe. That covers return values, errors, state they can read back, and effects on outside systems such as a request sent or a row written.
Implementation is what they cannot see, such as private helpers, the order of internal calls, and intermediate data.
Judge each test with two imagined edits.
First, break the behavior. Return a wrong value or skip an effect. If the test still passes, it proves nothing.
Second, restructure the internals while keeping every observable result. If the test now fails, it is pinned to the implementation.
Keep tests that catch the first edit and survive the second. Rewrite or remove the rest.
Drive the code through the interface its users call, with a concrete input. Take the expected value from the requirement, not from a run of the code.
Assert what the contract promises, no more and no less. An exact error message nobody reads is too much. The error type callers branch on is right.

Common hollow tests compare the code against its own output, assert on data the test built itself, or check only that some result exists.
