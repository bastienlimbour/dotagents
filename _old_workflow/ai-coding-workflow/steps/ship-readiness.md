# Ship Readiness

**Skill name:** `ship-readiness`

**Step type:** On-demand.

**Role:** Decide whether a change is ready to ship by checking evidence, blockers, rollback, and accepted risks.

**When to use:** Sensitive release, critical flow, user-facing change, infrastructure change, migration, security/performance risk, or explicit release gate.

**Possible inputs:** Diff, commits, Spec, task specs, QA, review, CI, logs, release context, feature flag state, migration plan, rollback plan, monitoring, deployment notes, feedback commands.

**Process:**

1. Define release scope and blast radius.
2. Determine release verification commands from project docs, scripts, CI, current release context, or existing tests; report command drift when discovered guidance is missing, stale, or insufficient.
3. Gather review, QA, CI, and verification evidence.
4. Identify rollback owner, rollback mechanism, monitoring, feature flags, migrations, environment/config changes, and external dependencies.
5. Check quality, security, performance, accessibility, migrations, and configuration when relevant.
6. Distinguish blockers, accepted risks, and pre-release recommendations.
7. Produce a clear `Go / No-Go` verdict with evidence and ownership.
8. Recommend post-launch checks when useful.

**Rules:**

- This is a contextual release gate, not a normal step for every initiative.
- Every `Go` needs evidence, owned accepted risks when risk remains, and rollback expectations when relevant.
- Every `No-Go` must name blockers and the path to unblock.
- Do not hide missing evidence behind a positive verdict.

**Output:** `Go / No-Go` verdict with release evidence, blockers, accepted risks, rollback, and recommendations.

**Output location:** Recommended default: session verdict. If a PR, release issue, parent issue, or active tracker item exists, ask before publishing the verdict there when release coordination matters. If the user does not confirm publication, keep the verdict in session only.

**Output template:**

```markdown
## Summary
<!-- Required. Paragraph, 1-3 sentences: what is shipping and the headline verdict. -->
<Ship readiness summary.>

## Verdict
<!-- Required. Single line. -->
Go / No-Go

## Scope & Blast Radius
<!-- Required. Paragraph, 1-4 sentences: what is shipping and who/what can be affected. -->
<Release scope and blast radius.>

## Evidence
<!-- Required. Bullet list: CI, tests, build, QA, review, browser check, logs, or monitoring evidence. -->
- <Evidence and result.>

## Blockers
<!-- Required for No-Go; otherwise omit or state `None`. Bullet list. -->
- **<Blocker>:** <Owner and path to unblock.>

## Accepted Risks
<!-- Required for Go when risk remains. Bullet list. -->
- **<Risk>:** <Owner, mitigation, and reason it is acceptable.>

## Rollback
<!-- Required for sensitive releases. Metadata list. -->
- **Owner:** <Person/team>
- **Mechanism:** <Rollback, feature flag, revert, migration rollback, or mitigation.>

## Release Notes
<!-- Conditional. Bullet list: config, migration, monitoring, feature flag, staged rollout, or post-launch check. -->
- <Release note.>
```

**Possible sizes:** lite (small safe release); standard (user-facing work); full (migrations, infrastructure, security, performance, or high-blast-radius releases).

**Verification:** Every `Go` has evidence, owned accepted risks, monitoring expectations when relevant, and a rollback plan. Every `No-Go` names blockers and the path to unblock.

**Human gate:** Accept risks or block the release.
