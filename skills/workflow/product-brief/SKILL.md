---
name: product-brief
description: Creates, initializes, or updates a product brief for an initiative, product idea, greenfield project, or substantial feature. Use when product-level framing is needed around problem, users, value, scope, decisions, assumptions, risks, or constraints.
---

# Product Brief

## Overview

Create or refine a lightweight product brief that frames an initiative before spec, validation, or implementation. The brief is product-first: it captures problem, users, value, scope, assumptions, and risks without becoming a technical spec or task list.

## When To Use

- The user requests creating, initializing, drafting, consolidating, or updating a product brief.
- A vague idea, greenfield project, substantial feature, or product initiative needs clearer product framing.
- Existing conversation, brainstorming notes, research, grilling output, issues, specs, docs, or repo context should be consolidated into a product source of truth.
- The main ambiguity is product-level: problem, users, use cases, value, scope, exclusions, risks, success signals, or constraints.

Do not use this skill for broad brainstorming, market validation, technical specs, task splitting, code implementation, codebase audits, ordinary Q&A, or brief status summaries that do not need an artifact.

## Workflow

### 1. Establish The Artifact

Resolve the initiative and product-brief artifact before writing. Use the project's local artifact conventions for paths, naming, and creation rules.

- Start from any user-provided initiative or artifact path; otherwise inspect existing initiatives and artifacts for a match to the current context.
- If nothing matches, propose a new initiative and a `product-brief.md` artifact.
- Report findings: matched initiative, matched artifact, proposed create/update action, and any ambiguity.
- Ask for confirmation before creating an initiative, creating an artifact, or updating an existing artifact.
- After confirmation, create or update the artifact as needed using [product-brief.md](assets/templates/product-brief.md) template.

If the user explicitly declines an artifact, continue in conversation only and state that no persistent product brief will be maintained.

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

Keep exploration lightweight. Don't do a full codebase exploration. Just enough to clarify the product context.

### 4. Draft The Brief

Use `assets/templates/product-brief.md` as the canonical template for new product briefs and as a structural guide for updates.

- Keep required sections unless the user explicitly requests a narrower artifact.
- Include optional sections only when they add useful information.
- If a section is not relevant for the current context, write `Not relevant` with a short explanation instead of deleting.
- If a section is not known yet, write `Not known yet` instead of deleting, and flag it to the user for clarification.
- Replace template guidance with concrete content; do not leave instructional placeholder prose in the artifact.
- Preserve useful existing content when updating. Reorganize only when it improves clarity or aligns with the product brief structure.
- Keep technical content lightweight in `Technical Notes`. Durable architecture or implementation decisions belong in a spec, task, ADR, or code change, not in the product brief.
- Keep the brief concise enough to guide future work. Prefer crisp bullets over long narrative when detail is uncertain.

Show the draft in conversation and obtain validation before writing or updating the artifact.

### 5. Write Safely

After explicit validation, create or update only the approved artifact.

- Keep the artifact simple Markdown with no frontmatter or metadata block.
- Do not overwrite existing product brief content silently.
- Do not store secrets, credentials, raw personal data, sensitive customer exports, or anything that should not be visible to someone with repo access.

## Guardrails

- Do not turn product-briefing into brainstorming or interview. If the idea space is too open, capture the ambiguity in `Open Questions` or suggest a separate exploratory or grilling session to the user without creating extra artifacts.
- Do not conduct market, competitor, legal, or technical validation by default. Capture unresolved validation needs under `Assumptions To Validate`, `Risks`, or `Open Questions`.
- Do not let code exploration become a heavy codebase audit. Inspect only enough to avoid wrong product/domain assumptions.

## Output

Provide a final summary of files created or updated, key product decisions captured, remaining `Not known yet` items, and suggested next step if obvious.

## Validation

Before finishing, verify:

- [ ] The artifact path was confirmed before creation or initialization.
- [ ] Substantive content was drafted in conversation and explicitly validated before writing.
- [ ] Existing `product-brief.md` or legacy `brief.md` content was inspected and not overwritten silently.
- [ ] Required sections are present unless the user approved a narrower structure.
- [ ] Optional sections appear only when useful.
- [ ] User-provided or referenced context was gathered separately from codebase exploration.
- [ ] Unknowns are marked `Not known yet` instead of invented.
- [ ] Technical notes remain lightweight and do not become a spec or ADR.
- [ ] Source-of-truth rules are respected if a tracker spec already exists.
- [ ] No secrets, credentials, sensitive raw personal data, unsupported tracker automation, triage workflow, spec, task list, or implementation artifact was created as part of this skill.
