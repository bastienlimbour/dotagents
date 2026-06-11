---
name: product-brief
description: Creates, initializes, or updates a product brief for an initiative, product idea, greenfield project, or substantial feature. Use when product-level framing is needed around problem, target users, scenarios, value, current/future scope, product model, decisions, assumptions, risks, constraints, or architecture handoff notes.
---

# Product Brief

## Overview

Create or refine a lightweight product brief that frames an initiative before validation, architecture research, spec, or implementation. The brief is product-first and PRD-light: problem, users, scenarios, value, scope horizons, assumptions, decisions, and risks.

## When To Use

- The user asks to create, initialize, draft, consolidate, or update a product brief.
- A vague idea, greenfield project, substantial feature, or product initiative needs clearer product framing.
- Existing conversation, brainstorming, research, grilling, issues, specs, docs, or repo context should become a product source of truth.

Do not use for brainstorming, validation reports, technical specs, task splitting, implementation, or brief status summaries that do not need an artifact.

## Workflow

### 1. Resolve Target

Resolve the initiative and `product-brief` artifact before drafting.

- Respect local artifact conventions already in context. If absent, use `.initiatives/<NNN-slug>/product-brief.md` with simple Markdown and no frontmatter.
- Start from any user-provided initiative or path; otherwise inspect existing initiatives and artifacts for a likely match.
- If updating, inspect the existing brief and preserve useful content.
- If no target matches, propose one initiative and artifact path.
- Report the matched or proposed target, create/update mode, and ambiguity. Ask for confirmation before creating an initiative or selecting a path.

Target confirmation approves only where the brief should live. If the user declines an artifact, continue in conversation only.

### 2. Gather Context

Use relevant context from:

- Current conversation.
- User-provided or referenced notes and files.
- Existing briefs.
- Brainstorming, research, validation, or grilling notes.
- Issues, specs, tasks, and project docs.

Inspect codebase/docs only when they clarify product terminology, current behavior, domain constraints, or system boundaries.

Prefer `CONTEXT.md`, `CONTEXT-MAP.md`, README/project docs, ADRs, nearby domain docs, and relevant code/tests/schemas/routes/UI/config. Keep exploration focused; do not do a codebase audit.

### 3. Classify Scope Horizons

Before drafting, sort material so the brief can discuss the whole product without confusing what is being built now.

- `Current Scope`: included now.
- `Near-term follow-up`: likely next iteration, not included now.
- `Future possibilities`: plausible later expansion, not committed.
- `Out Of Scope`: explicit exclusions only.
- `Open Questions`: unresolved decisions needed before validation, architecture, spec, or implementation.

Do not guess ambiguous horizon placement. Ask one targeted question when it materially affects the brief, or mark it as an open question. Preserve important future direction without making it current scope.

### 4. Draft And Check

Use `assets/templates/product-brief.md` for new briefs and as a structural guide for updates.

- Replace template guidance with concrete content; never leave placeholder prose.
- Keep template sections visible. Use `Not relevant` or `Not known yet` with a short explanation instead of deleting or inventing content.
- Build a non-redundant narrative: `Problem / Opportunity` -> `Target Users & Use Cases` -> `Current Journey / Context` -> `Proposed Solution` -> `Value Proposition`.
- Keep scope horizons consistent across sections; `Proposed Solution` must not silently promise later or excluded capabilities.
- Phrase `Assumptions To Validate` as testable bets when possible.
- Keep technical/architecture notes lightweight; do not turn them into a spec, ADR, schema, API contract, or implementation plan.
- Preserve useful existing content and reorganize only when it improves clarity.

Show the draft in conversation and obtain explicit content validation before writing or updating the artifact.

### 5. Write

After content validation:

- Create or update only the approved artifact path.
- Do not overwrite existing brief content silently.
- Do not include secrets, credentials, raw personal data, sensitive customer exports, or confidential material.

## Guardrails

- Keep this skill focused on product framing. If the idea space is too open, capture ambiguity in `Open Questions` or suggest a separate exploratory/grilling session.
- Do not conduct market, competitor, legal, or technical validation by default; capture those needs under `Assumptions To Validate`, `Risks`, or `Open Questions`.
- Do not create tracker issues, specs, task lists, implementation artifacts, or extra workflow artifacts unless the user explicitly asks and confirms.

## Output

End with:

- Files created or updated.
- Key product decisions captured.
- Remaining `Not known yet` items.
- An obvious next step if one exists.

## Validation

Before finishing, verify:

- Target confirmation and explicit draft approval.
- No silent overwrite.
- Clear scope horizons.
- Non-redundant opening narrative.
- Unknowns marked instead of invented.
- Lightweight technical handoff.
- No sensitive data or unrelated artifacts.
