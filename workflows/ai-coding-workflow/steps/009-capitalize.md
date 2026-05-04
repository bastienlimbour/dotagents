# 009 - Capitalize

**Skill:** `capitalize`

**Status:** Core step when there is a durable decision or documentation to maintain.

**Role:** Align project documentation and AI/agent documentation with what was actually built.

**When to use:** After a durable change to convention, architecture, API, documented behavior, ADR, future artifact, or agent rule.

**Possible inputs:** shipped code, diff, commits, PRD, task specs, Tech Design, ADRs, existing docs.

**Actions:**

- update obsolete docs
- verify that durable documentation does not duplicate a temporary artifact
- create or adjust ADRs
- create or update `CONTEXT.md` or `CONTEXT-MAP.md` if durable domain vocabulary changes
- update `.agents/` if agent-consumed configuration changes
- update AI/agent docs if a rule must persist
- realign invalidated PRD, Tech Design, or future artifacts
- delete, archive, close, or consolidate temporary artifacts that should no longer guide agents
- open debt or refactor follow-ups when needed

**Output:** updated docs, ADRs, agent rules, follow-ups, or a note that no capitalization is useful.

**Artifact publication:** Consolidate durable information into code, tests, project docs, `CONTEXT.md`, `CONTEXT-MAP.md`, `.agents/`, or `docs/decisions/`. If a parent issue, sub-issue, or tracker exists, propose updating the body/final comment, closing completed items, or opening follow-ups. In local Markdown mode, propose deleting or archiving `.initiatives/<initiative>/` after consolidation; ask for confirmation before deleting anything.

**Output contents:**

If there is nothing to capitalize:

- one sentence stating that no durable update is useful

If capitalization is done:

- documentation files modified
- ADRs created or adjusted
- domain vocabulary created or updated when applicable
- agent rules modified
- `.agents/` configuration modified when applicable
- future artifacts realigned
- temporary artifacts deleted, archived, or closed
- follow-ups opened
- decisions made durable

Avoid:

- full initiative summary
- documenting temporary decisions
- duplicating the PRD, Tech Design, or task specs

**Possible sizes:** short note if nothing should be capitalized, full update for a durable decision.

**Human gate:** validate what becomes the durable source of truth.

**Important:** Capitalize does not document for its own sake; it maintains what must stay useful and true. Temporary artifacts should not survive by default and create documentation rot.
