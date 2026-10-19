---
name: design
description: Sketch data shapes, types, signatures, and module boundaries before writing code, compare options when there is no precedent, and keep the design honest while the code fills in. Use for "design this", "how should we structure this", "sketch the shape first", or any sizable change where coding first would fix a poor structure in place.
---

# Design

Decide the shape before the code. A sketch is cheap to change. Code built on the wrong shape is not.

Track the phases with a todo list (TodoWrite in Claude Code, or the equivalent in your harness).

## 1. Ground

Learn every system the new code touches. Use the How mode of the **explain** skill ([../explain/SKILL.md](../explain/SKILL.md)) on each one. If the design moves ownership or layering, also use its Why mode so the old reasons become constraints, not guesses.

Skip this only for greenfield code with nothing around it.

## 2. Sketch

Write the caller's view first. Show what a caller imports, what it calls, and what comes back, in two or three realistic call sites. Derive everything else from that. When the sketch and the usage disagree, fix the sketch.

Then sketch, in this order:

1. **Data shapes.** The records, states, and invariants. Make illegal states impossible to write where the language allows it. See [model-the-domain](../poteto-mode/references/principles/model-the-domain.md).
2. **Types and signatures.** Public functions and methods with bodies left as `not implemented` or pseudocode.
3. **Module boundaries.** Which module owns which state and which decisions. Where outside data is parsed into domain types. See [boundary-discipline](../poteto-mode/references/principles/boundary-discipline.md).

Keep the sketch small. One file for a small change. A module map plus types for larger work.

## 3. Options

If the repo already solves this kind of problem, follow that precedent and say which file it comes from.

If there is no precedent, sketch two or three structurally different options. Different whole shapes, not small variations of one. For each, give one line on what it gets right and one line on what it costs. Prefer the option that hides the most behind the smallest public surface. See [exhaust-the-design-space](../poteto-mode/references/principles/exhaust-the-design-space.md).

## 4. Check red flags

Picture the next contributor as an agent with a narrow view. It reads a few files, imitates whatever code sits closest, and stops at the first version that builds. A good design makes the change that looks right from one file correct for the whole repo. Revise or reject an option that shows any of these.

- **Shallow module.** A wide interface over little behavior. Callers must call several methods in order to finish one task.
- **Leaked decision.** A storage format, wire type, or policy appears in more than one module, so a change needs edits in several places.
- **Split by time.** Separate load, check, change, and save modules that each repeat the same knowledge. Group by what a module knows, not when it runs.
- **Pass-through layer.** A method that forwards the same arguments to another method and adds nothing.
- **Shared ownership.** Two modules write the same state or keep their own copy.
- **Two ways to do one task.** Agents copy whichever they find first, so both keep growing.
- **Reachable internals.** Outside code can import a module's private parts. Make that import fail.
- **Hand-synced lists.** The same items listed in several places. Keep one list and derive the rest, or make the build fail when they disagree.

## 5. Present and decide

Write the design up with these parts.

- **Problem.** What we are doing and what makes the shape non-obvious. Name the constraints from step 1.
- **Usage.** The caller's view from step 2.
- **Shape.** Data first, then signatures, then boundaries. Which invariants live in types and where validation happens. What the design deliberately does not do.
- **Options.** Each option from step 3 with its gain and its cost, and why the losers lost. If only one shape fit, say why.
- **Tradeoffs accepted.** One line each, written as "we accept X to get Y."
- **Open questions.** Phrased as questions the user can answer.
- **Recommendation.** Your pick and the first thing you would build.

If the choice is a product call or an architecture call (public API, data model, ownership between modules, anything costly to reverse), present the design and wait for the user to choose. Ask only what the code cannot settle. See [ask-only-what-only-the-human-can-answer](../poteto-mode/references/principles/ask-only-what-only-the-human-can-answer.md).

If the choice is local and cheap to reverse, state the pick and the reason, then continue.

## 6. Build against the sketch

Replace `not implemented` bodies with real code. The agreed sketch is the contract. When the code needs something the sketch did not plan, such as a new parameter or an escape hatch, stop and ask which is wrong. The sketch, the requirement, or the code.

Revise the design when the code disagrees with it. Tell the user what changed and why when the change touches anything they chose in step 5.

## 7. Redesign when the shape is wrong

One awkward case does not condemn a design. A pattern does. Watch for these.

- The same workaround showing up in unrelated places.
- Many unrelated edge cases that each need a special branch.
- Types that need casts, `any`, or always-set optional fields to compile.
- A lock appearing where the sketch said state was not shared.
- Callers needing to know the module's internal rules.

When you see a pattern, go back to step 1 with what you learned. Redesign as if the new facts were known on day one. Shrink the sketch below its old size first, and only then let it expand. See [redesign-from-first-principles](../poteto-mode/references/principles/redesign-from-first-principles.md) and [subtract-before-you-add](../poteto-mode/references/principles/subtract-before-you-add.md). Present the new design to the user before building further.

**Reply.** The design write-up from step 5 with the recommendation, then, once building starts, each deviation from the sketch and how the design changed.
