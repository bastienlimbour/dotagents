# 005 - Slice

**Skill name:** `slice`

**Step type:** Core workflow step (required, for multi-task initiatives).

**Role:** Convert accepted product and technical context into vertical, verifiable tasks that agents can implement safely.

**When to use:** Multi-task initiative. Skip it for a minimal single-task PRD with a sufficient Execution Contract.

**Possible inputs:** PRD, Tech Design, ADRs, parent issue, repository context, product priorities, dependency constraints, team constraints, feedback commands.

**Process:**

1. Confirm the PRD is current enough to slice.
2. Confirm whether Tech Design or ADRs are needed before slicing.
3. Identify product requirements, dependencies, risk-first work, and likely verification routes.
4. Split work into vertical slices that each produce a useful end-to-end signal.
5. Include only the layers required by each slice: data, logic, API/routes, minimal UI, tests, or migration steps.
6. Order tasks by real dependencies and risk, not by technical layer.
7. Mark tracer-bullet or risk-first slices when early feedback matters.
8. Classify tasks as `AFK` or `HITL` when useful.
9. Assign rough size `XS / S / M / L`; split `L` tasks unless the reason to keep them is explicit.
10. Present granularity, dependencies, merge/split decisions, and `AFK | HITL` classification to the human before publication.
11. After validation, publish one sub-issue or task artifact per vertical slice.

**Rules:**

- A task spec is an Execution Contract, not a detailed implementation plan.
- Keep each task behaviorally self-contained, independently grabbable, and verifiable.
- Prefer vertical slices over technical-layer tasks.
- Do not slice against stale PRD or missing required Tech Design decisions.

**Output:** One task spec per vertical slice, each containing a sufficient Execution Contract for `Build`.

**Output location:** Check `.agents/workflow/output-locations.md` when it exists. Recommended default: sub-issues linked to the parent issue. Local Markdown alternative: `.initiatives/<initiative>/tasks/*.md`.

**Output template:**

```markdown
# <NNN> - <Task Title>

<!-- Required. Metadata list. Keep values short and machine-readable where possible. -->
- **Parent:** <Parent issue, PRD, or initiative link>
- **Type:** AFK / HITL
- **Size:** XS / S / M / L
- **Blocked by:** <Dependencies, or none>

## Goal
<!-- Required. Paragraph, 1-3 sentences: what this slice should achieve. -->
<Task goal.>

## Scope
<!-- Required. Bullet list: included behavior first, local non-goals when useful. -->
- <Included behavior.>
- <Local non-goal when useful.>

## Behavior
<!-- Required. Paragraph or short bullets: end-to-end behavior to build in this task. -->
<End-to-end behavior.>

## Acceptance Criteria
<!-- Required. Checklist or bullet list: observable task-level criteria. -->
- [ ] <Task-level observable acceptance criterion.>
- [ ] <Important edge case or error state.>

## Verification
<!-- Required. Bullet list: expected command, check, browser flow, test, or manual signal. -->
- <Expected verification signal.>

## References
<!-- Conditional. Bullet list: PRD requirement, Tech Design section, ADR, issue, or code area. -->
- <Reference.>

## Likely Touchpoints
<!-- Conditional. Bullet list: likely areas, without imposing a detailed implementation plan. -->
- <Likely area or module.>
```

**Possible sizes:** XS task for a tiny verifiable change; S task for one narrow behavior; M task for a normal vertical slice; L task only when the slice cannot be split without losing useful feedback.

**Verification:** Every task has behavior, task-level acceptance criteria, dependencies, expected verification, and enough context to start `Build` without copying the full PRD or Tech Design.

**Human gate:** Validate granularity, verticality, order, dependencies, verifiability, and `AFK | HITL` classification.
