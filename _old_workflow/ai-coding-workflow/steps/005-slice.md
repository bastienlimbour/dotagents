# 005 - Slice

**Skill name:** `slice`

**Step type:** Core, required (for multi-task initiatives).

**Role:** Convert an accepted Spec, plus any separate Technical Design context, into vertical, verifiable task specs that agents can implement safely.

**When to use:** Multi-task initiative. Skip it for a minimal single-task Spec or Execution Contract that is already sufficient for Build.

**Possible inputs:** Spec, Technical Design, ADRs, parent issue, repository context, product priorities, dependency constraints, team constraints, feedback commands, prototype or validation notes when referenced by the Spec.

**Process:**

1. Confirm the Spec is current enough to slice and owns the accepted initiative truth.
2. Confirm accepted Technical Design decisions are integrated into the Spec, or explicitly available as referenced context.
3. Confirm whether additional Technical Design or ADRs are needed before slicing.
4. Identify product requirements, user stories, technical decisions, dependencies, risk-first work, and likely verification routes.
5. Split work into vertical slices that each produce a useful end-to-end signal.
6. Include only the layers required by each slice: data, logic, API/routes, minimal UI, tests, or migration steps.
7. Order tasks by real dependencies and risk, not by technical layer.
8. Mark tracer-bullet or risk-first slices when early feedback matters.
9. Classify tasks as `AFK` or `HITL` when useful.
10. Assign rough size `XS / S / M / L`; split `L` tasks unless the reason to keep them is explicit.
11. Present granularity, dependencies, merge/split decisions, `AFK | HITL` classification, and requirement/user-story coverage to the human before publication.
12. After validation, ask before creating task issues, adding a parent issue comment, or writing local task artifacts.

**Rules:**

- A task spec is an Execution Contract, not a detailed implementation plan.
- Task specs derive from the Spec and any referenced Technical Design; copy only task-relevant product and technical context.
- Keep each task behaviorally self-contained, independently grabbable, and verifiable.
- Prefer vertical slices over technical-layer tasks.
- Do not slice against a stale Spec or missing required technical decisions.
- Apply the `AFK | HITL` rubric below; mark a task `HITL` when any trigger fires, otherwise `AFK`.

**AFK | HITL classification rubric:**

- `HITL` when any of:
  - public interface, schema, or contract change;
  - migration or data backfill;
  - security-, privacy-, or compliance-sensitive code;
  - ambiguous or contested behavior;
  - decision conflicts with an ADR or durable convention;
  - real performance or reliability trade-off;
  - untested or risky module without reliable feedback loop;
  - destructive, irreversible, or externally visible action.
- `AFK` otherwise: contract is unambiguous, behavior is observable, feedback loop is reliable, scope is bounded, and no public interface is touched.

**Output:** One task spec per vertical slice, each containing a sufficient Execution Contract for downstream implementation.

**Output location:** Recommended default: when a parent issue exists, ask before creating one normal task issue per vertical slice; each task issue references the parent issue. After task issue creation, ask before adding a parent issue comment linking the task issues. If no parent issue exists, ask the user to choose between creating/linking a parent issue for task issues and writing local `.initiatives/001-<initiative>/tasks/001-<task>.md` files. If the user does not confirm, keep the task specs in session only.

**Output template:**

```markdown
# <NNN> - <Task Title>

<!-- Required. Metadata list. Keep values short and machine-readable where possible. -->
- **Parent:** <Parent Spec issue or initiative link>
- **Type:** AFK | HITL
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
<!-- Conditional. Bullet list: Spec requirement, Technical Design section, ADR, issue, or code area. -->
- <Reference.>

## Likely Touchpoints
<!-- Conditional. Bullet list: likely areas, without imposing a detailed implementation plan. -->
- <Likely area or module.>
```

**Possible sizes:** Per task spec, use `XS / S / M / L` based on task scope: XS (tiny verifiable change); S (one narrow behavior); M (normal vertical slice); L (only when the slice cannot be split without losing useful feedback).

**Verification:** Every task has behavior, task-level acceptance criteria, dependencies, expected verification, `AFK | HITL` classification, and enough context from the Spec and any Technical Design to start implementation without copying the full upstream artifacts.

**Human gate:** Validate granularity, verticality, order, dependencies, verifiability, and `AFK | HITL` classification.
