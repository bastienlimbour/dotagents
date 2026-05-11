# 006 - Build

**Skill name:** `implement`

**Step type:** Core, required.

**Role:** Implement one vertical slice or task within its Execution Contract and verify the result with real feedback.

**When to use:** For each task spec, or directly from a minimal single-task Spec or any input with a sufficient Execution Contract.

**Possible inputs:** Minimal Spec, task spec, Technical Design, ADRs, repository context, project instructions, relevant source files, relevant tests, feedback commands.

**Process:**

1. Confirm a sufficient Execution Contract: scope, behavior, task-level acceptance criteria, edge cases, non-goals, verification, known feedback commands, `blocked-by` dependencies, `AFK | HITL` type when useful, and likely touchpoints without a detailed implementation plan.
2. Load only useful artifacts, project rules, source files, tests, and one similar implementation pattern when available.
3. Check worktree state and avoid touching unrelated changes.
4. Determine real feedback commands from the Execution Contract, project docs, scripts, CI, or existing tests; report command drift when discovered guidance is missing, stale, or insufficient.
5. Check official docs when framework or library behavior is version-sensitive.
6. Prepare a proportionate implementation plan; self-approve clear `AFK` tasks and request validation for `HITL` decisions.
7. Identify the test seam before coding when the `tdd` mode applies.
8. Implement the plan while staying inside the Execution Contract.
9. Debug through the most relevant feedback loop.
10. Run useful verification: tests, typecheck, lint, build, browser checks, reproduction, or task-specific commands.
11. Compare the implementation with task-level acceptance criteria before finalizing.
12. Report contract drift, artifact updates needed, or confirm that no upstream artifact or durable documentation update is needed.

**Rules:**

- If the Execution Contract is insufficient, do not start; report what is missing.
- Stay inside the Execution Contract and avoid unrelated changes.
- Clear `AFK` tasks may proceed with self-approval; `HITL` decisions need human validation before implementation.
- If implementation reveals a scope, behavior, Spec, or Technical Design change, stop expanding scope and report the contract drift.
- The `tdd` mode applies a behavior-by-behavior red-green-refactor loop: write a failing test, confirm it fails for the right reason, implement the minimum fix, refactor after green, and rerun useful feedback loops. Use `tdd` for bug fixes, business logic, sensitive behavior, or regression risk.
- Tests should verify behavior through public interfaces, ideally in an integration style with real code paths.
- Mocks are most useful at true system boundaries: external APIs, time, randomness, filesystem, or remote services.

**Output:** Implemented code plus final session response with verification status, deviations, and remaining risks.

**Output location:** Recommended default: code changes in the repository and a concise session summary. Ask before publishing any tracker or task update. If the user does not confirm publication, keep the update in session only.

**Output template:**

```markdown
## Summary
<!-- Required. Paragraph, 1-3 sentences: what was implemented and the headline verification status. -->
<Build summary.>

## Changes
<!-- Required. Bullet list: concise description of implemented changes. -->
- <Change made.>

## Verification
<!-- Required. Bullet list: actual commands or runtime checks run, with result. -->
- `<command>` - passed / failed / blocked: <result or blocker.>

## Contract Check
<!-- Required. Bullet list: acceptance criteria status and deviations. -->
- <Acceptance criterion or behavior> - satisfied / deviated / blocked: <note.>

## Contract Drift / Artifact Updates
<!-- Required. Bullet list: state `None` or describe the contract drift, artifact update, or durable documentation update needed (without naming a destination step). -->
- None / <Contract drift, artifact update, or durable documentation update needed.>

## TDD Evidence
<!-- Conditional. Bullet list: include only when the tdd mode was used. -->
- <Failing test observed, passing test observed, and refactor state.>

## Risks / Blockers
<!-- Conditional. Bullet list: remaining ambiguity, blocker, or risk. Omit if none. -->
- <Risk or blocker.>
```

**Possible sizes:** lite (clear small task); standard (normal AFK task); full (HITL task touching public interfaces, migrations, or ambiguous behavior).

**Modes:** `direct` (default), `tdd` (red-green-refactor loop for bug fixes, business logic, sensitive behavior, or regression risk).

**Verification:** Report actual commands or runtime checks run, their results, blockers, and any deviations from the Execution Contract. For bug fixes, include the reproduction or regression signal. For frontend work, include browser/runtime evidence when feasible.

**Human gate:** Validate the implementation plan for a `HITL` task. Clear `AFK` tasks may proceed with self-approval.
