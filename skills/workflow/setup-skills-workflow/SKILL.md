---
name: setup-skills-workflow
description: Sets up, audits, or realigns a project's agent conventions for efficiently using the skills-based AI coding workflow. Use when the user asks "setup agent workflow", "install the skills workflow", "setup the AI coding workflow", or any other variant of these phrases.
---

# Setup Skills Workflow

Configure project-specific conventions for efficiently using the skills-based AI coding workflow.

This is a prompt-driven skill, not a deterministic script. Explore, present what you found, confirm with the user, then write.

## When To Use

- A repo needs first-time setup for the skills-based AI coding workflow.
- Existing agent rules need an audit, cleanup, or realignment with the workflow.
- The user asks to setup agent workflow, configure workflow conventions, install workflow docs, or define conventions for issues, local artifacts, documentation, domain context, or ADRs.

Do not use this skill to create feature specs, split tasks, implement code, run triage automation, or create initiative artifacts such as `product-brief.md`, `brainstorming.md`, or `validation.md` unless the user separately asks for those artifacts.

## Workflow

### 1. Explore

Inspect the repo and the files before recommending changes:

- Is the repo hosted on GitHub, GitLab, or somewhere else? (check `git remote -v` and `.git/config`).
- Is `gh` or `glab` available and authenticated when the matching remote is detected?
- Does `CLAUDE.md` or `AGENTS.md` exist at the repo root? Is there already a `## Workflow Conventions` section in one of these AGENTS files?
- Does this skill's prior output `docs/agents/` exists ? And what is its content?
- Does `CONTEXT.md` or `CONTEXT-MAP.md` exist at the repo root?
- Does `docs/decisions/` or `**/docs/decisions/` exist in the codebase?
- Does `.initiatives/` exist at repo root?
- Do project or workflow conventions already exist in docs or agent instruction files?

Do not treat absent files as errors. If both `CLAUDE.md` and `AGENTS.md` exist, ask which AGENTS file is canonical before proposing adding a `## Workflow Conventions` section.

### 2. Report Findings

Briefly summarize:

- Agent instruction files already present.
- Issue tracker and CLI status detected.
- Local artifact conventions detected.
- Global documentation and ADR conventions detected.
- Useful missing pieces or drift, framed as optional setup work.

If a CLI is missing or unauthenticated, report it and recommend the next concrete setup action. Do not silently switch tracker conventions. Local markdown is a real issue tracker option.

### 3. Decide One Convention At A Time

For each material choice, give a short explanation, recommend one option, ask one question, and wait for the answer.

Cover only decisions that are not already clear from the repo or still need confirmation:

- Issue tracker: GitHub Issues via `gh`, GitLab Issues via `glab`, or local markdown under `.initiatives/`.
- Local artifacts: always configure guidance for local artifacts; decide only whether to create `.initiatives/` now.
- Domain context: whether to create `CONTEXT.md` when useful domain vocabulary is known and the file is absent.
- Context map: whether to create `CONTEXT-MAP.md` for repos with multiple packages, domains, apps, or bounded contexts.
- ADRs: whether durable architecture decisions should live in `docs/decisions/`.
- AGENTS file: use existing canonical AGENTS file, or ask whether to create `CLAUDE.md` or `AGENTS.md` when neither exists.

Default tracker recommendation follows the detected remote: GitHub for GitHub remotes, GitLab for GitLab remotes, local markdown otherwise. The user may still choose local markdown as the tracker even when a remote tracker exists.

Always produce or maintain both `docs/agents/issue-tracker.md` and `docs/agents/local-artifacts.md`. Issue operations use the selected issue tracker convention. Local artifact operations use `docs/agents/local-artifacts.md` regardless of the issue tracker choice.

### 4. Prepare Changes

Load only the templates needed for the confirmed choices:

| Target file | Template |
| --- | --- |
| `CLAUDE.md` or `AGENTS.md` | [conventions.md](assets/templates/conventions.md) |
| `docs/agents/issue-tracker.md` | [issue-tracker-github.md](assets/templates/issue-tracker-github.md) for GitHub |
| `docs/agents/issue-tracker.md` | [issue-tracker-gitlab.md](assets/templates/issue-tracker-gitlab.md) for GitLab |
| `docs/agents/issue-tracker.md` | [issue-tracker-local.md](assets/templates/issue-tracker-local.md) for local markdown |
| `docs/agents/local-artifacts.md` | [local-artifacts.md](assets/templates/local-artifacts.md) |
| `docs/agents/documentation.md` | [documentation.md](assets/templates/documentation.md) |
| `CONTEXT.md` | [context.md](assets/templates/context.md) |
| `CONTEXT-MAP.md` | [context-map.md](assets/templates/context-map.md) |

Use templates as scaffolds, not blind output. Replace placeholder guidance with project-specific conventions. Keep exact commands and stable rules when they are correct for the project.

Update natural Markdown sections in place. Do not use managed-block markers. Do not duplicate existing `Issue Tracker`, `Local Artifacts`, or `Documentation` sections. Preserve unrelated user rules and surrounding content.

Keep AGENTS.md or CLAUDE.md files short. Put detailed conventions in `docs/agents/`.

Before writing, preview the files to create or update and the intended change for each file. Wait for explicit confirmation.

### 5. Write Safely

After confirmation, create or update only the approved files.

## Output

During the run, provide:

- A concise findings summary after exploration.
- One decision question at a time, each with a recommended answer.
- A pre-write preview of files that will be created or changed.
- A final summary of files changed, conventions chosen, skipped optional items, and any remaining setup actions such as authenticating `gh` or `glab`.

## Validation

Before finishing, verify:

- [ ] The chosen AGENTS file points to `docs/agents/issue-tracker.md`, `docs/agents/local-artifacts.md`, and `docs/agents/documentation.md`.
- [ ] AGENTS file details are not duplicated from `docs/agents/`.
- [ ] Existing unrelated user instructions were preserved.
- [ ] The selected tracker matches `docs/agents/issue-tracker.md`.
- [ ] Local markdown issue tracking clearly points to `docs/agents/local-artifacts.md` for shared path and naming conventions while remaining the selected issue tracker convention.
- [ ] `docs/agents/local-artifacts.md` exists or remains maintained even when GitHub or GitLab is the issue tracker.
- [ ] `CONTEXT.md` was not created empty, speculatively, or as project status documentation.
- [ ] `CONTEXT-MAP.md` was created only for a multi-context repo or a confirmed need.
- [ ] No v1 out-of-scope artifacts were created.
- [ ] The final response reports validation performed and any remaining assumptions.
