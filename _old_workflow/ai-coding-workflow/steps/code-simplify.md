# Code Simplify

**Skill name:** `code-simplify`

**Step type:** On-demand.

**Role:** Simplify recently changed code while preserving observable behavior and keeping feedback loops green.

**When to use:** Code works but became hard to read, review found unnecessary complexity, implementation mixed too many local decisions, speculative abstractions appeared, or a small cleanup would reduce review risk.

**Possible inputs:** Recent diff, commits, task spec, Spec, Technical Design, tests, verification results, reviewer findings, current feedback commands.

**Process:**

1. Confirm current behavior is already verified or has a reliable feedback loop.
2. Understand purpose, callers, edge cases, and test coverage before editing.
3. Classify the work as local simplification or structural refactor.
4. Simplify incrementally and rerun useful checks after meaningful changes.
5. Remove unnecessary indirection, speculative abstractions, dead local code, overly generic helpers, deep nesting, and unclear naming.
6. Record structural follow-ups as separate candidates or tasks.

**Rules:**

- Preserve exact observable behavior.
- Code Simplify is not architecture rescue; new seams, modules, or durable technical decisions are out of scope.
- Keep public interfaces stable unless interface cleanup is explicitly in scope.
- Behavior changes and structural refactors are out of scope; report them as separate candidates without applying them.

**Output:** Simplified code plus session verification report.

**Output location:** Recommended default: code changes in the repository and a concise session summary. If a PR or task issue exists, ask before publishing a short comment when simplification materially affects review or follow-up decisions. If the user does not confirm publication, keep the update in session only.

**Output template:**

```markdown
## Summary
<!-- Required. Paragraph, 1-3 sentences: what was simplified and the headline outcome. -->
<Simplification summary.>

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
<!-- Conditional. Bullet list: structural refactor candidate or separate task surfaced for later, without naming a destination step. -->
- <Follow-up.>
```

**Possible sizes:** lite (tiny cleanup inside one file); standard (local simplification after one task); full (focused pass on a small recent diff).

**Verification:** Previously useful feedback loops still pass, and the diff is smaller, clearer, or more local without behavior drift.

**Human gate:** Validate deletion of unclear code, public interface cleanup, or follow-ups that fall outside the simplification scope.
