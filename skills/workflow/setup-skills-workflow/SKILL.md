---
name: setup-skills-workflow
description: Configures or realigns the skills-based AI coding workflow conventions in a project repo. Use when the user asks "setup skills workflow", "setup agents workflow", "setup AI coding workflow", or any similar trigger phrases.
---

# Setup Skills Workflow

Configure project-specific conventions for the skills-based AI coding workflow.

This is prompt-driven: explore, report findings, ask one decision question at a time, preview changes, then write only after confirmation.

## When To Use

- A project needs first-time setup for the skills-based AI coding workflow.
- The project needs audit, cleanup, or realignment with the workflow.
- The user asks to configure workflow conventions for issues, local artifacts, documentation, domain context, or ADRs.

## Workflow

### 1. Explore

Inspect before recommending changes:

- Git remote and tracker type: GitHub, GitLab, or other (`git remote -v`, `.git/config`).
- Matching CLI availability/authentication: `gh` or `glab`.
- Root agent instructions files: `AGENTS.md` or `CLAUDE.md`, and any existing `## Skills Workflow` sections.
- Existing `docs/agents/` content from prior setup.
- Existing `CONTEXT-MAP.md`, `CONTEXT.md`, `**/CONTEXT.md`, `docs/decisions/`, `**/docs/decisions/`, or `.initiatives/`.

If both `CLAUDE.md` and `AGENTS.md` exist, ask which is canonical before proposing workflow convention edits.

### 2. Report Findings

Briefly summarize what's present and what's missing:

- Agent instructions files.
- Issue tracker and CLI status.
- Local artifacts conventions.
- Documentation and ADR conventions.
- Useful missing pieces or drift.

If a CLI is missing or unauthenticated, report the concrete next setup action; do not silently switch tracker conventions.

### 3. Ask One Decision Question At A Time

For each unresolved material choice, ask one question at a time with short explanations, options, and your recommended choice, and wait for the answer. Don't dump all questions at once.

Ask about what is not already clear:

- Issue tracker: GitHub via `gh`, GitLab via `glab`, or local markdown under `.initiatives/`.
- Local artifacts: always maintain guidance; ask only whether to create `.initiatives/` now.
- Domain docs - confirm the file structure:
  - Single-context: one `CONTEXT.md` at the repo root.
  - Multi-context: `CONTEXT-MAP.md` at the repo root, pointing to per-context `CONTEXT.md` files.
- ADRs: ask whether durable architecture decisions should live in `docs/decisions/`.
- Agent instructions file: use canonical existing file, or ask whether to create `AGENTS.md` or `CLAUDE.md` when neither exists.

Default tracker recommendation follows the remote: GitHub for GitHub, GitLab for GitLab, local markdown otherwise. The user may still choose local markdown.

Always create or maintain `docs/agents/issue-tracker.md`, `docs/agents/local-artifacts.md`, and `docs/agents/documentation.md`. Issue operations use the selected tracker; local artifact operations always use local artifact conventions.

### 4. Prepare Changes

Load only templates needed for confirmed choices:

| Target | Template |
| --- | --- |
| `CLAUDE.md` or `AGENTS.md` | [agent-instructions.md](assets/templates/agent-instructions.md) |
| `docs/agents/issue-tracker.md` | [issue-tracker-github.md](assets/templates/issue-tracker-github.md), [issue-tracker-gitlab.md](assets/templates/issue-tracker-gitlab.md), or [issue-tracker-local.md](assets/templates/issue-tracker-local.md) |
| `docs/agents/local-artifacts.md` | [local-artifacts.md](assets/templates/local-artifacts.md) |
| `docs/agents/documentation.md` | [documentation.md](assets/templates/documentation.md) |

Use templates as scaffolds, not blind output.

- Replace placeholders with project-specific conventions.
- Update natural Markdown sections in place.
- Do not use managed-block markers.
- Do not duplicate `Issue Tracker`, `Local Artifacts`, or `Documentation` sections.
- Preserve unrelated user rules.
- Keep `CLAUDE.md`/`AGENTS.md` short and put details in `docs/agents/`.
- Do not create `CONTEXT.md` or `CONTEXT-MAP.md`, just create or maintain guidance for future skills to use.

Before writing, preview files to create/update and the intended change for each. Wait for explicit confirmation.

### 5. Write Safely

After confirmation, create or update only approved files.

## Validation

Before finishing, verify:

- The agent instructions file points to the three `docs/agents/` convention files without duplicating their details.
- Unrelated user instructions were preserved.
- The selected tracker matches `issue-tracker.md`.
- Local artifacts remain documented regardless of tracker.
- `CONTEXT.md` and `CONTEXT-MAP.md` were not created speculatively.
