# Minimize Reader Load

**Apply when** you review or shape code that is hard to follow.

Code is maintainable when a reader can understand it with little effort. Measure that effort on two axes.
The first is layers, the number of hops between a question and its answer.
The second is state, the hidden or changing context the reader must keep in mind.
Inline wrappers with one caller and adapters with only one implementation.
Merge a layer into its neighbor when it only mirrors the neighbor's methods and parameters.
Prefer interfaces that hide a real decision behind a small surface.
Shrink the scope of state. Prefer return values to mutation, locals to fields, and derived values to values kept in sync.
State an invariant once at the boundary, not in every consumer.
A new layer or new state must pay for itself. It should remove more reading effort than it adds.

The test is a new reader answering "where does this value come from?" and "what can change it?" in about half a minute.
This is the human side of [guard-the-context-window](guard-the-context-window.md). Readers have finite working memory too.
