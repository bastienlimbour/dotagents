# 003 - Technical Design

**Skill name:** `technical-design`

**Step type:** Core, optional.

**Role:** Resolve material technical uncertainty before accepted technical decisions are integrated into the Spec.

**When to use:** Stack or library choice, architecture change, data model, integration, migration, security, performance, scalability, observability, structural refactor, public interface change, unclear testing strategy, technical feasibility risk, or any technical decision that should be explored before writing the Spec.

**Possible inputs:** Brief, validation note, draft Spec, grill summary, repository context, current architecture, existing technical docs, ADRs, conventions, external services, stack constraints, non-functional requirements, official documentation, library candidates, prototypes.

**Process:**

1. Choose Technical Design size and list the technical questions it must resolve.
2. Confirm product direction is stable enough for technical decisions; treat unstable product scope as a blocker.
3. Explore relevant repository patterns, modules, tests, feedback commands, and current constraints.
4. Read durable vocabulary, context maps, and ADRs when available.
5. Check official documentation or credible primary sources for version-sensitive framework, library, API, or platform decisions.
6. Interview the user one question at a time for decisions that code, docs, or sources cannot answer; provide a recommendation for each question.
7. Compare alternatives when a decision has real trade-offs.
8. Define accepted technical decisions for stack, libraries, modules, interfaces, data, APIs, integrations, migrations, security, performance, observability, compatibility, rollback, and testing when relevant.
9. Identify risks, open questions, and ADR candidates.
10. Summarize exactly what should be integrated into the Spec.
11. After drafting, ask before publishing the design, writing a local artifact, or creating durable ADRs.

**Rules:**

- Technical Design clarifies decisions; it is not the parent initiative source of truth.
- Accepted decisions from Technical Design must be integrated into the Spec before slicing or implementation depends on them.
- Use the smallest useful size. If only a few obvious technical decisions exist, put them directly in the Spec instead of creating a separate Technical Design artifact.
- Do not solve unstable product scope here; return product questions to Brief, Validate, Grill Me, or Grill With Docs.
- Do not turn the output into task sequencing or brittle file-by-file implementation instructions.
- Propose ADRs only for durable decisions with useful long-term context.

**Output:** Markdown Technical Design note that resolves technical questions, compares meaningful alternatives, records accepted decisions and rationale, and lists what must be integrated into the Spec.

**Output location:** Recommended default: session output while drafting a Spec, or local `.initiatives/001-<initiative>/technical-design.md` when a reusable artifact is useful. If a parent issue already exists, ask before publishing as a parent issue comment. Every issue comment, local file write/update, or ADR write/update requires confirmation. If the user does not confirm, keep the Technical Design in session only.

**Output template:**

```markdown
# <Initiative> Technical Design

## Summary
<!-- Required. Paragraph, 2-5 sentences: technical questions resolved and recommended direction. -->
<Technical design summary.>

## Questions To Resolve
<!-- Required. Bullet list: the technical decisions this artifact exists to answer. -->
- <Technical question and why it matters.>

## Current State
<!-- Required. Paragraph or bullet list: relevant architecture, modules, constraints, and existing behavior. -->
<Current technical state.>

## Options Considered
<!-- Required when trade-offs exist. One subsection per option. -->

### <Option>
- **Pros:** <Useful advantage.>
- **Cons:** <Cost, risk, or limitation.>
- **Sources:** <Official docs, code reference, ADR, or observed evidence.>

## Accepted Technical Decisions
<!-- Required. Decision list; include rationale and source when useful. -->
- **Decision:** <Choice>
  **Rationale:** <Trade-off and source when useful.>

## Interfaces, Data & Boundaries
<!-- Conditional. Bullet list: include only important interfaces, modules, data objects, seams, or boundaries. -->
- **<Interface / module / data object>:** <Responsibility, invariants, callers, and ownership.>

## Testing & Verification Decisions
<!-- Required. Bullet list: technical feedback loops to carry into the Spec. -->
- <Unit, integration, e2e, migration, browser, performance, observability, or manual check.>

## Risks, Rollback & Compatibility
<!-- Conditional. Bullet list: include risk, mitigation, rollback path, or compatibility note. -->
- **<Risk>:** <Mitigation, rollback path, or compatibility note.>

## Open Questions
<!-- Conditional. Bullet list: technical questions that still block or shape the Spec. -->
- <Technical question and what would unblock it.>

## Integrate Into Spec
<!-- Required. Bullet list: accepted decisions or notes that must be copied or summarized into the Spec. -->
- <Spec-ready technical decision, testing decision, risk, or open question.>

## References
<!-- Conditional. Bullet list: Brief, validation, ADR, official docs, issue, or relevant code area. -->
- <Reference.>
```

**Possible sizes:** lite (one technical decision or library choice); standard (multi-module feature or integration); full (architecture, migration, security, performance, or structural refactor work).

**Verification:** The design resolves the targeted technical questions, cites useful sources or code evidence, states accepted decisions and trade-offs, identifies risks and open questions, and provides Spec-ready technical content.

**Human gate:** Validate technical trade-offs, module boundaries, public interfaces, migrations, security/privacy decisions, and durable decisions before they are integrated into the Spec.
