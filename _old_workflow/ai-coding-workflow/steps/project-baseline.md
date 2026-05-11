# Project Baseline

**Skill name:** `project-baseline`

**Step type:** On-demand.

**Role:** Establish durable understanding of an existing project so future agents can work from observed project context instead of rediscovering the repository every session.

**When to use:** Legacy onboarding, abandoned project, poorly documented codebase, takeover of an existing project, first serious use of agents on a repository, or whenever weak durable docs make the project hard to work with.

**Possible inputs:** Repository, README, existing docs, scripts, tests, CI config, architecture, tickets, user context, project conventions, deployment or runtime notes, and existing durable decisions.

**Process:**

1. Bound the baseline scope before exploration: whole repo, one app/package, one bounded context, or one code area.
2. Explore repository structure, current docs, source layout, tests, CI, scripts, runtime/deployment notes, and naming conventions.
3. Identify stable observed facts with source-backed evidence: project purpose, architecture, major modules, data flow, integrations, runtime boundaries, conventions, testing strategy, risk areas, stale docs, and missing decisions.
4. Locate existing durable docs that should be updated.
5. Draft fallback durable docs only when no better source of truth exists.
6. Draft durable doc updates with stable, observed information, then ask before every durable doc write or update.
7. If durable docs are created, moved, or renamed, ask before updating `.agents/rules/context-sources.md` pointers.
8. Summarize updated docs, stable findings, unknowns, risks, and follow-ups.

**Rules:**

- Project Baseline documents observed reality.
- Durable baseline claims must be source-backed. For non-obvious architecture, convention, testing, or domain claims, include source references, confidence, or explicit unknowns.
- Agent rule setup (output guidance, feedback commands, context-source pointers, and agent boundaries) is out of scope except for confirmed context-source pointer updates after durable docs move.
- Product planning and refactoring are out of scope.
- Prefer updating existing durable docs over creating new standalone baseline artifacts.
- Use fallback durable docs only when no better source of truth exists: `docs/architecture.md`, `docs/conventions.md`, `docs/testing-strategy.md`, `CONTEXT.md`, `CONTEXT-MAP.md`, or `docs/decisions/*`.
- Keep `docs/testing-strategy.md` focused on verification strategy, test structure, risk-based checks, and feedback-loop gaps.
- Keep exact executable commands in `.agents/rules/feedback-commands.md`. Do not maintain a parallel command inventory in baseline docs.
- If baseline discovers command drift or missing operational rules, report it as a setup follow-up instead of duplicating it here.
- Do not duplicate output locations, tracker conventions, or agent boundaries in durable docs.

**Output:** Durable project documentation updates plus a concise baseline summary.

**Output location:** Recommended default: ask before writing or updating existing durable docs such as `README.md`, `docs/*`, `CONTEXT.md`, `CONTEXT-MAP.md`, or `docs/decisions/*`. If durable docs are created, moved, or renamed, ask before updating `.agents/rules/context-sources.md`. If an onboarding issue exists, ask before publishing a summary comment. If the user does not confirm, keep the baseline summary in session only.

**Output template:**

```markdown
## Summary
<!-- Required. Paragraph, 1-3 sentences: what was baselined and the headline findings. -->
<Project baseline summary.>

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

## Evidence & Confidence
<!-- Required for non-obvious durable claims. Bullet list: source, claim, confidence, or unknown. -->
- **<Source path or signal>:** <Claim supported, confidence, or remaining unknown.>

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

## Evidence & Confidence
- <Source path or signal, supported claim, confidence, or unknown.>
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

## Evidence & Confidence
- <Source path or signal, supported claim, confidence, or unknown.>
```

```markdown
# Testing Strategy

## Feedback Loops
- <Which verification signals matter and when. Link to `.agents/rules/feedback-commands.md` for exact commands.>

## Test Structure
- <Where tests live and how they are organized.>

## Recommended Verification By Change Type
- <Feature, bug fix, refactor, UI, migration, or release verification guidance.>

## Command Source
- Exact executable commands live in `.agents/rules/feedback-commands.md`.

## Gaps & Limitations
- <Missing, slow, flaky, or unreliable feedback loop.>

## Evidence & Confidence
- <Source path or signal, supported claim, confidence, or unknown.>
```

**Possible sizes:** lite (onboarding); standard (maintained project with weak docs); full (legacy, abandoned, or multi-app repository).

**Verification:** Future agents can understand project purpose, structure, architecture, conventions, testing strategy, domain vocabulary, risks, and documentation gaps from durable docs.

**Human gate:** Validate what becomes project source of truth.
