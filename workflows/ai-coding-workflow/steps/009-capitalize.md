# 009 - Capitalize

**Skill name:** `capitalize`

**Step type:** Core workflow step (recommended, when durable information changed).

**Role:** Move useful lasting knowledge from the initiative into the project's durable sources of truth.

**When to use:** After a durable change to product behavior, convention, architecture, API, documented behavior, ADR, future artifact, engineering practice, or agent/LLM rule.

**Possible inputs:** Shipped code, diff, commits, PRD, task specs, Tech Design, ADRs, review findings, QA findings, existing docs, tracker state.

**Process:**

1. Identify what changed that should remain true after the initiative closes.
2. Distinguish durable truth from temporary initiative context.
3. Locate the current source of truth before editing or creating docs.
4. Update obsolete durable docs directly when the destination is clear.
5. Create or adjust ADRs for durable technical decisions.
6. Update `CONTEXT.md` or `CONTEXT-MAP.md` when durable domain vocabulary changes.
7. Update `.agents/` or agent docs when future agents need a persistent rule or output convention.
8. Realign future PRD, Tech Design, or task artifacts invalidated by implementation.
9. Clean up, archive, close, or consolidate temporary artifacts when approved or project convention allows it.
10. Open follow-ups for debt, refactors, or deferred documentation when needed.
11. Report explicitly when no capitalization is useful.

**Rules:**

- Capitalize maintains lasting truth.
- Temporary artifacts should not become documentation rot.
- Update durable docs only with stable information that future agents or humans should reuse.
- Do not create new durable docs when a concise no-op summary is the honest result.

**Output:** Durable docs updates, ADRs, agent rule updates, tracker follow-ups, temporary artifact cleanup, or a concise no-op summary.

**Output location:** Check `.agents/workflow/output-locations.md` when it exists. Recommended default: write durable information directly into the relevant source of truth: code, tests, product docs, repository docs, project docs, engineering docs, `CONTEXT.md`, `CONTEXT-MAP.md`, `.agents/workflow/`, agent/LLM docs, or `docs/decisions/`.

**Output template:**

```markdown
## Capitalization Summary
<!-- Required. Paragraph, 1-3 sentences: what durable truth changed, or state that no durable update is useful. -->
<Summary.>

## Durable Updates
<!-- Conditional. Bullet list: files, ADRs, agent rules, or tracker items updated. -->
- **<File or destination>:** <Durable information updated.>

## Source of Truth
<!-- Required when updates were made. Bullet list: current canonical locations future agents should use. -->
- <Canonical source and what it now owns.>

## Temporary Artifact Cleanup
<!-- Conditional. Bullet list: artifacts deleted, archived, closed, or intentionally retained. -->
- <Artifact and cleanup status.>

## Follow-ups
<!-- Conditional. Bullet list: debt, docs, refactor, or product follow-up opened or recommended. -->
- <Follow-up and destination.>
```

**Possible sizes:** No-op note when nothing durable changed; targeted doc update for one stable behavior or convention; full capitalization pass after a large initiative, architecture decision, or release.

**Verification:** Future agents can find current behavior, durable decisions, workflow rules, and follow-ups without relying on stale initiative artifacts.

**Human gate:** Validate what becomes durable source of truth and approve cleanup of local artifacts when needed.
