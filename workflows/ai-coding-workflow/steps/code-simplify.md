# Code Simplify

**Skill name:** `code-simplify`

**Step type:** On-demand step

**Role:** Simplify recently changed code while preserving observable behavior and keeping feedback loops green.

**When to use:** Code works but became hard to read, review found unnecessary complexity, implementation mixed too many local decisions, speculative abstractions appeared, or a small cleanup would reduce review risk.

**Possible inputs:** Recent diff, commits, task spec, PRD, Tech Design, tests, verification results, reviewer findings, current feedback commands.

**Process:**

1. Confirm current behavior is already verified or has a reliable feedback loop.
2. Understand purpose, callers, edge cases, and test coverage before editing.
3. Classify the work as local simplification or structural refactor.
4. Simplify incrementally and rerun useful checks after meaningful changes.
5. Remove unnecessary indirection, speculative abstractions, dead local code, overly generic helpers, deep nesting, and unclear naming.
6. Record structural follow-ups as separate candidates or tasks.

**Rules:**

- Preserve exact observable behavior.
- `Code Simplify` is not architecture rescue.
- New seams, modules, or durable technical decisions belong in `Improve Codebase Architecture` and `Tech Design`.
- Keep public interfaces stable unless interface cleanup is explicitly in scope.
- Route behavior changes back to `Build` and structural refactors to `Improve Codebase Architecture`.

**Output:** Simplified code plus session verification report.

**Output location:** Check `.agents/workflow/output-locations.md` when it exists. Recommended default: code changes in the repository and a concise session summary. If a PR or task issue exists, publish a short comment only when simplification materially affects review or follow-up decisions.

**Output template:**

```markdown
## Simplification Summary

## Simplifications Made
<!-- Required. Bullet list: changes that reduced complexity while preserving behavior. -->
- <Simplification made.>

## Behavior Preserved
<!-- Required. Bullet list: behavior or acceptance criteria checked. -->
- <Behavior or acceptance criteria checked.>

## Verification
<!-- Required. Bullet list: actual command, test, build, browser check, or blocker. -->
- `<command or check>` - passed / failed / blocked: <result.>

## Follow-ups
<!-- Conditional. Bullet list: structural refactor candidate or separate task. -->
- <Follow-up.>
```

**Possible sizes:** Tiny cleanup inside one file; local simplification after one task; focused simplification pass on a small recent diff.

**Verification:** Previously useful feedback loops still pass, and the diff is smaller, clearer, or more local without behavior drift.

**Human gate:** Validate deletion of unclear code, public interface cleanup, or escalation into structural refactor.
