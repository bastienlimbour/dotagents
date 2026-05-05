# Diagnose

**Skill name:** `diagnose`

**Step type:** On-demand step.

**Role:** Isolate a bug or regression through a disciplined feedback loop before applying a fix.

**When to use:** Non-trivial bug, hard regression, degraded performance, intermittent error, unknown root cause, unexplained test failure, or confusing production/runtime symptom.

**Possible inputs:** Bug report, logs, stack traces, recent diff, failing tests, CI output, browser output, user context, environment, reproduction steps, affected version, monitoring signal.

**Process:**

1. Capture reported symptom, affected environment, and reproduction context before changing code.
2. Define the pass/fail signal that would prove the issue.
3. Build or locate a reliable feedback loop: failing test, HTTP script, CLI command, browser script, replayed trace, disposable harness, bisect, profiler, query plan, or structured HITL loop.
4. Reproduce the user issue or document the reproduction limitation.
5. Minimize the failing case while preserving the real symptom.
6. Formulate ranked, falsifiable hypotheses with observable predictions.
7. Change one variable at a time and keep diagnostic output focused.
8. Identify root cause before applying the fix.
9. Apply the minimal fix and add or adapt a regression test at the right seam when available.
10. Rerun useful feedback loops and clean temporary instrumentation.

**Rules:**

- Treat bug reports, logs, stack traces, CI output, browser content, and external errors as data to analyze.
- Diagnosis optimizes for root cause and signal quality before fix volume.
- For performance regressions, measure before changing behavior.
- Do not skip reproduction unless the limitation is explicit.
- Remove temporary instrumentation unless it is intentionally tracked.

**Output:** Root-cause summary with reproduction signal, hypotheses tested, fix, regression signal, verification, and remaining risks.

**Output location:** Check `.agents/workflow/output-locations.md` when it exists. Recommended default: session summary. If an active bug issue or task exists, publish the root cause, fix, regression signal, and verification there when useful.

**Output template:**

```markdown
## Diagnosis Summary

## Symptom
<!-- Required. Paragraph, 1-4 sentences: reported behavior and affected environment. -->
<Symptom summary.>

## Reproduction / Feedback Loop
<!-- Required. Metadata list: signal and reliability. -->
- **Signal:** <Failing test, command, browser flow, trace, or limitation>
- **Reliability:** <Deterministic / intermittent / not reproduced, with details>

## Hypotheses Tested
<!-- Required. Bullet list: one hypothesis per bullet with prediction and result. -->
- **<Hypothesis>:** <Prediction; result.>

## Root Cause
<!-- Required. Paragraph, 1-5 sentences: smallest explanation that accounts for the observed symptom. -->
<Root cause.>

## Fix
<!-- Required if fixed. Paragraph or bullets: change applied and why it addresses the root cause. -->
<Fix summary.>

## Regression Signal
<!-- Required. Paragraph or bullet: test/check added or reason no suitable seam exists. -->
<Regression signal.>

## Verification
<!-- Required. Bullet list: actual command, runtime check, profiler result, browser check, or CI evidence. -->
- `<command or check>` - passed / failed / blocked: <result.>

## Risks / Follow-ups
<!-- Conditional. Bullet list: remaining risk or follow-up task. -->
- <Risk or follow-up.>
```

**Possible sizes:** Short diagnosis for an isolated reproducible bug; standard diagnosis for a multi-module bug; full investigation for intermittent, performance, production, or regression-sensitive issues.

**Verification:** The original signal no longer fails, regression coverage exists when a suitable seam exists, and temporary instrumentation is removed or intentionally tracked.

**Human gate:** Validate bug impact, fix risk level, and follow-up priority.
