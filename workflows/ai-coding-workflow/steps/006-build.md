# 006 - Build

**Skills:** `implement`, `implement-tdd`

**Step type:** Core workflow step (required).

**Role:** Implement one vertical slice or task within its Execution Contract and verify the result with real feedback.

**When to use:** For each task spec, or directly from a minimal single-task PRD or any input with a sufficient Execution Contract.

**Possible inputs:** Minimal PRD, task spec, Tech Design, ADRs, repository context, project instructions, relevant source files, relevant tests, feedback commands.

**Process:**

1. Confirm a sufficient Execution Contract: scope, behavior, acceptance criteria, dependencies, non-goals, and verification.
2. Load only useful artifacts, project rules, source files, tests, and one similar implementation pattern when available.
3. Check worktree state and avoid touching unrelated changes.
4. Detect real feedback commands from project docs, scripts, CI, or existing tests.
5. Check official docs when framework or library behavior is version-sensitive.
6. Prepare a proportionate implementation plan; self-approve clear `AFK` tasks and request validation for `HITL` decisions.
7. Identify the test seam before coding when `implement-tdd` is used.
8. Implement the plan while staying inside the Execution Contract.
9. Debug through the most relevant feedback loop.
10. Run useful verification: tests, typecheck, lint, build, browser checks, reproduction, or task-specific commands.
11. Compare the implementation with task-level acceptance criteria before finalizing.

**Rules:**

- If the Execution Contract is insufficient, route back to `PRD`, `Tech Design`, `Slice`, `Grill Me`, or `Grill With Docs`.
- Stay inside the Execution Contract and avoid unrelated changes.
- Clear `AFK` tasks may proceed with self-approval; `HITL` decisions need human validation before implementation.
- For `implement-tdd`, apply a behavior-by-behavior red-green-refactor loop: write a failing test, confirm it fails for the right reason, implement the minimum fix, refactor after green, and rerun useful feedback loops.
- Tests should verify behavior through public interfaces, ideally in an integration style with real code paths.
- Mocks are most useful at true system boundaries: external APIs, time, randomness, filesystem, or remote services.

**Output:** Implemented code plus final session response with verification status, deviations, and remaining risks.

**Output location:** Check `.agents/workflow/output-locations.md` when it exists. Recommended default: code changes in the repository and a concise session summary. Publish tracker/task updates only when the project convention or user request calls for it.

**Output template:**

```markdown
## Build Summary
<!-- Required. Bullet list: concise description of implemented changes. -->
- <Change made.>

## Verification
<!-- Required. Bullet list: actual commands or runtime checks run, with result. -->
- `<command>` - passed / failed / blocked: <result or blocker.>

## Contract Check
<!-- Required. Bullet list: acceptance criteria status and deviations. -->
- <Acceptance criterion or behavior> - satisfied / deviated / blocked: <note.>

## TDD Evidence
<!-- Conditional. Bullet list: include only when implement-tdd was used. -->
- <Failing test observed, passing test observed, and refactor state.>

## Risks / Blockers
<!-- Conditional. Bullet list: remaining ambiguity, blocker, or risk. Omit if none. -->
- <Risk or blocker.>
```

**Possible sizes:** Direct build for a clear small task; standard build for a normal AFK task; TDD build for bug fixes, business logic, sensitive behavior, or regression risk; HITL build for public interfaces, migrations, or ambiguous behavior.

**Verification:** Report actual commands or runtime checks run, their results, blockers, and any deviations from the Execution Contract. For bug fixes, include the reproduction or regression signal. For frontend work, include browser/runtime evidence when feasible.

**Human gate:** Validate the implementation plan for a `HITL` task. Clear `AFK` tasks may proceed with self-approval.
