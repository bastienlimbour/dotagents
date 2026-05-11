# Brainstorm

**Skill name:** `brainstorm`

**Step type:** On-demand.

**Role:** Expand and structure the option space before the workflow converges on a direction.

**When to use:** Unclear idea, new product, new direction, major feature, product/technical exploration, UX exploration, or lack of useful options.

**Possible inputs:** Brainstorming goal, user context, intuition, notes, transcript, existing ideas, data, code context, project documentation, market or product constraints.

**Process:**

1. Define the brainstorming goal, exploration type, and timebox.
2. Draft session notes first; ask before creating or updating a local brainstorming artifact when a durable session note is useful.
3. Ask open-ended questions that generate options and reveal assumptions.
4. Explore problems, opportunities, users, use cases, solution directions, capabilities, constraints, risks, and selection criteria.
5. Group ideas by theme, problem, user, use case, solution, capability, or assumption.
6. After meaningful user responses, ask before updating any confirmed local artifact; otherwise keep structured notes in session.
7. Preserve promising directions without forcing a final decision.
8. Hand off the structured options when the user is ready to converge.

**Rules:**

- `Brainstorm` intentionally diverges; convergence is out of scope.
- Stop when the user confirms enough directions, the timebox elapses, or further options would not change the next decision.
- Do not promote raw brainstorming notes to product truth without an explicit convergence step.

**Output:** Markdown brainstorming note with structured options, clusters, candidate directions, selection criteria, and open questions.

**Output location:** Recommended default: ask before writing or updating local `.initiatives/001-<initiative>/brainstorming.md`. Session-only brainstorming is acceptable for lightweight exploration or when the user does not confirm a file write.

**Output template:**

```markdown
# <Initiative> Brainstorming

## Goal
<!-- Required. Paragraph, 1-3 sentences: what is being explored and why. -->
<Brainstorming goal.>

## Context
<!-- Conditional. Bullet list: only context that helps generate or filter ideas. -->
- <Relevant user, product, technical, business, or market context.>

## Idea Clusters
<!-- Required. Grouped bullet lists. Use one subsection per theme, problem, user, use case, solution, capability, or assumption. -->

### <Theme>
- <Idea, opportunity, problem, solution, or capability.>

## Candidate Directions
<!-- Required. Bullet list: promising directions to evaluate later, without choosing one. -->
- <Promising direction to filter later.>

## Selection Criteria
<!-- Conditional. Bullet list: criteria that may help choose later. -->
- <Criterion that may help choose later.>

## Assumptions & Risks
<!-- Conditional. Bullet list: assumptions, constraints, or risks surfaced during brainstorming. -->
- <Assumption, constraint, or risk.>

## Open Questions
<!-- Required. Bullet list: questions still open after the session, with what would unblock each. -->
- <Open question and what would unblock it.>
```

**Possible sizes:** lite (one decision); standard (one product area); full (new product, MVP, or broad strategy session).

**Verification:** The output expands and organizes useful possibilities without prematurely choosing the product direction.

**Human gate:** Choose which directions to filter, converge, validate, or discard.
