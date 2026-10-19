# Encode Lessons in Structure

**Apply when** an instruction you already gave once is about to be written again, or a correction you have seen before shows up once more.

Saying the same thing twice is the signal. The second time, stop writing prose and build something that enforces it.

Ways to enforce, roughly from strongest to weakest:
- a type that cannot hold the bad value
- a test or lint rule that fails the build
- a schema or runtime assertion
- a script or a metadata flag that tooling reads

Prose depends on someone reading and remembering. An enforcement fires on every run whether anyone remembers or not.

Where it goes. In the project, beside the code it protects. Never in the user's home configuration.

What to remove. Once the check exists, delete the old written instruction it replaces, so there is one source of truth.

When no check is possible because the lesson needs judgment, write it down next to the code where the mistake happens, with a short example of the mistake.

Evidence that it worked is simple. The next time the mistake happens, a check fails before a person has to say anything.

This is about mistakes that recur. Tools for finishing the current task belong to [build-the-lever](build-the-lever.md).
