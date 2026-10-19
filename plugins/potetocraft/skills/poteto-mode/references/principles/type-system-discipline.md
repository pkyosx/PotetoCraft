# Type System Discipline

**Apply when** you design types, review a function signature, or write code in a statically typed language.

Let the compiler reject impossible states, mixed-up values, and unhandled cases.
Shape types so that invalid combinations cannot be written, instead of adding handlers for them.
Give meaningful primitives their own types. A user id and an order id may both be strings, but they should not be swappable. Validate once when the value is created, then trust the type.
Treat external data as untyped until a parse function at the boundary turns it into your model, per [boundary-discipline](boundary-discipline.md).
Handle every variant of a union, and let the compiler flag a missing one.
When a schema file owns a shape, such as an API spec, a database migration, or a protocol definition, derive the type from it instead of writing a parallel copy, per [encode-lessons-in-structure](encode-lessons-in-structure.md).

You broke this when two parameters of the same primitive type can be passed in the wrong order without an error, or a switch has a default branch that hides new cases.
You followed it when the bug you worried about would fail to compile.
