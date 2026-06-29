---
name: to-spec
description: Turns conversation, briefs, research, issues, docs, and codebase context into a canonical implementation spec. Use when the user is ready to formalize what should be built before task splitting or implementation; not for product briefs, validation reports, task creation, or code changes.
---

# To Spec

Create or update a canonical spec that captures what should be built, durable product and technical decisions, and constraints needed for safe task splitting and implementation. The spec is product plus technical direction, not a PRD, task list, or file-by-file implementation plan.

## When To Use

- The user asks to create, draft, publish, write, update, or consolidate a spec.
- Conversation, product brief, brainstorming, validation, research, issues, docs, or codebase exploration should become the source of truth for what to build.
- A feature is clear enough for stable user stories, explicit scope, constraints, decisions, testing direction, and acceptable open questions.

Do not use for product briefs, validation reports, task splitting, implementation, code review, QA checklists, or ADRs.

## Workflow

### 1. Resolve Canonical Target

Determine whether this is a new spec, an update to an existing spec, or a draft in conversation only.

- Start from any user-provided issue, artifact path, initiative, or spec reference.
- If updating, inspect the existing spec first and preserve stable user story IDs.
- Respect issue tracker and local artifact conventions already in context.
- If no convention exists, recommend GitHub Issues for GitHub remotes, GitLab Issues for GitLab remotes, otherwise markdown local under `.initiatives/<id>/spec.md`.
- If the target is ambiguous, report the likely target and ask for confirmation before treating it as canonical.

Target confirmation approves only where the spec should live. Complete draft content still requires explicit approval before writing or publishing.

### 2. Gather And Verify Context

Collect explicit context first:

- Conversation.
- Existing spec or tracker issue.
- User-provided files and notes.
- Product brief, brainstorming, validation, research, or handoff notes.
- Issues, tasks, comments, tickets, docs, and linked artifacts.

Inspect repo/docs only when they clarify terminology, current behavior, system boundaries, integration points, constraints, or testing surfaces.

Use project docs, `CONTEXT.md`, `CONTEXT-MAP.md`, ADRs, relevant code, tests, schemas, routes, APIs, config, or package boundaries. If repo/docs can answer, inspect before asking. Do not perform a general audit.

### 3. Clarify Spec Decisions

Ask one targeted question at a time only when the missing answer would materially change the spec. Prefer carrying acceptable uncertainty in `Risks And Open Questions` over running a long interview.

Clarify or confirm when needed:

- Scope and out of scope.
- Actors, workflows, variants, and edge cases.
- Durable product decisions.
- Durable implementation direction, seams, key modules/interfaces, deep-module opportunities, and architecture constraints.
- Testing strategy, regression risks, feedback loops, and main zones to test.
- Privacy, security, performance, compatibility, rollout, dependencies, and project conventions.

Before final draft approval, explicitly confirm key modules/interfaces and main zones to test unless unambiguous from context.

### 4. Draft And Check

Use `assets/templates/spec.md` for new specs and as the reference shape for updates.

- Replace all template guidance with concrete content.
- Use project domain language and respect ADRs and documented conventions; surface contradictions before overriding them.
- Keep the spec durable enough to survive implementation changes and precise enough for later vertical task splitting.
- Capture important decisions and constraints, not every implementation step.
- Use enough user stories to cover actors, flows, variants, edge cases, and benefits without padding.
- Use stable immutable IDs: `US-001`, `US-002`, etc. Never renumber existing IDs; mark invalid stories as `Deprecated` or `Replaced by US-0XX` and assign new IDs after the current maximum.
- Include prototype snippets only when they encode a durable decision better than prose, and label them as prototype-derived.

Before showing the draft, check required sections, no placeholders, no scope contradictions, correct product/implementation/testing decision separation, explicit risks, and no fragile implementation detail.

### 5. Validate And Publish

Show the complete draft in conversation. Revise until the user explicitly approves the content.

After approval, write or publish only to the confirmed canonical target.

If `gh` or `glab` is required but unavailable or unauthenticated, report the blocker and concrete next action; do not silently switch trackers.

For markdown local, write `.initiatives/<id>/spec.md` with simple Markdown unless local tracker conventions require lightweight issue metadata.

Do not create the following unless the user separately asks and confirms:

- Task issues or task files.
- QA comments.
- ADRs or global docs.
- Implementation changes.
- Triage labels, autonomous loops, local initiative indexes, or `decision-log.md`.

Do not include secrets, credentials, raw personal data, sensitive customer exports, or confidential material.

## Guardrails

- Keep the spec focused on what to build and durable decisions needed to build it correctly.
- Do not include KPIs, market validation, success metrics, why-now rationale, or default acceptance criteria.
- Do not include exhaustive file-by-file plans, line numbers, fragile snippets, pseudo-code, or micro-steps unless a prototype snippet is the clearest durable decision record.

## Output

End with:

- Canonical spec location.
- Source context used.
- Key product and implementation decisions.
- Main constraints and testing decisions.
- Remaining risks or open questions.
- Files or tracker artifacts created or updated.

## Validation

Before finishing, verify:

- Target confirmation and explicit draft approval.
- Repo/docs evidence was used before asking when it could answer.
- Conventions and ADRs were respected, or contradictions were surfaced.
- Scope and out-of-scope are explicit.
- Material constraints are captured.
- Product, implementation, and testing decisions are separated.
- User story IDs are stable.
- Risks and open questions are documented.
- No forbidden artifact or sensitive data was introduced.
