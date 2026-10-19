# Minimize Reader Load

**Apply when** you review or shape code that is hard to follow.

Good code costs a newcomer little effort. Two things drive that cost:
- **Hops.** How many files and functions a reader must open to answer one question.
- **Hidden state.** How much changing context they must keep in their head while reading.

To cut hops:
- Fold a wrapper into its only caller.
- Drop an interface that has a single implementation.
- Merge two layers when one just repeats the other's method names and arguments.
- Keep abstractions that hide a real decision behind a narrow entry point.

To cut hidden state:
- Return a value instead of mutating a shared one.
- Use a local variable instead of a field.
- Compute a value when needed instead of storing a copy that must be kept in sync.
- Validate a rule where data enters, and let everything downstream trust it.

Every new layer or field must save readers more effort than it costs them.

Try it on a stranger. Can they find where a value comes from, and what can change it, in about thirty seconds? This is the human version of [guard-the-context-window](guard-the-context-window.md). People run out of working memory too.
