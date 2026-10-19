# Minimize Reader Load

**Apply when** you review or shape code that is hard to follow.

Code is maintainable when a reader can understand it with little effort. Measure that effort on two axes.
The first is layers, the number of hops between a question and its answer.
The second is state, the hidden or changing context the reader must keep in mind.
Inline wrappers with one caller and adapters with only one implementation.
Collapse a layer that repeats the same methods and arguments as the layer next to it.
Prefer interfaces that hide a real decision behind a small surface.
Shrink the scope of state. Prefer return values to mutation, locals to fields, and derived values to values kept in sync.
State an invariant once at the boundary, not in every consumer.
Before you add a layer or a piece of state, ask whether it saves the reader more than it costs.

The test is a new reader answering "where does this value come from?" and "what can change it?" in about half a minute.
This is the human side of [guard-the-context-window](guard-the-context-window.md). Readers have finite working memory too.
