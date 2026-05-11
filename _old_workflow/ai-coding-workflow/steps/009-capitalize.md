# 009 - Capitalize

**Skill name:** `capitalize`

**Step type:** Core, recommended (when durable information changed).

**Role:** Move useful lasting knowledge from the initiative into the project's durable sources of truth.

**When to use:** After a durable change to product behavior, convention, architecture, API, documented behavior, ADR, future artifact, engineering practice, or agent/LLM rule.

**Possible inputs:** Shipped code, diff, commits, Spec, task specs, Technical Design, ADRs, review findings, QA findings, existing docs, tracker state.

**Process:**

1. Identify what changed that should remain true after the initiative closes.
2. Distinguish durable truth from temporary initiative context.
3. Locate the current source of truth before editing or creating docs.
4. Draft obsolete durable doc updates when the destination is clear, then ask before every durable doc write or update.
5. Draft ADRs for durable technical decisions, then ask before creating or updating them.
6. Draft `CONTEXT.md` or `CONTEXT-MAP.md` updates when durable domain vocabulary changes, then ask before writing them.
7. Draft `.agents/rules/*` or agent doc updates when future agents need a persistent rule or output convention, then ask before writing them.
8. Realign future Spec, Technical Design, or task artifacts invalidated by implementation.
9. Ask before cleaning up, archiving, closing, or consolidating temporary artifacts.
10. Draft follow-ups for debt, refactors, or deferred documentation when needed, then ask before opening any tracker item or writing any follow-up artifact.
11. Report explicitly when no capitalization is useful.

**Rules:**

- Capitalize maintains lasting truth.
- Temporary artifacts should not become documentation rot.
- Update durable docs only with stable information that future agents or humans should reuse.
- Do not create new durable docs when a concise no-op summary is the honest result.

**Output:** Durable docs updates, ADRs, agent rule updates, tracker follow-ups, temporary artifact cleanup, or a concise no-op summary.

**Output location:** Recommended default: ask before writing durable information directly into the relevant source of truth: code, tests, product docs, repository docs, project docs, engineering docs, `CONTEXT.md`, `CONTEXT-MAP.md`, `.agents/rules/*`, agent/LLM docs, or `docs/decisions/`. Ask before tracker follow-ups or temporary artifact cleanup. If the user does not confirm, keep the capitalization summary in session only.

**Output template:**

```markdown
## Summary
<!-- Required. Paragraph, 1-3 sentences: what durable truth changed, or state that no durable update is useful. -->
<Capitalization summary.>

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

**Possible sizes:** lite (no-op note or one stable behavior/convention); standard (targeted doc updates after a feature); full (capitalization pass after a large initiative, architecture decision, or release).

**Verification:** Future agents can find current behavior, durable decisions, workflow rules, and follow-ups without relying on stale initiative artifacts.

**Human gate:** Validate what becomes durable source of truth and approve cleanup of local artifacts when needed.
