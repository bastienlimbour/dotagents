---
name: setup-skills-workflow
description: Sets up, audits, or realigns a project's agent conventions for efficiently using the skills-based AI coding workflow. Use when the user asks "setup agent workflow", "install the skills workflow", "setup the AI coding workflow", or any other variant of these phrases.
---

# Setup Skills Workflow

## Overview

Configure project-specific conventions for the skills-based AI coding workflow. This is prompt-driven: explore, report findings, decide one convention at a time, preview changes, then write only after confirmation.

## When To Use

- A repo needs first-time setup for the skills-based AI coding workflow.
- Existing agent rules need audit, cleanup, or realignment with the workflow.
- The user asks to configure workflow conventions for issues, local artifacts, documentation, domain context, or ADRs.

Do not use to create feature specs, split tasks, implement code, run triage automation, or create initiative artifacts unless separately requested.

## Workflow

### 1. Explore

Inspect before recommending changes:

- Git remote and tracker type: GitHub, GitLab, or other.
- Matching CLI availability/authentication: `gh` or `glab`.
- Root agent instruction files: `CLAUDE.md`, `AGENTS.md`, and any existing `## Workflow Conventions`.
- Existing `docs/agents/` content from prior setup.
- Existing `CONTEXT.md`, `CONTEXT-MAP.md`, root or nested `docs/decisions/`, `.initiatives/`, and project/workflow conventions in docs.

Absent files are not errors. If both `CLAUDE.md` and `AGENTS.md` exist, ask which is canonical before proposing workflow convention edits.

### 2. Report Findings

Briefly summarize:

- Agent files.
- Issue tracker and CLI status.
- Local artifact conventions.
- Documentation and ADR conventions.
- Useful missing pieces or drift.

If a CLI is missing or unauthenticated, report the concrete next setup action; do not silently switch tracker conventions.

### 3. Decide One Convention At A Time

For each unresolved material choice, give a short explanation, recommend one option, ask one question, and wait.

Decide only what is not already clear:

- Issue tracker: GitHub via `gh`, GitLab via `glab`, or local markdown under `.initiatives/`.
- Local artifacts: always maintain guidance; decide only whether to create `.initiatives/` now.
- Domain context: create `CONTEXT.md` only when useful domain vocabulary is known.
- Context map: create `CONTEXT-MAP.md` only for multi-context repos or confirmed need.
- ADRs: decide whether durable architecture decisions should live in `docs/decisions/`.
- Agent file: use canonical existing file, or ask whether to create `CLAUDE.md` or `AGENTS.md` when neither exists.

Default tracker recommendation follows the remote: GitHub for GitHub, GitLab for GitLab, local markdown otherwise. The user may still choose local markdown.

Always create or maintain `docs/agents/issue-tracker.md`, `docs/agents/local-artifacts.md`, and `docs/agents/documentation.md`. Issue operations use the selected tracker; local artifact operations always use local artifact conventions.

### 4. Prepare Changes

Load only templates needed for confirmed choices:

| Target | Template |
| --- | --- |
| `CLAUDE.md` or `AGENTS.md` | [conventions.md](assets/templates/conventions.md) |
| `docs/agents/issue-tracker.md` | [issue-tracker-github.md](assets/templates/issue-tracker-github.md), [issue-tracker-gitlab.md](assets/templates/issue-tracker-gitlab.md), or [issue-tracker-local.md](assets/templates/issue-tracker-local.md) |
| `docs/agents/local-artifacts.md` | [local-artifacts.md](assets/templates/local-artifacts.md) |
| `docs/agents/documentation.md` | [documentation.md](assets/templates/documentation.md) |
| `CONTEXT.md` | [context.md](assets/templates/context.md) |
| `CONTEXT-MAP.md` | [context-map.md](assets/templates/context-map.md) |

Use templates as scaffolds, not blind output.

- Replace placeholders with project-specific conventions.
- Update natural Markdown sections in place.
- Do not use managed-block markers.
- Do not duplicate `Issue Tracker`, `Local Artifacts`, or `Documentation` sections.
- Preserve unrelated user rules.
- Keep `CLAUDE.md`/`AGENTS.md` short and put details in `docs/agents/`.

Before writing, preview files to create/update and the intended change for each. Wait for explicit confirmation.

### 5. Write Safely

After confirmation, create or update only approved files.

## Output

During the run, provide:

- Concise findings summary.
- One decision question at a time with recommendation.
- Pre-write preview.
- Final summary of files changed, conventions chosen, skipped optional items, validation performed, and remaining setup actions.

## Validation

Before finishing, verify:

- The agent file points to the three `docs/agents/` convention files without duplicating their details.
- Unrelated user instructions were preserved.
- The selected tracker matches `issue-tracker.md`.
- Local artifacts remain documented regardless of tracker.
- `CONTEXT.md` and `CONTEXT-MAP.md` were not created speculatively.
- No v1 out-of-scope artifacts were created.
