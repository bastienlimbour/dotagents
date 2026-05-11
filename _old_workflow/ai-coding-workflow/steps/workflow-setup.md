# Workflow Setup

**Skill name:** `workflow-setup`

**Step type:** On-demand (usually run once per repository or when agents/skills behavior feels under-specified).

**Role:** Establish concise repo-level agent rules for workflow outputs, issue-tracker publication, local Markdown artifacts, feedback commands, context sources, agent boundaries, and `AGENTS.md` trigger pointers.

**When to use:** New repository, first use of this workflow in a project, takeover, unclear artifact or tracker publication behavior, missing feedback commands, missing `AGENTS.md` pointers, unclear context sources, unclear agent boundaries, or repeated agent drift.

**Possible inputs:** Repository, `AGENTS.md`, `.agents/rules/*`, README, existing docs, package scripts, CI config, Makefiles, issue tracker conventions, local initiative artifacts, user preferences, and project workflow notes.

**Process:**

1. Explore the current repository before proposing files. Read whatever exists; do not assume `AGENTS.md`, `.agents/rules/`, `.initiatives/`, command, tracker, or durable-doc conventions.
2. Present findings before writing: existing `AGENTS.md`, existing rule files, tracker clues, discovered commands, durable doc locations, local initiative conventions, `.gitignore` state, and ambiguity.
3. Ask all unresolved setup decisions one at a time and recommend a default for each decision. Default issue tracker setup is GitHub Issues through `gh`; ask if the user wants another tracker setup.
4. Draft all four rule files: `.agents/rules/output-locations.md`, `.agents/rules/feedback-commands.md`, `.agents/rules/context-sources.md`, and `.agents/rules/agent-boundaries.md`.
5. Draft the `AGENTS.md` pointer block with trigger-based guidance for when agents should read each rule file.
6. Let the user review or edit the draft before writing persistent instructions.
7. Ask for explicit confirmation before every file creation or update, including rule files, `AGENTS.md`, and `.gitignore`.
8. Write only approved changes, updating existing sections in place.
9. Summarize created or updated files and any setup gaps.

**Rules:**

- Setup documents how agents should operate in this repository.
- Setup creates or updates all four rule files by default, unless the user declines a specific file.
- `AGENTS.md` is the canonical agent entrypoint. If no `AGENTS.md` exists, ask before creating one.
- `.agents/rules/output-locations.md` explains how to create local Markdown artifacts and how to publish to an issue tracker; it does not maintain per-step output mappings.
- Use GitHub Issues through `gh` as the default tracker template, but adapt to another official tracker CLI or MCP when the user chooses one.
- Use `.initiatives/001-<initiative>/` for local initiative folders and `.initiatives/001-<initiative>/tasks/001-<task>.md` for local task specs.
- Ask before adding `.initiatives/` to `.gitignore` when local artifacts should stay untracked.
- Do not append duplicate `AGENTS.md` pointer blocks; update existing workflow blocks in place.
- Every persistent write or update requires explicit confirmation. If the user does not confirm, do not write or publish.
- Setup maps operational rules but does not create project knowledge; durable architecture, conventions, testing strategy, domain, and decision docs belong to dedicated baseline work.
- Keep setup files operational and concise. Do not duplicate durable project knowledge from `README.md`, `docs/*`, `CONTEXT.md`, `CONTEXT-MAP.md`, or `docs/decisions/*`.

**Output:** Created or updated `.agents/rules/*` Markdown instructions, `AGENTS.md` trigger-based pointer block, optional `.gitignore` update for `.initiatives/`, and a concise setup summary.

**Output location:** Recommended default: `.agents/rules/` plus `AGENTS.md`. Ask before every write or update. Use an initiative artifact only when setup is part of a larger onboarding initiative and the user confirms that artifact write.

**Output template:** Use strict headings and concise, flexible content. Omit sections that do not apply. Use `unknown` only when the source cannot be discovered and the user cannot decide yet.

`.agents/rules/output-locations.md`:

