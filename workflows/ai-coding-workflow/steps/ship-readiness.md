# Ship Readiness

**Skill name:** `ship-readiness`

**Step type:** On-demand step.

**Role:** Decide whether a change is ready to ship by checking evidence, blockers, rollback, and accepted risks.

**When to use:** Sensitive release, critical flow, user-facing change, infrastructure change, migration, security/performance risk, or explicit release gate.

**Possible inputs:** Diff, commits, PRD, task specs, QA, review, CI, logs, release context, feature flag state, migration plan, rollback plan, monitoring, deployment notes.

**Process:**

1. Define release scope and blast radius.
2. Gather review, QA, CI, and verification evidence.
3. Identify rollback owner, rollback mechanism, monitoring, feature flags, migrations, environment/config changes, and external dependencies.
4. Check quality, security, performance, accessibility, migrations, and configuration when relevant.
5. Distinguish blockers, accepted risks, and pre-release recommendations.
6. Produce a clear `Go / No-Go` verdict with evidence and ownership.
7. Recommend post-launch checks when useful.

**Rules:**

- This is a contextual release gate, not a normal step for every initiative.
- Every `Go` needs evidence, owned accepted risks when risk remains, and rollback expectations when relevant.
- Every `No-Go` must name blockers and the path to unblock.
- Do not hide missing evidence behind a positive verdict.

**Output:** `Go / No-Go` verdict with release evidence, blockers, accepted risks, rollback, and recommendations.

**Output location:** Check `.agents/workflow/output-locations.md` when it exists. Recommended default: session verdict. If a PR, release issue, parent issue, or active tracker item exists, publish the verdict there when release coordination matters.

**Output template:**

```markdown
## Ship Readiness

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

**Possible sizes:** Quick readiness check for a small safe release; standard release gate for user-facing work; full readiness review for migrations, infrastructure, security, performance, or high-blast-radius releases.

**Verification:** Every `Go` has evidence, owned accepted risks, monitoring expectations when relevant, and a rollback plan. Every `No-Go` names blockers and the path to unblock.

**Human gate:** Accept risks or block the release.
