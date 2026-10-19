# Boundary Discipline

**Apply when** you wire up validation, error handling, or adapters for a framework or external system.

Validate and parse input at the edge it comes in through. Past that edge, internal code relies on it.
Boundaries are command line arguments, config files, network input, and responses from external services.
At a boundary, validate, parse into domain types, and return clear errors.
Inside, pass typed data and let errors propagate. Do not check the same thing again.
Do not leak the boundary's private formats, such as wire types or storage rows, through the inner interface.
Put the business rules in plain functions with no framework imports. Keep the outer shell thin.

You broke this when null checks appear deep in a call chain for values the entry point already checked, or when business rules live inside a request handler.
Ask two questions. Is this data crossing a boundary right now? If not, the check is redundant. Could this logic be a pure function the shell calls? If so, extract it.
See [type-system-discipline](type-system-discipline.md) for turning parsed data into types the compiler enforces.
