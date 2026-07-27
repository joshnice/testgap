# A finding must be falsifiable

TestGap accepts a finding from two sources only. **Built-in signals** — unhandled errors, failed network requests, error boundaries, crashes, hangs — need no authoring and are on by default. Deliberately not console errors, which are too polluted by third-party noise to be a trustworthy signal.

**Model-raised findings** must be falsifiable: the model may suspect anything, but nothing is recorded as a finding until it has written a concrete assertion that fails. A suspicion the model cannot express as a failing check is not reported as a finding.

This is not primarily about hallucination, though it does filter them. Shrinking re-runs a program many times asking "does this still reproduce?", and that predicate has to be cheap and deterministic. Model judgement is neither — it costs a model call per evaluation and can answer differently on identical input. A concrete assertion is both, and it doubles as the assertion inside the saved repro.

## Consequences

The model will sometimes notice something genuinely wrong and fail to express it as a clean assertion, and that signal is dropped rather than reported. This is accepted: a tool that cries wolf gets uninstalled, and unfalsifiable findings cannot be shrunk or frozen anyway.
