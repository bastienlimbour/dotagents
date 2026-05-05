# 004 - Tech Design

**Skill name:** `tech-design`

**Step type:** Core workflow step (required, except for trivial changes).

**Role:** Define the technical approach, interfaces, trade-offs, and verification strategy needed to build the accepted product behavior.

**When to use:** Architecture change, data model, integration, migration, security, performance, scalability, observability, structural refactor, durable stack choice, or non-trivial implementation uncertainty.

**Possible inputs:** PRD, grill summary, repository context, current architecture, existing technical docs, ADRs, conventions, external services, stack constraints, non-functional requirements.

**Process:**

1. Choose Tech Design size before writing.
2. Confirm PRD scope and unresolved product questions.
3. Explore relevant repository patterns, tests, and feedback commands.
4. Read durable vocabulary, context maps, and ADRs when available.
5. Document relevant current state, constraints, and technical requirements.
6. Propose target architecture, modules, interfaces, seams, data model, integrations, and migrations when relevant.
7. Identify stable invariants, error modes, compatibility expectations, and rollback considerations.
8. Compare alternatives when a decision has real trade-offs.
9. Define technical testing and verification strategy.
10. Propose ADRs for durable, surprising, or hard-to-reverse decisions.

**Rules:**

- Tech Design usually follows PRD.
- If technical feasibility is the main uncertainty, run a lightweight spike first, then complete the Tech Design after product scope is clear.
- Check official documentation for version-sensitive framework or library decisions.
- Explain how to build the PRD safely without turning the design into task sequencing.
- Propose ADRs only for durable decisions with useful long-term context.

**Output:** Markdown Tech Design that explains how to build the PRD safely without turning the design into task sequencing.

**Output location:** Check `.agents/workflow/output-locations.md` when it exists. Recommended default: short Tech Design section in the parent issue body for lite designs; detailed parent issue comment for non-trivial designs. Local Markdown alternative: `.initiatives/<initiative>/tech-design.md`. Durable decisions may also become ADRs.

**Output template:**

```markdown
# <Initiative> Tech Design

## Summary
<!-- Required. Paragraph, 2-5 sentences: technical approach and why it fits the PRD. -->
<Technical summary.>

## Current State
<!-- Required. Paragraph or bullet list: relevant architecture, modules, constraints, and existing behavior. -->
<Current technical state.>

## Technical Constraints
<!-- Required when constraints shape the design. Bullet list. -->
- <Non-functional requirement, platform constraint, compatibility need, or project convention.>

## Proposed Approach
<!-- Required. Paragraph plus optional bullets: target architecture and main implementation strategy. -->
<Proposed technical approach.>

## Interfaces, Data & Boundaries
<!-- Conditional. Bullet list: include only important interfaces, modules, data objects, seams, or boundaries. -->
- **<Interface / module / data object>:** <Responsibility, invariants, callers, and ownership.>

## Key Decisions
<!-- Required for non-obvious choices. Decision list; include trade-off and source when useful. -->
- **Decision:** <Choice>
  **Rationale:** <Trade-off and source when useful.>

## Testing & Verification
<!-- Required. Bullet list: technical feedback loops expected during Build and release. -->
- <Unit, integration, e2e, migration, browser, performance, or observability check.>

## Risks, Rollback & Compatibility
<!-- Conditional. Bullet list: include risk, mitigation, rollback path, or compatibility note. -->
- **<Risk>:** <Mitigation, rollback path, or compatibility note.>

## Open Questions
<!-- Conditional. Bullet list: technical questions that block or shape execution. -->
- <Technical question that blocks or shapes execution.>

## References
<!-- Conditional. Bullet list: PRD, ADR, official docs, issue, or relevant code area. -->
- <Reference.>
```

**Possible sizes:** Tech Design Lite for a limited implementation choice; standard Tech Design for a multi-module feature; full Tech Design for architecture, migration, security, performance, or structural refactor work.

**Verification:** The design identifies current state, target approach, important interfaces, technical decisions, test strategy, risks, rollback/compatibility concerns, and open questions enough for `Slice` or `Build` to proceed.

**Human gate:** Validate technical trade-offs, module boundaries, public interfaces, migrations, and durable decisions before `Slice` or `Build`.