```markdown
# Output Locations

These rules explain how to create local initiative Markdown artifacts and how to publish workflow outputs to an issue tracker after a skill has drafted the content and asked for confirmation.

## Local Markdown Artifacts
- When a skill says to create a local Markdown file, draft the content in session first and ask before every create or update.
- If the user does not confirm, do not write the file; keep the content in the session only.
- Use `.initiatives/001-<initiative>/` for initiative artifacts.
- Use `.initiatives/001-<initiative>/brainstorming.md`, `brief.md`, `validation.md`, `technical-design.md`, `spec.md`, or `qa.md` for standard artifacts.
- Use `.initiatives/001-<initiative>/tasks/001-<task>.md` for local task specs.
- Use kebab-case slugs and increment numeric prefixes for initiatives and task files.
- Use `.initiatives/index.md` only when a local initiative index is useful; prefer tracker views or durable docs for collaborative indexes.
- Ask before adding `.initiatives/` to `.gitignore` if local artifacts should stay untracked and it is not already ignored.
- Treat local artifacts as temporary working material. Consolidate durable decisions into durable docs when they should outlive the initiative.

## Issue Tracker Publication
- Default to GitHub Issues through `gh` unless the repository uses another official tracker CLI or MCP.
- When a skill says to publish to the issue tracker, draft the content in session first and ask before every issue creation, issue edit, issue comment, PR comment, or equivalent tracker update.
- If the user does not confirm, do not publish or update the tracker; keep the content in the session only.
- Create an issue with `gh issue create --title "<title>" --body "<body>"`.
- Update an issue body with `gh issue edit <number> --body "<body>"`.
- Comment on an issue with `gh issue comment <number> --body "<body>"`.
- Inspect an issue with `gh issue view <number> --comments`.
- When a skill says to create or update an issue body, keep the body focused on that artifact's canonical content.
- When a skill says to publish a tracker comment, prefer a single concise comment that can be linked from later comments or issues.
- When a skill says to create task issues, create normal issues that reference the parent issue; when it says to add a parent issue comment, link the created task issues there.
- Do not edit an issue body just to add secondary links unless the user explicitly confirms that issue-body update.
- Link or summarize secondary locations instead of duplicating primary tracker truth.
```

`.agents/rules/feedback-commands.md`:

```markdown
# Feedback Commands

## Commands
- Install: `<command or unknown>`
- Dev: `<command or unknown>`
- Test: `<command or unknown>`
- Typecheck: `<command or unknown>`
- Lint: `<command or unknown>`
- Format: `<command or unknown>`
- Build: `<command or unknown>`
- Browser / E2E: `<command or unknown>`
- CI: `<command or unknown>`
- Migrations / seeds: `<command or unknown>`

## Command Selection
- Prefer targeted commands for the touched area when available.
- Run broader checks before completion when risk or project convention requires it.
- Report blockers instead of inventing commands.

## Update When
- Install, dev, test, typecheck, lint, format, build, browser, CI, migration, seed, or verification commands change.

## Gaps
- <missing command, unreliable feedback loop, or verification limitation>
```

`.agents/rules/context-sources.md`:

```markdown
# Context Sources

## Durable Sources
- Project overview: `README.md`
- Architecture: `docs/architecture.md`
- Conventions: `docs/conventions.md`
- Testing strategy: `docs/testing-strategy.md`
- Decisions: `docs/decisions/`
- Domain vocabulary: `CONTEXT.md`
- Context map: `CONTEXT-MAP.md`

## When To Read
- Architecture: before Technical Design, Spec, refactor, or unfamiliar implementation.
- Conventions: before Build and Review.
- Testing strategy: before Build, QA, Diagnose, or Ship Readiness.
- Decisions: before changing established architecture or behavior.
- Domain docs: before product, UX, naming, or domain-sensitive work.

## Update When
- Durable docs are created, moved, renamed, deprecated, split, or consolidated.

## Missing Sources
- <doc path or context source that does not exist yet>
```

`.agents/rules/agent-boundaries.md`:

```markdown
# Agent Boundaries

## Always Do
- <stable agent behavior>

## Ask First
- <decision requiring human approval>

## Never Do
- <hard project constraint>

## Project Constraints
- <project-specific operational rule>

## Update When
- Stable always-do, ask-first, never-do, risky-operation, security, deployment, or repository constraints change.

## Gaps
- <boundary that needs user confirmation>
```

`AGENTS.md` pointer block:

```markdown
## AI Coding Workflow

Repo-specific workflow rules for agents live in `.agents/rules/`.

Read only the rule file needed for the current action:

- Local Markdown artifacts or issue-tracker publication: `.agents/rules/output-locations.md`
- Tests, typecheck, lint, build, dev server, browser, CI, migration, seed, or release checks: `.agents/rules/feedback-commands.md`
- Durable docs, project vocabulary, architecture, conventions, testing strategy, or ADR context: `.agents/rules/context-sources.md`
- Persistent, risky, destructive, externally visible, security-sensitive, deployment, or repository-boundary decisions: `.agents/rules/agent-boundaries.md`
```

**Possible sizes:** lite (small repository); standard (active project); full (multi-agent, tracker-heavy, or poorly documented projects).

**Verification:** Future agents can find output guidance, feedback commands, context sources, tracker conventions, and agent boundaries through `AGENTS.md` trigger pointers without step-specific rule-loading instructions.

**Human gate:** Validate persistent setup decisions and draft files before they are written.
