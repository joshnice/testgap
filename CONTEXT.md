# TestGap

TestGap is an automated QA engineer for applications. Developers declare a typed library of actions; a model composes those actions into programs, runs them in a browser, and reports what broke.

## Language

**Action**:
A single typed operation a developer has declared, which the model may call to drive the application. Actions are the only vocabulary the model has — it cannot touch the browser directly. Every action carries its own assertion that it succeeded, so an action is both a way to move and a way to check.
_Avoid_: Step, command, tool

**Scenario**:
A chain of actions the model has composed, forming one complete program to run against the application.
_Avoid_: Test, case, path

**Exploration Run**:
One session in which the model writes and executes programs looking for bugs, scoped by what a set of changes touched. Deliberately non-deterministic — two runs over identical code will explore differently.
_Avoid_: Test run, scan, crawl

**Finding**:
A defect an exploration run surfaced, together with the evidence that it is real.
_Avoid_: Failure, issue, bug report

**Brief**:
A plain-English description of what the developer changed and what they intended it to do, given at the start of a run. The only statement of intent TestGap receives — a diff shows what the code does, never what it was meant to do.
_Avoid_: Prompt, description, spec

**Glossary**:
An optional document in the project describing what the application's own domain terms mean, which the model reads before composing scenarios. Types say what may be called; the glossary says what it means. Accumulates over time rather than being written up front.
_Avoid_: Manifest, vocabulary, docs

**Repro**:
The shortest sequence of actions that still triggers a finding, saved as a standalone deterministic test. Once saved, a repro runs without any model involvement.
_Avoid_: Regression test, reproduction steps, minimal case

**Setup**:
Developer-supplied work that brings the application to a usable starting point, by creating something new rather than wiping what is already there — a fresh map, a fresh account, a fresh list.
_Avoid_: Reset, teardown, seed

**Cleanup**:
Developer-supplied work that removes debris left by earlier runs. Runs at the start of a run rather than the end, so a crashed run is recovered from rather than compounded, and only ever removes what TestGap itself created.
_Avoid_: Teardown, reset
