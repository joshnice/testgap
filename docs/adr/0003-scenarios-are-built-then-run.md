# Scenarios are built in full, then run

A scenario is assembled as a complete chain of actions before anything touches the browser. The model writes the whole program, hands it over, and only then does it execute.

The reason is shrinking. A built-first scenario is a plain list of actions, so reducing a finding to minimal steps means dropping entries from that list and re-running — a few lines of code. Were scenarios to execute as they were written, there would be no list to reduce, only code that already ran, and shrinking would mean rewriting a TypeScript AST. The same list also serialises straight back out as the saved repro.

Chains are still built with ordinary TypeScript, so loops and conditionals remain available to the model when composing — they simply run at build time and flatten into the resulting list.

## Consequences

The model cannot react to what it sees partway through a scenario. There is no "if the dialog appeared, do X" — it writes blind, runs, reads the result, and adapts in the *next* scenario. Reacting happens between scenarios, never inside one.

Whether the model may have several scenarios in flight at once is a configuration option. With parallelism off, it writes one and waits.
