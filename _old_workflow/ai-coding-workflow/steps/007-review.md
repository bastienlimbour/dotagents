# 007 - Review

**Skill name:** `review`

**Step type:** Core, recommended.

**Role:** Evaluate code independently from implementation, prioritizing bugs, regressions, risks, and deviations from the agreed contract.

**When to use:** Any non-trivial task, complex logic, sensitive change, architecture, security, performance, migration, or need for a fresh review.

**Possible inputs:** Diff, commits, PR, Spec, task spec, Technical Design, tests, verification results, project standards.

**Process:**

1. Start from a fresh review mindset, ideally a fresh context.
2. Understand intended behavior before judging implementation.
3. Compare code against Spec, task spec, Technical Design, and task-level acceptance criteria.
4. Review tests and verification evidence.
5. When independent verification is needed, determine relevant checks from project docs, scripts, CI, existing tests, or current task context; report command drift when discovered guidance is missing, stale, or insufficient.
6. For high-risk changes, run or request independent verification instead of relying only on reported evidence.
7. Focus review on correctness, regressions, scope drift, security, performance, accessibility, migrations, dependencies, and config when triggered.
8. Check for secrets, accidental config changes, missed migrations, and out-of-scope edits.
9. Verify that tests cover real behavior and important edge cases.
10. Check whether the implementation invalidates Spec, Technical Design, task specs, future tasks, or durable docs.
11. State findings first, ordered by severity, with file/line references when possible.
12. Report unreviewed areas or confidence level when useful.

**Rules:**

- `Review` evaluates code. It is not manual QA.
- Do not silently fix code before stating findings.
- Findings are the primary output; summaries are secondary.
- Prioritize bugs, risks, behavioral regressions, and contract deviations over style preferences.
- Use risk-based independent verification for migrations, security-sensitive changes, core flows, public APIs, and high-blast-radius changes.
- Report contract drift and surface needed artifact updates instead of treating them as review style notes.

**Output:** Findings-first code review verdict in session, PR comment, or tracker comment.

**Output location:** Recommended default: session review. Ask before publishing a PR review/comment or tracker comment. If the user does not confirm publication, keep the review in session only.

**Output template:**

```markdown
## Summary
<!-- Required. Paragraph, 1-3 sentences: what was reviewed and the headline verdict. -->
<Review summary.>

## Findings
<!-- Required. Findings-first bullet list. State `No findings` when empty. -->
- **Critical:** `<file>:<line>` - <Bug or release blocker.>
- **Important:** `<file>:<line>` - <Likely defect, regression, or contract deviation.>
- **Suggestion:** `<file>:<line>` - <Optional improvement with clear value.>

## Verdict
<!-- Required. Single line. -->
Approved / Changes requested

## Verification Reviewed
<!-- Required. Bullet list: tests, commands, CI, browser checks, or evidence reviewed. -->
- <Verification evidence reviewed.>

## Contract Drift / Artifact Updates
<!-- Required. Bullet list: state `None` or describe the contract drift, artifact update, or durable documentation update needed (without naming a destination step). -->
- None / <Contract drift, artifact update, or durable documentation update needed.>

## Residual Risks
<!-- Conditional. Bullet list: unreviewed area, confidence note, or remaining risk. -->
- <Residual risk or unreviewed area.>
```

**Possible sizes:** lite (simple diff); standard (normal task); full (security, performance, migration, public API, or architecture-sensitive changes).

**Verification:** The review makes a clear verdict and ties findings to specific behavior, files, lines, tests, or risks.

**Human gate:** Accept the task, request fixes, or block release.
