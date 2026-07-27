# Targeting a run is deliberately imprecise

A run is scoped by what changed, from two inputs: the git diff against the branch being merged into, and an optional plain-English brief from the developer (`testgap "I have added a create map object tool which adds shapes as circles"`). Either works alone; together they are stronger.

Matching changes to actions is left to the model reading names and descriptions, rather than to declared path mappings or measured coverage. Precision is not the goal and would in fact be the wrong goal: a change to layer creation breaks things in object creation, undo/redo and saving, so a run must cover the blast radius rather than the edited file. Approximate matching gets that for free; precise matching would actively exclude it.

The brief is not only a targeting hint. It is the only statement of *intent* TestGap ever receives — a diff says what the code now does, never what it was supposed to do. It is therefore the primary source for the assertions described in [ADR 0002](./0002-what-counts-as-a-finding.md).

## Consequences

Measured coverage — learning which files each action touches at runtime — remains the better long-term mapping and is left open. It is not worth building before there is evidence that sharper targeting changes what gets found.
