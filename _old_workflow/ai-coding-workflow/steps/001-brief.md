# 001 - Brief

**Skill name:** `brief`

**Step type:** Core, optional.

**Role:** Converge rough product context into a clear direction that can be validated, challenged, or integrated into a Spec.

**When to use:** After brainstorming, for a new product, MVP, large feature, unclear idea, or when the opportunity needs product framing before validation or specification. Skip it for a clear, bounded change that can go directly to Spec or a sufficient Execution Contract.

**Possible inputs:** Raw idea, brainstorming notes, transcript, user signals, business context, product context, relevant constraints.

**Process:**

1. Name the initiative and draft the brief before deciding whether a local Markdown note is useful.
2. Load only useful brainstorming notes, user context, and constraints.
3. Separate observed facts, assumptions, and missing context.
4. Select the most promising direction or small set of directions to converge.
5. Clarify problem, target users, value proposition, and high-level solution direction.
6. Frame expected scope with `MVP / Future / Excluded` when useful.
7. Make critical hypotheses, constraints, non-goals, and open questions explicit.
8. Surface what would unblock the next decision as explicit open questions or pending validations.

**Rules:**

- The brief converges product direction; it stops before detailed requirements, Technical Design, task slicing, or implementation planning.
- The brief may ask lightweight clarifying questions, but use `Grill Me` when dependent decisions need a full decision-tree interview.
- Keep the brief product-level; do not add implementation details.
- Carry forward only context that helps the next decision.

**Output:** Markdown brief that summarizes the product direction, initial scope, critical hypotheses, and the open questions or pending decisions that would unblock validation or Spec creation.

**Output location:** Recommended default: ask before writing or updating local `.initiatives/001-<initiative>/brief.md`. If the user does not confirm, keep the brief in session only. If the brief is immediately promoted, integrate the useful points into the Spec instead of preserving a separate artifact.

**Output template:**

```markdown
# <Initiative> Brief

## Problem
<!-- Required. Paragraph, 2-5 sentences: who has the problem, what is painful, and why it matters. -->
<Problem statement.>

## Target Users
<!-- Required. Bullet list: one user segment per bullet. -->
- **<User segment>:** <Context, need, or job-to-be-done.>

## Value Proposition
<!-- Required. Paragraph, 1-3 sentences: why this direction is worth pursuing. -->
<Value proposition.>

## Solution Direction
<!-- Required. Paragraph or short bullet list: high-level product direction, without Technical Design or implementation content. -->
<Solution direction.>

## Scope
<!-- Required. Bullet list. Keep each scope line short. -->
- **MVP:** <Smallest useful outcome that tests the direction.>
- **Future:** <Deferred ideas to revisit only if MVP succeeds. Illustrative, not committed.>
- **Excluded:** <Explicit non-goals decided early.>

## Critical Hypotheses
<!-- Required. Bullet list: assumptions that could change the next investment decision. -->
- <Assumption to validate before investing further.>

## Constraints & Open Questions
<!-- Conditional. Bullet list: include only constraints, risks, or questions that affect the next step. -->
- <Constraint, risk, or question.>

## Pending Decisions
<!-- Required. Bullet list: blocking questions, validations, or judgments that must resolve before validation or Spec creation can proceed. -->
- <Pending decision and what would unblock it.>
```

**Possible sizes:** lite (one clear feature direction); standard (multi-flow feature); full (new product, MVP, or high-uncertainty initiative).

**Verification:** A human can explain the problem, target user, value, initial scope, non-goals, critical hypotheses, and pending decisions without reading raw brainstorming notes.

**Human gate:** Confirm direction, initial scope, and the pending decisions that need to resolve before product specification.
