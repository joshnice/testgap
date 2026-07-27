# The model may only call declared actions

The model never drives the browser directly. It composes scenarios exclusively from actions the project has declared, in TypeScript, and anything outside that vocabulary is unavailable to it. Where a capability is missing, the answer is to declare a new action — not to reach past the boundary.

This is the opposite bet to the rest of the AI QA space, which points unconstrained browser agents at applications and relies on the model to work out what to do. Unconstrained agents are slow, expensive, non-reproducible and impossible to typecheck. Constraint buys all four back: scenarios compile before they run, they serialise to readable repros, they replay identically, and there is no model in the loop once a repro is frozen.

The philosophy is borrowed from [Lakebed](https://docs.lakebed.dev/), which restricts what agents may do inside a capsule for the same reason — a smaller surface is a verifiable one.

## Consequences

The vocabulary is a hard ceiling on what TestGap can find. A bug reachable only through an interaction nobody declared an action for is invisible, and no amount of model capability changes that. Growing the vocabulary is therefore a permanent part of using the tool, not a one-off setup cost.
