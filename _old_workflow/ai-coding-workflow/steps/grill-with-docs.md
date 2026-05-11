# Grill With Docs

**Skill name:** `grill-with-docs`

**Step type:** On-demand.

**Role:** Align an intent or plan with durable vocabulary, existing decisions, and code reality before creating or updating artifacts.

**When to use:** Existing project, ambiguous business vocabulary, plan touching multiple modules, structural refactor, domain onboarding, or need to align product and codebase before Brief, Technical Design, Spec, Slice, or implementation.

**Possible inputs:** Intent, brief, grill summary, draft Technical Design, draft Spec, task spec, `CONTEXT.md`, `CONTEXT-MAP.md`, `docs/decisions/`, project docs, relevant code, existing architecture.

**Process:**

1. Locate durable vocabulary, decisions, and relevant code before questioning the user.
2. Separate observed facts, recommendations, and decisions needing validation.
3. Challenge vague, overloaded, or inconsistent terms.
4. Ask one question at a time when code or docs are insufficient.
5. Resolve conflicts between user intent, code vocabulary, durable docs, and ADRs.
6. Identify durable vocabulary or decision updates that may be needed.
7. Summarize clarified decisions, selected terms, source-backed constraints, conflicts, and remaining ambiguities.

**Rules:**

- Grill With Docs aligns language and decisions; it is not code review and not a full codebase map.
- Limit source reading to the intent or area under discussion.
- Provide a recommendation for each question.
- Explore code and docs before asking the user when the answer is discoverable.
- Propose ADRs only for decisions that are durable, surprising without context, and based on real trade-offs.
- Report conflicts between user intent, code vocabulary, durable docs, and ADRs explicitly.
- Do not create a competing source of truth; integrate accepted decisions into the Brief, Technical Design, Spec, or task spec that depends on them.

**Output:** Session alignment summary with clarified decisions, selected terms, source-backed constraints, vocabulary conflicts, and remaining ambiguities.

**Output location:** Recommended default: session context only. Ask before updating durable docs, domain glossaries, ADRs, local artifacts, issues, or tracker comments after accepted decisions are validated. If the user does not confirm, keep the alignment summary in session only.

**Output template:**

```markdown
## Summary
<!-- Required. Paragraph, 1-3 sentences: what alignment was reached and which conflicts remain. -->
<Alignment summary.>

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
<!-- Conditional. Bullet list: unresolved question and what would unblock it. -->
- <Question and what would unblock it.>
```

**Possible sizes:** lite (one term or interface); standard (one feature area); full (pre-specification alignment session on an existing project).

**Verification:** Intent, code vocabulary, durable docs, and accepted decisions no longer contradict each other in the scoped area, or the remaining contradictions are explicit human decisions.

**Human gate:** Validate terms, durable decisions, and ADR candidates before they become source of truth.
