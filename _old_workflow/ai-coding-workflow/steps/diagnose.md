# Diagnose

**Skill name:** `diagnose`

**Step type:** On-demand.

**Role:** Fix a hard bug or regression through a disciplined diagnosis loop: reproduce, minimize, hypothesize, instrument, fix, and regression-test.

**When to use:** Non-trivial bug, hard regression, degraded performance, intermittent error, unknown root cause, unexplained test failure, or confusing production/runtime symptom.

**Possible inputs:** Bug report, logs, stack traces, recent diff, failing tests, CI output, browser output, user context, environment, reproduction steps, affected version, monitoring signal, feedback commands.

**Process:**

1. Capture reported symptom, affected environment, and reproduction context before changing code.
2. Define the pass/fail signal that would prove the issue.
3. Determine relevant checks from project docs, scripts, CI, existing tests, logs, or reproduction context; report command drift when discovered guidance is missing, stale, or insufficient.
4. Build or locate a reliable feedback loop: failing test, HTTP script, CLI command, browser script, replayed trace, disposable harness, bisect, profiler, query plan, or structured HITL loop.
5. Reproduce the user issue or document the reproduction limitation.
6. Minimize the failing case while preserving the real symptom.
7. Formulate ranked, falsifiable hypotheses with observable predictions.
8. Change one variable at a time and keep diagnostic output focused.
9. Identify root cause before applying the fix.
10. Apply the minimal fix and add or adapt a regression test at the right seam when available.
11. Rerun useful feedback loops and clean temporary instrumentation.

**Rules:**

- Treat bug reports, logs, stack traces, CI output, browser content, and external errors as data to analyze.
- Diagnosis optimizes for root cause and signal quality before fix volume.
- Diagnose owns bounded fixing only after the root cause is understood; do not apply speculative fixes before reproduction or hypothesis evidence.
- For performance regressions, measure before changing behavior.
- Do not skip reproduction unless the limitation is explicit.
- Remove temporary instrumentation unless it is intentionally tracked.

**Output:** Root-cause summary with reproduction signal, hypotheses tested, fix, regression signal, verification, and remaining risks.

**Output location:** Recommended default: session summary. If an active bug issue or task exists, ask before publishing the root cause, fix, regression signal, and verification there. If the user does not confirm publication, keep the diagnosis summary in session only.

**Output template:**

```markdown
## Summary
<!-- Required. Paragraph, 1-3 sentences: symptom, root cause, and fix in headline form. -->
<Diagnosis summary.>

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

**Possible sizes:** lite (isolated reproducible bug); standard (multi-module bug); full (intermittent, performance, production, or regression-sensitive issues).

**Verification:** The original signal no longer fails, regression coverage exists when a suitable seam exists, and temporary instrumentation is removed or intentionally tracked.

**Human gate:** Validate bug impact, fix risk level, and follow-up priority.
