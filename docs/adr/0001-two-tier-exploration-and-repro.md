# Two tiers: a non-deterministic explorer and a frozen repro suite

TestGap's explorer is an LLM that writes TypeScript against a typed action library and runs it in a browser, choosing paths based on what a diff touched. That makes it deliberately non-deterministic, which is what gives it diff-targeted reach — but it also means a passing run proves nothing, and a bug found on Tuesday can walk back in on Friday when the explorer happens to look elsewhere.

So findings do not stop at a report. When the explorer finds a bug, the program that triggered it is reduced to minimal steps and saved as a standalone, deterministic test. That frozen repro runs forever afterwards with no model involved: fast, free, and identical every time.

## Considered options

**Explorer only.** Rejected. Every run starts from zero, so the tool never accumulates value — you pay a model to rediscover the same bugs at random, and nothing about the run is safe to gate a deploy on.

**Generate tests up front, model-based.** Rejected. This is what a state-machine path generator does, and the generated artifact becomes the thing people hand-edit, at which point the model rots. A repro is immune to this because it documents one specific bug rather than being a living test someone has to maintain.

## Consequences

Frozen repros live in the user's repository permanently, so generated code has to be readable by humans. That sets a quality bar on both the action API and the codegen prompt that an explorer-only design would not have imposed.
