# Ship Readiness

**Skill:** `ship-readiness`

**Status:** On-demand step, optional release gate.

**Role:** Verify that a change is ready to ship under good conditions.

**When to use:** Sensitive release, critical flow, user-facing or infrastructure change, migration, security/performance risk.

**Possible inputs:** diff, commits, PRD, task specs, QA, review, CI, logs, release context.

**Actions:**

- verify CI, automated checks, and available evidence
- verify quality, security, performance, and accessibility when relevant
- verify migrations, environment variables, monitoring, rollback owner, and rollback plan
- distinguish blockers, accepted risks, and pre-release recommendations

**Output:** `Go / No-Go` verdict, pre-release checklist, or tracker equivalent.

**Artifact publication:** If a PR, release issue, parent issue, or active tracker item exists, propose publishing the `Go / No-Go` verdict, blockers, accepted risks, and evidence there. Without an active artifact location, keep the verdict in session or propose a local file only for a release that must be audited.

**Output contents:**

Required content:

- `Go / No-Go` verdict
- blockers
- accepted risks
- available evidence or checks
- rollback plan
- pre-release recommendations

Conditional content:

- quality checks
- security checks
- performance
- accessibility when relevant
- migrations and environment variables
- monitoring / alerting

Avoid:

- generic checklist without verdict
- implicit or unowned risks
- full duplication of QA or review

**Possible sizes:** short checklist, or full release gate.

**Human gate:** accept risks or block the release.

**Important:** This is not a normal step for every initiative.
