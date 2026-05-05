# Grill Me

**Skill name:** `grill-me`

**Step type:** On-demand step.

**Role:** Resolve important decisions through a focused interview, one question at a time.

**When to use:** Clear idea with implicit decisions, plan/design to challenge, dependent decisions, ambiguous Execution Contract, or explicit request to "grill me".

**Possible inputs:** Brief, PRD, Tech Design, task spec, implementation plan, user intent, repository context, current decision log.

**Process:**

1. Identify unresolved decisions that most affect the next step.
2. Answer discoverable questions from repository context or docs before asking the user.
3. Order questions by dependency, risk, and decision value.
4. Ask the highest-value unresolved question.
5. Capture the accepted decision, intentionally deferred branch, or remaining ambiguity.
6. Repeat until the next step is unblocked or the remaining ambiguity is intentionally deferred.
7. Route resolved context to the next artifact or step.

**Rules:**

- Ask one question at a time.
- Provide a recommendation and concise choices when possible.
- Use `Grill Me` at the most useful ambiguity point: after `Brief`, after `PRD`, after `Tech Design`, or before `Build` when the Execution Contract is ambiguous.
- Do not ask the user questions that repository context or docs can answer.

**Output:** Session decision log with clarified decisions, accepted recommendations, deferred branches, and assumptions to integrate into the next step.

**Output location:** Check `.agents/workflow/output-locations.md` when it exists. Recommended default: session context only. Update an artifact only when the user asks or when project convention requires accepted decisions to be consolidated.

**Output template:**

```markdown
## Grill Me Decision Log

## Clarified Decisions
<!-- Required. Bullet list: accepted decisions and recommendation chosen. -->
- **<Decision area>:** <Accepted decision and rationale.>

## Dependencies Resolved
<!-- Conditional. Bullet list: decision dependencies or branches resolved. -->
- <Dependency or branch resolved.>

## Deferred Branches
<!-- Conditional. Bullet list: questions intentionally left open and their destination. -->
- <Deferred question and next step.>

## Assumptions to Carry Forward
<!-- Conditional. Bullet list: assumptions to integrate into the next artifact. -->
- <Assumption and target artifact.>

## Recommended Next Step
<!-- Required. One sentence: next workflow step and rationale. -->
<Recommended next step and rationale.>
```

**Possible sizes:** Micro-interview for one blocking decision; standard interview for one feature intent; full interview for a plan with several dependent decisions.

**Verification:** Decisions are explicit enough to update the next artifact or proceed, and unresolved branches are intentionally assigned to the right next step.

**Human gate:** Answer questions and validate accepted decisions.
