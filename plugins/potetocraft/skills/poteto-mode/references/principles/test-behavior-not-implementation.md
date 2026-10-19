# Test Behavior, Not Implementation

**Apply when** you write, change, or decide whether to keep a test.

Each test asserts something the code promises to its callers, whether those are people or other systems.
Behavior is what those users can observe. Examples are what a call returns, which errors it raises, state a caller can query later, and side effects outside the process such as a request sent or a row written.
Implementation is what they cannot see, such as private helpers, the order of internal calls, and intermediate data.
Judge each test with two imagined edits.
First, break the behavior. Return a wrong value or skip an effect. A test that stays green here is worthless.
Second, restructure the internals while keeping every observable result. A test that breaks under this edit is coupled to internals.
Keep tests that catch the first edit and survive the second. Rewrite or remove the rest.
Call the code the way its users do, and feed it a specific input. The expected value comes from the spec, never from copying what the code printed.
Assert what the contract promises, no more and no less. An exact error message nobody reads is too much. The error type callers branch on is right.

Common hollow tests compare the code against its own output, assert on data the test built itself, or check only that some result exists.
