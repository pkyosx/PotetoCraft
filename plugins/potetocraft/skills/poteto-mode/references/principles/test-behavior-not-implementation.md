# Test Behavior, Not Implementation

**Apply when** a test is being added, edited, or judged worth keeping.

A test is a promise written down. It should describe what someone outside the code relies on, and nothing else.

Outside observers can see return values, raised errors, data they can read back later, and effects that leave the process, such as a file on disk or an outgoing email. They cannot see helper functions, call order inside the module, or temporary structures. Tests that reach into the second group make every refactor painful.

Quick check for any test, using a date parser as the example:
- **Sabotage it.** Make `parse("2024-02-30")` return a date instead of an error. Does the test go red? If not, it protects nothing.
- **Reshuffle it.** Replace the regex inside with a hand-written scanner that gives the same answers. Does the test still pass? If not, it is tied to the inside.

A good test fails the sabotage and passes the reshuffle. For tests the current change touches, fix the ones that do not. Mention other weak tests in the report instead of removing them.

Write the test from the spec. Call the public entry point with a concrete input, and type the expected answer from what the behavior should be. Do not paste in whatever the code printed. Match the precision of the promise. If callers check the error class, assert the class. Do not pin the message text unless someone reads it.

Watch for tests that compare a function to itself, check only that something came back, or verify values the test itself put there.
