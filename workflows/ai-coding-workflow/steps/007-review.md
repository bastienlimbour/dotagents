# 007 - Review

**Skill:** `review`

**Status:** Recommended core step.

**Role:** Cold code review, separate from implementation.

**When to use:** Any non-trivial task, complex logic, sensitive change, architecture, security, performance, or need for a fresh review.

**Possible inputs:** diff, commits, PRD, task spec, Tech Design, tests, verification results.

**Actions:**

- ideally start from a fresh context, possibly with a different LLM than the one that implemented the code
- explicitly provide useful project standards to the reviewer
- compare code, PRD/task spec, Tech Design, and acceptance criteria
- review tests and verification
- look for divergences, omissions, bugs, and regressions
- check for out-of-scope changes, secrets, accidental config changes, and missed migrations
- evaluate correctness, readability, architecture, security, and performance
- verify that tests cover real behavior and important edge cases
- flag dead code and obvious simplifications
- explicitly report unreviewed areas or confidence level when needed

**Output:** session feedback, or review comment in the tracker/PR.

**Artifact publication:** If a PR exists, propose publishing the review as a PR comment by default. Otherwise, if an active sub-issue or tracker issue exists, propose a comment there. Without an active artifact location, keep the review in session; do not create a local file by default.

**Output contents:**

Required content:

- verdict
- findings by severity, or explicit `No findings`
- file/line references when possible
- test and verification coverage

Conditional content:

- deviations from PRD, task spec, or Tech Design
- regression risks
- fix suggestions
- unreviewed areas or confidence level

Avoid:

- optimistic summary before findings
- code fixes before stating the problems
- non-actionable style comments

**Possible sizes:** short review for a simple change, full review for a sensitive change.

**Human gate:** accept the task or send it back for correction.

**Important:** `Review` evaluates code. It is not a manual functional validation checklist. The reviewer lists findings first; they do not modify code before stating the problems.
