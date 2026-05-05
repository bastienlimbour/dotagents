# Project Baseline

**Skill name:** `project-baseline`

**Step type:** On-demand step.

**Role:** Establish durable understanding of an existing project so future agents can work from observed project context instead of rediscovering the repository every session.

**When to use:** Legacy onboarding, abandoned project, poorly documented codebase, takeover of an existing project, first serious use of agents on a repository, or after `Workflow Setup` identifies weak durable docs.

**Possible inputs:** Repository, README, existing docs, scripts, tests, CI config, architecture, tickets, user context, project conventions, deployment or runtime notes, `.agents/workflow/context-loading.md`, and existing durable decisions.

**Process:**

1. Bound the baseline scope before exploration: whole repo, one app/package, one bounded context, or one code area.
2. Explore repository structure, current docs, source layout, tests, CI, scripts, runtime/deployment notes, and naming conventions.
3. Identify stable observed facts: project purpose, architecture, major modules, data flow, integrations, runtime boundaries, conventions, testing strategy, risk areas, stale docs, and missing decisions.
4. Locate existing durable docs that should be updated.
5. Create fallback durable docs only when no better source of truth exists.
6. Update durable docs with stable, observed information.
7. If durable docs are created, moved, or renamed, update only the pointers and load rules in `.agents/workflow/context-loading.md` when it exists.
8. Summarize updated docs, stable findings, unknowns, risks, and follow-ups.

**Rules:**

- `Project Baseline` documents observed reality.
- Workflow configuration belongs to `Workflow Setup`; product planning and refactoring happen in later steps.
- Check whether `Workflow Setup` exists when output locations, feedback command routing, or agent boundaries are needed.
- Prefer updating existing durable docs over creating new standalone baseline artifacts.
- Use fallback durable docs only when no better source of truth exists: `docs/architecture.md`, `docs/conventions.md`, `docs/testing-strategy.md`, `CONTEXT.md`, `CONTEXT-MAP.md`, or `docs/decisions/*`.
- Keep `docs/testing-strategy.md` focused on verification strategy, test structure, risk-based checks, and feedback-loop gaps.
- Keep exact executable commands in `.agents/workflow/feedback-commands.md`. Do not maintain a parallel workflow command inventory in baseline docs.
- If baseline discovers command drift, report a `Workflow Setup` follow-up instead of duplicating command lists.
- Do not duplicate output locations, tracker conventions, or agent boundaries in durable docs.

**Output:** Durable project documentation updates plus a concise baseline summary.

**Output location:** Recommended default: existing durable docs such as `README.md`, `docs/*`, `CONTEXT.md`, `CONTEXT-MAP.md`, or `docs/decisions/*`. Use `.agents/workflow/context-loading.md` only for pointers to durable docs. If an onboarding issue exists, publish a summary comment using `.agents/workflow/output-locations.md` when available.

**Output template:**

```markdown
## Project Baseline Summary

## Scope
<!-- Required. One sentence or bullet list: what was baselined and what was not. -->
<Baseline scope.>

## Durable Docs Updated
<!-- Required when files changed. Bullet list: file and purpose. -->
- **<File>:** <Purpose of update.>

## Project Understanding
<!-- Required. Concise summary or links to durable docs. -->
- Purpose: <observed project purpose>
- Architecture: <link to durable architecture source or short observed summary>
- Conventions: <link to durable conventions source or short observed summary>
- Testing strategy: <link to durable testing source or short observed summary>
- Domain / decisions: <links to durable domain or decision sources>

## Risk Areas & Gaps
<!-- Conditional. Bullet list: risk, inconsistency, missing feedback loop, stale doc, or unknown area. -->
- <Risk area or gap.>

## Follow-ups
<!-- Conditional. Bullet list: recommended setup, docs, testing, refactor, or decision follow-up. -->
- <Follow-up.>
```

Fallback durable doc templates:

```markdown
# Architecture

## System Overview
<What the system does and its main runtime parts.>

## Main Boundaries
- <App, package, service, module, or bounded context.>

## Data Flow
- <Important request, event, job, persistence, or integration flow.>

## Key Dependencies
- <Framework, service, database, queue, API, or external system.>

## Risks & Unknowns
- <Observed architectural risk, stale area, or unanswered question.>
```

```markdown
# Conventions

## Code Organization
- <Observed file, module, package, or boundary convention.>

## Naming & Domain Language
- <Observed naming rule or stable domain term.>

## Implementation Patterns
- <Observed pattern agents should preserve.>

## Testing Conventions
- <Observed testing style or placement rule.>

## Documentation Conventions
- <Where durable decisions, docs, or project notes belong.>
```

```markdown
# Testing Strategy

## Feedback Loops
- <Which verification signals matter and when. Link to `.agents/workflow/feedback-commands.md` for exact commands.>

## Test Structure
- <Where tests live and how they are organized.>

## Recommended Verification By Change Type
- <Feature, bug fix, refactor, UI, migration, or release verification guidance.>

## Command Source
- Exact executable commands live in `.agents/workflow/feedback-commands.md`.

## Gaps & Limitations
- <Missing, slow, flaky, or unreliable feedback loop.>
```

**Possible sizes:** Quick baseline for onboarding; standard baseline for a maintained project with weak docs; full baseline for a legacy, abandoned, or multi-app repository.

**Verification:** Future agents can understand project purpose, structure, architecture, conventions, testing strategy, domain vocabulary, risks, and documentation gaps from durable docs.

**Human gate:** Validate what becomes project source of truth.
