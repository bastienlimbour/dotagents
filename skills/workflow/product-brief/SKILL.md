---
name: product-brief
description: Creates, initializes, or updates a product brief for an initiative, product idea, greenfield project, or substantial feature. Use when product-level framing is needed around problem, target users, scenarios, value, current/future scope, product model, decisions, assumptions, risks, constraints, or architecture handoff notes.
---

# Product Brief

## Overview

Create or refine a lightweight product brief that frames an initiative before validation, architecture research, spec, or implementation. The brief is product-first and PRD-light: it aligns on problem, users, scenarios, value, scope horizons, assumptions, decisions, and risks without becoming a full PRD, technical spec, or task list.

## When To Use

- The user requests creating, initializing, drafting, consolidating, or updating a product brief.
- A vague idea, greenfield project, substantial feature, or product initiative needs clearer product framing.
- Existing conversation, brainstorming notes, research, grilling output, issues, specs, docs, or repo context should be consolidated into a product source of truth.
- The main ambiguity is product-level: problem, users, scenarios, value, current/future scope, product model, exclusions, risks, success signals, or constraints.

Do not use this skill for broad brainstorming, market validation, technical specs, task splitting, code implementation, codebase audits, ordinary Q&A, or brief status summaries that do not need an artifact.

## Workflow

### 1. Resolve Brief Target

Resolve the initiative and `product-brief` artifact before writing.

Use this step only to identify create/update mode and the artifact target; collect substantive product content in the next steps.

Use the project's local artifact conventions for paths, naming, and creation rules.

- Start from any user-provided initiative or artifact path; otherwise inspect existing initiatives and artifacts for a match to the current context.
- If the user is updating an existing brief artifact, inspect that artifact before drafting and preserve useful content.
- If nothing matches, propose a new initiative and a `product-brief.md` artifact, unless the project conventions use a different artifact filename.
- Report findings: matched initiative, matched artifact, proposed create/update action, and any ambiguity.
- Ask for confirmation before creating an initiative or selecting an artifact path. This confirmation approves the target only.
- After target confirmation, continue to the next step of this workflow. Do not create the artifact or draft substantive content during this step.

If the user explicitly declines an artifact, continue in conversation only and clearly state that no persistent `product-brief` will be maintained.

### 2. Gather Context

Collect everything that might be relevant in the conversation context:

- Current conversation.
- User-provided notes or files.
- Existing product brief.
- User-provided or referenced brainstorming, research, validation, or grilling notes.
- User-provided or referenced issues, tickets, or tracker items.
- User-provided or referenced specs, tasks, or project docs.
- Any other context that might be relevant for the product brief.

### 3. Explore Codebase

Inspect codebase sources only when they can reveal product terminology, current behavior, domain constraints, or existing system boundaries:

- `CONTEXT.md`, `CONTEXT-MAP.md`, README files, project docs, ADRs, and nearby domain docs.
- Relevant code paths, tests, schemas, routes, UI flows, or configuration when they reveal current behavior or constraints.

Keep exploration lightweight. Do not do a full codebase exploration or codebase audit; inspect only enough to clarify product context and avoid wrong assumptions.

### 4. Classify Scope Horizons

Before drafting, sort captured material by horizon so the brief can discuss the whole product without confusing what is being built now.

- `Current Scope`: included in the current initiative, release, MVP, or feature iteration.
- `Near-term follow-up`: likely next iteration or important adjacent capability, but not included now.
- `Future possibilities`: plausible later expansion paths that are not yet committed.
- `Out Of Scope`: explicit exclusions only, not ordinary future ideas.
- `Open Questions`: unresolved decisions needed before validation, architecture, spec, or implementation.

If a capability could belong to more than one horizon, do not guess. Ask one targeted question when it materially affects the brief, or mark it as an open question.

Do not discard future product direction. Capture important post-current-scope capabilities under `Near-term follow-up` or `Future possibilities`, not as implicit current scope.

### 5. Draft And Check The Brief

Use `assets/templates/product-brief.md` as the canonical template for new product briefs and as a structural guide for updates.

Prepare the draft:

- Align on what to build, why, for whom, the current scope, and what must be clarified next.
- Keep template sections visible. If a section is not relevant for the current context or adds no useful information, write `Not relevant` with a short explanation instead of deleting.
- Clearly label items as current, near-term, or future when horizon ambiguity would matter.
- If an important section is not known yet, write `Not known yet` and flag it to the user for clarification.
- Replace template guidance with concrete content; do not leave instructional placeholder prose in the artifact.
- Preserve useful existing content when updating. Reorganize only when it improves clarity or aligns with the product brief structure.
- Keep the brief concise enough to guide future work. Prefer crisp bullets over long narrative when detail is uncertain.
- Do not turn the brief into a full PRD. Avoid exhaustive user stories, detailed requirements, backlog items, implementation plans, design specifics, detailed telemetry plans, or architecture design.

Coherence check before showing the draft:

- No capability appears as current in one section and later or excluded in another.
- `Solution Direction` does not implicitly promise capabilities outside `Current Scope` unless labelled as near-term or future.
- Information about current, near-term, or future items are clearly labeled when horizon ambiguity would matter.
- `Later Scope` does not contain explicit exclusions, and `Out Of Scope` does not contain ordinary future ideas.
- `Assumptions To Validate` are phrased as testable bets when possible.
- `Open Questions` are unresolved decisions, not parking-lot ideas.

Then show the draft in conversation and obtain explicit content validation before writing or updating the artifact.

### 6. Write The Brief

After explicit content validation, create or update only the approved artifact path.

- Keep the artifact simple Markdown with no frontmatter or metadata block.
- Do not overwrite existing product brief content silently.
- Do not store secrets, credentials, raw personal data, sensitive customer exports, or anything that should not be visible to someone with repo access.

## Guardrails

- Keep this skill focused on product framing. If the idea space is too open, capture ambiguity in `Open Questions` or suggest a separate exploratory or grilling session without creating extra artifacts.
- Do not conduct market, competitor, legal, or technical validation by default. Capture unresolved validation needs under `Assumptions To Validate`, `Risks`, or `Open Questions`.
- Do not create tracker issues, specs, task lists, implementation artifacts, or extra workflow artifacts unless the user explicitly asks for them.

## Output

At the end of the task, provide:

- A final summary of files created or updated.
- Key product decisions captured.
- Remaining `Not known yet` items.
- Suggested next step if obvious.

## Validation

Before finalizing, verify:

- [ ] The artifact target was confirmed before creation or update, and substantive content was written only after explicit draft validation.
- [ ] Existing product brief content was inspected and not overwritten silently.
- [ ] Unknowns are marked `Not known yet` instead of invented.
- [ ] Sections that lack useful content are marked `Not relevant` or `Not known yet` with a short explanation instead of being silently deleted or filled with placeholder prose.
- [ ] Scope horizons are clear: current scope, near-term follow-up, future possibilities, explicit exclusions, and open questions are not mixed.
- [ ] `Solution Direction` does not promise unlabelled capabilities outside the current scope.
- [ ] `Product Model`, `Product Rules`, `Decisions Made`, `Assumptions To Validate`, and `Open Questions` use the right category and do not duplicate each other.
- [ ] Technical handoff notes remain lightweight and do not become a spec, detailed architecture doc, or ADR.
- [ ] No secrets, credentials, sensitive raw personal data, unsupported tracker automation, triage workflow, spec, task list, or implementation artifact was created as part of this skill.
