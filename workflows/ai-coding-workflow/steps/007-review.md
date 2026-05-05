# 007 - Review

**Skill name:** `review`

**Step type:** Core workflow step (recommended).

**Role:** Evaluate code independently from implementation, prioritizing bugs, regressions, risks, and deviations from the agreed contract.

**When to use:** Any non-trivial task, complex logic, sensitive change, architecture, security, performance, migration, or need for a fresh review.

**Possible inputs:** Diff, commits, PR, PRD, task spec, Tech Design, tests, verification results, project standards.

**Process:**

1. Start from a fresh review mindset, ideally a fresh context.
2. Understand intended behavior before judging implementation.
3. Compare code against PRD, task spec, Tech Design, and task-level acceptance criteria.
4. Review tests and verification evidence.
5. Focus review on correctness, regressions, scope drift, security, performance, accessibility, migrations, dependencies, and config when triggered.
6. Check for secrets, accidental config changes, missed migrations, and out-of-scope edits.
7. Verify that tests cover real behavior and important edge cases.
8. State findings first, ordered by severity, with file/line references when possible.
9. Report unreviewed areas or confidence level when useful.

**Rules:**

- `Review` evaluates code. It is not manual QA.
- Do not silently fix code before stating findings.
- Findings are the primary output; summaries are secondary.
- Prioritize bugs, risks, behavioral regressions, and contract deviations over style preferences.

**Output:** Findings-first code review verdict in session, PR comment, or tracker comment.

**Output location:** Check `.agents/workflow/output-locations.md` when it exists. Recommended default: session review. If a PR exists, use a PR review/comment when useful; if an active task issue exists, use a tracker comment when coordination matters.

**Output template:**

```markdown
## Verdict
<!-- Required. Single line. -->
Approved / Changes requested / No findings

## Findings
<!-- Required. Findings-first bullet list. Use `No findings` when empty. -->
- **Critical:** `<file>:<line>` - <Bug or release blocker.>
- **Important:** `<file>:<line>` - <Likely defect, regression, or contract deviation.>
- **Suggestion:** `<file>:<line>` - <Optional improvement with clear value.>

## Verification Reviewed
<!-- Required. Bullet list: tests, commands, CI, browser checks, or evidence reviewed. -->
- <Verification evidence reviewed.>

## Residual Risks
<!-- Conditional. Bullet list: unreviewed area, confidence note, or remaining risk. -->
- <Residual risk or unreviewed area.>
```

**Possible sizes:** Short review for a simple diff; standard review for a normal task; focused deep review for security, performance, migration, public API, or architecture-sensitive changes.

**Verification:** The review makes a clear verdict and ties findings to specific behavior, files, lines, tests, or risks.

**Human gate:** Accept the task, request fixes, or route back to `Build`.
