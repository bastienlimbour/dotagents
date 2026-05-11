# Grill Me

**Skill name:** `grill-me`

**Step type:** On-demand.

**Role:** Resolve important decisions through a focused interview, one question at a time.

**When to use:** Clear idea with implicit decisions, Brief or Spec direction to challenge, Technical Design decision tree, dependent decisions, ambiguous Execution Contract, or explicit request to "grill me". Use before or after Brief, Validate, Technical Design, Spec, or Slice when unresolved decisions block progress.

**Possible inputs:** Brief, validation note, Technical Design, Spec, task spec, implementation plan, user intent, repository context, current decision log.

**Process:**

1. Identify unresolved decisions that most affect the work waiting on them.
2. Answer discoverable questions from repository context or docs before asking the user.
3. Order questions by dependency, risk, and decision value.
4. Ask the highest-value unresolved question.
5. Capture the accepted decision, intentionally deferred branch, or remaining ambiguity.
6. Repeat until the work is unblocked or the remaining ambiguity is intentionally deferred.
7. Hand off the structured decision log as session output for integration into the next artifact.

**Rules:**

- Ask one question at a time.
- Provide a recommendation and concise choices when possible.
- Apply `Grill Me` at the most useful ambiguity point in the work being unblocked.
- Do not ask the user questions that repository context or docs can answer.
- Do not create a competing source of truth; integrate accepted decisions into the Brief, validation note, Technical Design, Spec, or task spec that depends on them.

**Output:** Session decision log with clarified decisions, accepted recommendations, deferred branches, and assumptions to integrate into the unblocked work.

**Output location:** Recommended default: session context only. Ask before writing or updating any local artifact, durable doc, issue, or tracker comment to consolidate accepted decisions. If the user does not confirm, keep the decision log in session only.

**Output template:**

```markdown
## Summary
<!-- Required. Paragraph, 1-3 sentences: what was clarified and what is now unblocked. -->
<Grill summary.>

## Clarified Decisions
<!-- Required. Bullet list: accepted decisions and recommendation chosen. -->
- **<Decision area>:** <Accepted decision and rationale.>

## Dependencies Resolved
<!-- Conditional. Bullet list: decision dependencies or branches resolved. -->
- <Dependency or branch resolved.>

## Deferred Branches
<!-- Conditional. Bullet list: questions intentionally left open and what would unblock them. -->
- <Deferred question and what would unblock it.>

## Assumptions to Carry Forward
<!-- Conditional. Bullet list: assumptions to integrate into the next artifact. -->
- <Assumption and target artifact.>

## Open Conditions
<!-- Required. Bullet list: pending conditions that must hold before the unblocked work can proceed safely. -->
- <Open condition.>
```

**Possible sizes:** lite (one blocking decision); standard (one feature intent); full (plan with several dependent decisions).

**Verification:** Decisions are explicit enough to update the unblocked artifact or proceed, and unresolved branches list the conditions that would resolve them.

**Human gate:** Answer questions and validate accepted decisions.
