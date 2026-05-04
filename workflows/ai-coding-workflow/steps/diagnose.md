# Diagnose

**Skill:** `diagnose`

**Status:** On-demand step.

**Role:** Diagnose a complex bug or regression with a disciplined loop before fixing it.

**When to use:** Non-trivial bug, hard regression, degraded performance, intermittent error, unknown root cause, unexplained test failure.

**Possible inputs:** bug report, logs, stack traces, recent diff, failing tests, user context, environment, reproduction steps.

**Actions:**

- record environment, reproduction command, and reproduction reliability
- first build a reliable feedback loop: failing test, HTTP script, CLI command, browser script, replayed trace, disposable harness, fuzz/property loop, bisect, or structured HITL loop
- improve the loop: faster, more deterministic, more precise signal
- reproduce the user issue or document why it cannot be reproduced
- minimize the failing case without losing the real symptom
- formulate 3 to 5 ranked, falsifiable hypotheses with observable predictions
- instrument when needed, changing one variable at a time
- keep logs limited to excerpts useful for falsifying a hypothesis
- tag any temporary instrumentation with a unique prefix for cleanup
- identify the root cause before fixing
- apply the minimal fix
- add or adapt a regression test at the right seam if that seam exists
- rerun useful feedback loops
- clean temporary logs, disposable harnesses, and debug prototypes before declaring completion

**Output:** root cause, fix, regression test, verification commands, remaining risks.

**Artifact publication:** If an active bug issue, sub-issue, or tracker item exists, propose publishing root cause, fix, regression test, and verification there. Without an active artifact location, keep the summary in session; propose a new issue only if diagnosis reveals follow-up work. Logs, harnesses, and temporary instrumentation stay local and must be cleaned up.

**Output contents:**

Required content:

- observed symptom
- environment and minimal reproduction, or reason for non-reproduction
- feedback loop built, command, or reproduction limitation
- hypotheses tested
- root cause
- fix applied
- regression test, or documented absence of the right seam
- verifications run
- risks or follow-ups

Avoid:

- long unannotated logs
- fix without isolated root cause
- stacking multiple unfalsified fixes

**Possible sizes:** short diagnosis for an isolated bug, or full investigation for a complex regression.

**Human gate:** validate bug impact, fix risk level, and possible follow-ups.

**Important:** `Diagnose` avoids random fixes. Do not stack multiple fixes before isolating the cause.

If no credible feedback loop can be built, stop explicitly, list what was tried, and ask for environment access, a captured artifact, or permission to add temporary instrumentation. Do not switch to pure hypothesis without a loop.

For a performance regression, measure first: baseline, profiler, query plan, or timing harness. Fix only after measuring.
