# 001 - Brief

**Skill name:** `brief`

**Step type:** Core workflow step (optional).

**Role:** Converge rough product context into a clear direction that can be validated, challenged, or turned into a PRD.

**When to use:** After brainstorming, for a new product, a large feature, an unclear idea, or when the opportunity needs framing. Skip it for a clear, bounded feature.

**Possible inputs:** Raw idea, brainstorming notes, transcript, user signals, business context, product context, relevant constraints.

**Process:**

1. Name the initiative and decide whether a durable local note is useful.
2. Load only useful brainstorming notes, user context, and constraints.
3. Separate observed facts, assumptions, and missing context.
4. Select the most promising direction or small set of directions to converge.
5. Clarify problem, target users, value proposition, and high-level solution direction.
6. Frame expected scope with `MVP / V1 / Later / Excluded` when useful.
7. Make critical hypotheses, constraints, non-goals, and open questions explicit.
8. Recommend the next gate: `Validate`, `Grill Me`, `Grill With Docs`, or `PRD`.

**Rules:**

- The brief converges product direction; it does not replace validation, PRD, or Tech Design.
- Keep the brief product-level; do not add implementation design.
- Carry forward only context that helps the next decision.

**Output:** Markdown brief that summarizes the product direction, initial scope, critical hypotheses, and recommended next gate.

**Output location:** Check `.agents/workflow/output-locations.md` when it exists. Recommended default: local `.initiatives/<initiative>/brief.md`. If the brief is immediately promoted, integrate the useful points into the PRD instead of preserving a separate artifact.

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
<!-- Required. Paragraph or short bullet list: high-level product direction, without technical design. -->
<Solution direction.>

## Scope
<!-- Required. Bullet list. Keep each scope line short. -->
- **MVP:** <Smallest useful outcome.>
- **V1:** <Important near-term expansion.>
- **Later:** <Deferred ideas.>
- **Excluded:** <Explicit non-goals.>

## Critical Hypotheses
<!-- Required. Bullet list: assumptions that could change the next investment decision. -->
- <Assumption to validate before investing further.>

## Constraints & Open Questions
<!-- Conditional. Bullet list: include only constraints, risks, or questions that affect the next step. -->
- <Constraint, risk, or question.>

## Recommended Next Gate
<!-- Required. One sentence: Validate / Grill Me / Grill With Docs / PRD, with rationale. -->
<Recommended next gate and rationale.>
```

**Possible sizes:** Minimal brief for one clear feature direction; standard brief for a multi-flow feature; full brief for a new product, MVP, or high-uncertainty initiative.

**Verification:** A human can explain the problem, target user, value, initial scope, non-goals, critical hypotheses, and next gate without reading raw brainstorming notes.

**Human gate:** Confirm direction and initial scope before `Validate`, `Grill Me`, `Grill With Docs`, or `PRD`.
