# 006 - Build

**Skills:** `implement`, `implement-tdd`

**Status:** Required core step.

**Role:** Implement a task while staying within scope and planning execution before writing code.

**When to use:** For each task spec, or directly from a minimal single-task PRD or any input with a sufficient Execution Contract.

**Possible inputs:** Minimal PRD, task spec, `tech-design.md`, ADRs, repository context, project instructions.

**Actions:**

- start from a clean context and only the strictly useful artifacts
- verify the scope, Execution Contract, and worktree state without modifying unrelated changes
- prepare a proportionate implementation plan (Plan mode / Read only)
- confirm public interface changes and priority behaviors to test when the task is non-trivial
- identify the test seam before coding when `implement-tdd` is used
- implement the plan while staying in scope
- use red-green-refactor when `implement-tdd` is selected
- debug when needed
- run required verification: tests, typecheck, lint, build, or specific commands
- if a check fails, fix it or document the blocker before expanding scope
- verify compliance with the Execution Contract

**Output:** implemented code + session report.

**Report publication:** No artifact file is created by default. If an active sub-issue, tracker issue, or PR exists, propose publishing the final report there with changes, checks run, and blockers. In local Markdown mode, keep the report in session unless the user explicitly asks to add it to the task spec.

**Output contents:**

Build Preflight:

- selected approach
- likely areas or files when useful
- planned tests and checks
- risks or clarifications needed for a `HITL` task

Final report:

- changes made
- tests and checks run
- verification result
- final status
- remaining ambiguities or blockers

Avoid:

- detailed log of every micro-action
- exhaustive file inventory without review value
- scope expansion to fix adjacent issues

**Possible sizes:** very short plan for an obvious task, detailed plan for a sensitive or HITL task.

**Implementation plan:** always present but adapted to the scope and task. It may require human validation (HITL) or be self-approved (AFK).

An `AFK` task may be self-approved only if dependencies, checks, and success criteria are explicit. A blocked or ambiguous task remains `HITL` until resolved.

**Skill choice:** `implement` for integration, UI, glue code, and configuration. `implement-tdd` for bug fixes, business logic, sensitive behavior, or high regression risk.

**Human gate:** validate the implementation plan for a `HITL` task. Self-approval is allowed for a clear `AFK` task.

**Important:** If the Execution Contract is insufficient, route back to `PRD`, `Tech Design`, `Slice`, `Grill Me`, or `Grill With Docs`.

#### TDD red-green-refactor

`implement-tdd` applies a behavior-by-behavior loop:

1. write a failing test that expresses the expected behavior
2. confirm the test fails for the right reason
3. implement the minimum needed to make it green
4. refactor only after reaching a green state
5. rerun useful feedback loops

Do not write all tests and then the full implementation. That is a horizontal slice. The correct loop is vertical: one test, one behavior, minimal implementation, then the next behavior.

Tests should verify behavior through public interfaces, ideally in an integration style with real code paths. Avoid tests coupled to internals, excessive mocks, private-method tests, and after-the-fact tests that only confirm the implementation.

Mocks: only at system boundaries when useful: external APIs, time, randomness, filesystem, or database if no practical local substitute exists. Do not mock internal modules you control. Prefer a DB test, in-memory adapter, or local substitute when it gives a more realistic signal.

Prefer specific interfaces for external operations over a generic fetcher that is hard to test.
