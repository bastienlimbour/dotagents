# 004 - Spec

**Skill name:** `spec`

**Step type:** Core, required for initiatives except trivial direct work.

**Role:** Create the parent initiative source of truth that combines accepted product behavior, technical decisions, testing decisions, scope boundaries, and enough context for slicing or implementation.

**When to use:** Before splitting or implementing any non-trivial initiative. Use a minimal Execution Contract instead only for trivial fixes, hotfixes, or single-task work that is already fully specified.

**Possible inputs:** Clear idea, `brief.md`, `validation.md`, Technical Design output, grill summary, prototype summary, user feedback, product constraints, repository context, existing documentation, relevant current behavior, ADRs, feedback commands.

**Process:**

1. Choose Spec size before writing.
2. Consolidate accepted decisions from the prompt, Brief, Validate, Grill, Technical Design, prototype, and existing docs; do not re-interview unless a blocking gap remains.
3. Explore relevant repository context when current behavior, modules, integrations, or test patterns affect the Spec.
4. Define product summary, problem, solution, users, use cases, requirements or user stories, important edge cases, and out-of-scope behavior.
5. Capture accepted technical decisions: tools and libraries, modules built or modified, architecture, interfaces, data or schema changes, API contracts, integrations, migrations, specific interactions, technical clarifications, risks, and compatibility concerns.
6. Capture testing decisions: feedback loops, test types, modules or seams to test, prior art, manual QA needs, and verification expectations.
7. Surface blocking and non-blocking open questions explicitly.
8. Add split notes when they help downstream vertical slicing.
9. After drafting, ask the user to choose the output target; recommend a parent GitHub/tracker issue body by default, with local Markdown as the alternative.

**Rules:**

- Spec is the initiative source of truth. Upstream discovery artifacts feed it; once accepted decisions are integrated, they should not remain competing truth.
- Keep product, technical, and testing sections distinct even though they live in one parent artifact.
- Technical Decisions should record accepted decisions and constraints, not detailed task sequencing or brittle file-by-file instructions.
- If product direction is unstable, resolve it through Brief, Validate, Grill Me, or Grill With Docs before finalizing the Spec.
- If technical decisions are too uncertain, large, risky, or source-dependent, use Technical Design before finalizing the Spec.
- Use durable vocabulary from `CONTEXT.md` or project docs when available.
- Requirements must be concrete, observable, and sliceable.

**Output:** Markdown Spec that becomes the current parent source of truth for downstream slicing and implementation.

**Output location:** Recommended default: ask the user to choose between creating or updating a parent GitHub/tracker issue body and writing local `.initiatives/001-<initiative>/spec.md`; recommend the issue body. Every issue create/edit or file write/update requires confirmation. If the user does not confirm, keep the Spec in session only.

**Output template:**

Use the smallest useful Spec and omit sections without real signal.

```markdown
# <Initiative or Feature Name>

## Summary
<!-- Required. Paragraph, 1-3 sentences: what is being built, for whom, and why. -->
<Concise initiative summary.>

## Problem
<!-- Required for product work. Paragraph, 2-5 sentences: user or business problem, not the absence of a solution. -->
<Problem statement.>

## Solution
<!-- Required. Paragraph, 2-6 sentences: target behavior from the user's or system's perspective. -->
<Solution description.>

## Users / Use Cases
<!-- Required for user-facing work. Bullet list: one actor, segment, or use case per bullet. -->
- **<Actor or segment>:** <Need, context, or job-to-be-done.>

## Requirements / User Stories
<!-- Required. Use concrete requirements, user stories, or both. Each item must be observable and sliceable. -->
1. As a <actor>, I want <behavior>, so that <benefit>.
- [P0] <Required behavior, rule, edge case, or error state.>

## Out of Scope
<!-- Required. Explicit non-goals and deferred behavior. -->
- <Excluded behavior, technical approach, or future candidate.>

## Technical Decisions
<!-- Required for codebase changes. Include only accepted decisions and constraints useful for slicing or implementation. -->

### Tools & Libraries
- <Library, framework, or tool decision and rationale.>

### Modules & Boundaries
- **<Module or boundary>:** <Responsibility, ownership, or expected change.>

### Data, APIs & Integrations
- <Schema change, API contract, migration, external service, or integration decision.>

### Architecture & Interactions
- <Architecture decision, system interaction, compatibility expectation, or rollback note.>

## Testing Decisions
<!-- Required. Include feedback loops and what deserves automated or manual coverage. -->
- <Unit, integration, e2e, migration, browser, visual, performance, or manual QA decision.>

## Open Questions
<!-- Conditional. Mark blocking questions explicitly. -->
- **Blocking / Non-blocking:** <Question and what would unblock it.>

## Split Notes
<!-- Conditional. Notes for vertical slicing: likely tracer bullet, dependency, risky area, or batching hint. -->
- <Useful slicing note.>

## References
<!-- Conditional. Links or source names, not copied source text. -->
- <Brief, validation note, Technical Design, prototype, issue, customer feedback, ADR, official docs, or durable docs.>
```

**Possible sizes:** lite (single clear feature or technical change); standard (multi-flow feature); full (product-critical, cross-functional, or technically complex initiative).

**Verification:** A reviewer can determine included behavior, excluded behavior, accepted technical decisions, testing expectations, unresolved questions, and sliceability without reading prior chat.

**Human gate:** Validate product scope, ambiguous behaviors, technical decisions, testing decisions, open questions, and readiness for slicing.
