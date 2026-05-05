# Grill With Docs

**Skill name:** `grill-with-docs`

**Step type:** On-demand step.

**Role:** Align an intent or plan with durable vocabulary, existing decisions, and code reality before creating or updating artifacts.

**When to use:** Existing project, ambiguous business vocabulary, plan touching multiple modules, structural refactor, domain onboarding, or need to align product and codebase before `PRD` or `Tech Design`.

**Possible inputs:** Intent, brief, grill summary, draft PRD, draft Tech Design, `CONTEXT.md`, `CONTEXT-MAP.md`, `docs/decisions/`, project docs, relevant code, existing architecture.

**Process:**

1. Locate durable vocabulary, decisions, and relevant code before questioning the user.
2. Separate observed facts, recommendations, and decisions needing validation.
3. Challenge vague, overloaded, or inconsistent terms.
4. Ask one question at a time when code or docs are insufficient.
5. Resolve conflicts between user intent, code vocabulary, durable docs, and ADRs.
6. Identify durable vocabulary or decision updates that may be needed.
7. Summarize clarified decisions, selected terms, source-backed constraints, conflicts, and remaining ambiguities.

**Rules:**

- `Grill With Docs` aligns language and decisions. It does not replace `Review` or a full codebase map.
- Limit source reading to the intent or area under discussion.
- Provide a recommendation for each question.
- Propose ADRs only for decisions that are durable, surprising without context, and based on real trade-offs.
- Report conflicts between user intent, code vocabulary, durable docs, and ADRs explicitly.

**Output:** Session alignment summary with clarified decisions, selected terms, source-backed constraints, vocabulary conflicts, and remaining ambiguities.

**Output location:** Check `.agents/workflow/output-locations.md` when it exists. Recommended default: session context only. Update PRD, Tech Design, domain docs, or ADRs only after accepted decisions are validated.

**Output template:**

```markdown
## Docs Alignment Summary

## Clarified Decisions
<!-- Required. Bullet list: accepted decisions grounded in docs, code, or user validation. -->
- **<Decision area>:** <Accepted decision and rationale.>

## Selected Terms
<!-- Required when vocabulary matters. Definition list. -->
- **<Term>:** <Definition or source-backed meaning.>

## Source-Backed Constraints
<!-- Conditional. Bullet list: constraint plus source reference. -->
- <Constraint with code, doc, or ADR reference.>

## Conflicts Resolved
<!-- Conditional. Bullet list: docs/code/user-intent conflict and accepted resolution. -->
- <Conflict and accepted resolution.>

## Durable Updates to Consider
<!-- Conditional. Bullet list: durable docs to update after validation. -->
- <CONTEXT, CONTEXT-MAP, ADR, or project doc update.>

## Remaining Ambiguities
<!-- Conditional. Bullet list: unresolved question and recommended next step. -->
- <Question and recommended next step.>
```

**Possible sizes:** Micro-alignment for one term or interface; standard alignment for one feature area; full pre-PRD or pre-Tech Design session on an existing project.

**Verification:** Intent, code vocabulary, durable docs, and accepted decisions no longer contradict each other in the scoped area, or the remaining contradictions are explicit human decisions.

**Human gate:** Validate terms, durable decisions, and ADR candidates before they become source of truth.
