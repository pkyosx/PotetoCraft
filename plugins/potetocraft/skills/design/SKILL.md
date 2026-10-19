---
name: design
description: Sketch data shapes, types, signatures, and module boundaries before writing code, compare options when there is no precedent, and keep the design honest while the code fills in. Use for "design this", "how should we structure this", "sketch the shape first", or any sizable change where writing code first would lock in a weak structure.
---

# Design

Settle the structure while it is still a page of stubs. Rewriting a sketch takes minutes. Unwinding code that grew on a bad structure takes days.

Keep the phases below in your harness's todo tool (TodoWrite in Claude Code) or in the reply.

## Learn the terrain

For each existing system the work will touch, use the How mode of the **explain** skill ([../explain/SKILL.md](../explain/SKILL.md)). When the design shifts who owns what, or moves logic between layers, add its Why mode too, so past reasons turn into known constraints instead of guesses. Only fully greenfield code with no neighbors can skip this.

## Write it from the outside in

1. **Call sites.** Write two or three realistic snippets of code that use the new thing. What do they import, what do they call, what do they get back? Everything else follows from these. If a later piece of the sketch makes these snippets awkward, change the sketch, not the snippets.
2. **Data.** The records, the states they move through, and the rules that always hold. Where the language allows, make a broken state unrepresentable. See [model-the-domain](../poteto-mode/references/principles/model-the-domain.md).
3. **Signatures.** Public functions and methods, with stub bodies such as `throw new Error("todo")` or pseudocode.
4. **Ownership.** Which module holds which state and makes which decisions, and where raw outside input becomes trusted domain types. See [boundary-discipline](../poteto-mode/references/principles/boundary-discipline.md).

A small change fits in one file. Larger work needs a module map and the key types, not more.

## Look for alternatives

If the codebase has already solved a problem like this, reuse that approach and name the file you took it from.

If it has not, draft two or three options that differ in their overall structure, for example an event log versus a mutable record versus a pair of tables. Give each one line of benefit and one line of cost. Lean toward the option that keeps the most behavior behind the smallest public surface. See [exhaust-the-design-space](../poteto-mode/references/principles/exhaust-the-design-space.md).

## Stress test each option

Assume whoever touches this next is an agent that opens three files, copies the nearest example, and stops once tests pass. A strong design makes that habit produce correct code. Ask of every option:

- Could someone outside the module import its private parts? Make that fail to build.
- Can a caller reach the same result by two different routes? Both routes will keep spreading.
- Do two modules both write, or both cache, the same state?
- Does a storage format, wire shape, or business rule appear in several modules, so one change means several edits?
- Must a caller call three methods in the right order to do one thing? The interface is too thin for its behavior.
- Are modules cut by phase, such as fetch, validate, write, each repeating the same knowledge? Cut by what they know instead.
- Does any layer just forward its arguments unchanged?
- Is the same list of items kept by hand in several files? Derive them from one, or fail the build when they drift.

Fix or drop an option that fails any of these.

## Write it up and decide

The design note has these parts:
- **Problem.** The goal and what makes its shape hard, including the constraints you found while learning the terrain.
- **Usage.** The call site snippets.
- **Shape.** Data, then signatures, then ownership. Which rules the types enforce, where input is validated, and what is out of scope on purpose.
- **Options.** Each one with its benefit and cost, and why the others lost. If only one shape worked, explain why.
- **Accepted tradeoffs.** One line each in the form "we give up X to get Y."
- **Open questions.** Worded so the user can answer them.
- **Recommendation.** Your choice and the first piece you would build.

When the decision is a product call or a costly architecture call, such as a public API, a data model, or ownership between modules, present the note and wait for the user to choose. Ask only what the code cannot answer. See [ask-only-what-only-the-human-can-answer](../poteto-mode/references/principles/ask-only-what-only-the-human-can-answer.md). When the decision is local and easy to reverse, state your choice and reason and keep going.

## Build to the sketch

Fill the stubs with real code. The agreed sketch is the contract. If the code wants something the sketch never planned, such as an extra parameter or a special bypass, pause and work out which one is mistaken. It could be the sketch, the requirement, or the code. Update the design when the code proves it wrong, and tell the user whenever the update touches something they chose.

## Know when to start over

A single clumsy case is normal. A recurring pattern means the shape is wrong. Signs include:
- the same workaround in places that have nothing to do with each other
- one special branch after another for unrelated edge cases
- casts, `any`, or optional fields that are always filled, just to compile
- a lock showing up in state the sketch said nobody shares
- callers that need to understand the module's internal rules

Then return to the terrain step with the new facts and design as though you had known them from the start. Cut the sketch smaller than before, and only then let it grow. See [redesign-from-first-principles](../poteto-mode/references/principles/redesign-from-first-principles.md) and [subtract-before-you-add](../poteto-mode/references/principles/subtract-before-you-add.md). Show the user the new design before building more.

**Reply.** The design note with its recommendation. Once building starts, also list each place the code departed from the sketch and how the design changed.
