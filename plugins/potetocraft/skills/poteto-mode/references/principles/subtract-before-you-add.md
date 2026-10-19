# Subtract Before You Add

**Apply when** you plan the order of an addition, a refactor, or a rewrite.

Remove what is not needed first, then build on the smaller base.
Dead code, unused options, redundant checks, and stub references go before new code arrives.
Get to the minimum that works before you polish it.
Design for usage you have observed, not for edge cases you imagine.
Add no validator, parser, or guard the requirement does not call for.
If a section, reference, or instruction says nothing new, remove it instead of leaving a stub.
Aim to leave the design a little simpler than you found it, with the same or a smaller surface.

You broke this when new code works around old code that nobody uses.
You followed it when the removal is its own step, checked on its own, and the addition that follows is smaller because of it.
Removing code is part of the change the user asked for. It never means removing files outside that change.
