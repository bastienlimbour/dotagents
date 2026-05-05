# Workflow Setup

**Skill name:** `workflow-setup`

**Step type:** On-demand step, usually run once per repository or when workflow behavior feels under-specified.

**Role:** Establish concise repo-level Markdown instructions that future workflow steps consume: output locations, tracker conventions, feedback commands, context-loading instructions, and agent boundaries.

**When to use:** New repository, first use of this workflow in a project, takeover, unclear output location, unclear tracker convention, missing feedback commands, missing agent entrypoint pointers, or repeated agent drift.

**Possible inputs:** Repository, `AGENTS.md`, `CLAUDE.md`, `.agents/workflow/*`, README, existing docs, package scripts, CI config, Makefiles, tracker conventions, issue tracker, local initiative artifacts, user preferences, and project workflow notes.

**Process:**

1. Explore the current repository before proposing files. Read whatever exists; do not assume repository, tracker, agent-file, `.agents/workflow/`, `.initiatives/`, command, or durable-doc conventions.
2. Present findings before writing: existing setup files, missing setup files, tracker clues, discovered commands, durable doc locations, root agent files, and ambiguity.
3. Ask unresolved setup decisions one at a time and recommend a default for each decision.
4. Draft the `.agents/workflow/*` files and root agent-file pointer blocks that will be created or updated.
5. Let the user review or edit the draft before writing persistent instructions.
6. Write approved changes, updating existing sections in place.
7. Summarize created or updated files and any setup gaps.

**Rules:**

- Setup documents how agents should operate in this repository.
- Setup maps durable docs but does not create project knowledge; use `Project Baseline` for durable architecture, conventions, testing strategy, domain, and decision docs.
- Exploration should check hosted repo clues, root agent files, existing `.agents/workflow/`, `.initiatives/`, README, scripts, CI, Makefiles, and durable docs.
- Ask unresolved setup decisions one at a time for primary output mode, tracker conventions, local Markdown convention, feedback commands, context-loading pointers, and agent boundaries.
- Draft `.agents/workflow/output-locations.md`, `.agents/workflow/feedback-commands.md`, `.agents/workflow/context-loading.md`, `.agents/workflow/agent-boundaries.md`, and root pointer blocks when useful.
- Do not append duplicate workflow blocks.
- If no root agent file exists, ask before creating one. Do not choose between `AGENTS.md`, `CLAUDE.md`, or another entrypoint without user confirmation.
- Record missing durable sources in `.agents/workflow/context-loading.md` and route durable documentation work to `Project Baseline`.
- Keep setup files operational and concise. Do not duplicate durable project knowledge from `README.md`, `docs/*`, `CONTEXT.md`, `CONTEXT-MAP.md`, or `docs/decisions/*`.
- When consuming existing setup, load only the `.agents/workflow/` file needed for the current action.

**Output:** Created or updated `.agents/workflow/*` Markdown instructions, root agent-file pointer blocks when useful, and a concise setup summary.

**Output location:** Recommended default: `.agents/workflow/`. Use an initiative artifact only when setup is part of a larger onboarding initiative.

**Output template:** Use strict headings and concise, flexible content. Omit sections that do not apply. Use `unknown` only when the source cannot be discovered and the user cannot decide yet.

`.agents/workflow/output-locations.md`:

```markdown
# Workflow Output Locations

## Primary Mode
- Mode: <GitHub Issues / tracker / local Markdown / session>
- Primary source of truth: <where current initiative truth lives>

## Initiative Outputs
- Brainstorm: `.initiatives/<initiative>/brainstorming.md`
- Brief: `.initiatives/<initiative>/brief.md`
- Validation: `.initiatives/<initiative>/validation.md`
- PRD: <parent issue body / tracker item / `.initiatives/<initiative>/prd.md`>
- Tech Design: <parent issue section/comment / tracker comment / `.initiatives/<initiative>/tech-design.md`>
- Tasks: <sub-issues / tracker children / `.initiatives/<initiative>/tasks/*.md`>
- QA: <`.initiatives/<initiative>/qa.md` / tracker comment / PR comment>
- Review: <PR review / tracker comment / session summary>

## Tracker
- Tool: <GitHub / Linear / Jira / GitLab / other / none>
- Access: <CLI / MCP / web / none>
- Parent-child convention: <how tasks link to initiatives>
- Comments: <where decisions, designs, QA, or status updates go>
- Role mapping: <optional labels/statuses for AFK-ready, HITL, blocked, done, won't fix>

## Local Markdown
- Root: `.initiatives/`
- Initiative naming: `001-kebab-case`
- Task naming: `001-kebab-case.md`
- Git tracking: <tracked / gitignored / project-specific>

## Publishing Rules
- Keep one active primary output location per initiative.
- Link or summarize secondary locations instead of duplicating primary truth.
- Ask before publishing PRD, Tech Design, or tasks when no convention is known.

## Update When
- Tracker, primary mode, artifact paths, labels/statuses, parent-child links, or publishing rules change.

## Gaps
- <missing tracker rule, unclear location, or setup follow-up>
```

`.agents/workflow/feedback-commands.md`:

```markdown
# Workflow Feedback Commands

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

`.agents/workflow/context-loading.md`:

```markdown
# Workflow Context Loading

## Start Here
- Load only the `.agents/workflow/` file needed for the current action.
- Read `.agents/workflow/output-locations.md` before publishing workflow artifacts.
- Read `.agents/workflow/feedback-commands.md` before implementation, review, QA, diagnosis, or release checks.
- Read `.agents/workflow/agent-boundaries.md` before making persistent, risky, destructive, or externally visible changes.
- Load durable docs only when relevant to the current task.

## Durable Sources
- Project overview: `README.md`
- Architecture: `docs/architecture.md`
- Conventions: `docs/conventions.md`
- Testing strategy: `docs/testing-strategy.md`
- Decisions: `docs/decisions/`
- Domain vocabulary: `CONTEXT.md`
- Context map: `CONTEXT-MAP.md`

## When To Load
- Architecture: before Tech Design, refactor, or unfamiliar implementation.
- Conventions: before Build and Review.
- Testing strategy: before Build, QA, Diagnose, or Ship Readiness.
- Decisions: before changing established architecture or behavior.
- Domain docs: before product, UX, naming, or domain-sensitive work.

## Update When
- Durable docs are created, moved, renamed, deprecated, split, or consolidated.

## Missing Sources
- <doc path or context source that does not exist yet>
```

`.agents/workflow/agent-boundaries.md`:

```markdown
# Workflow Agent Boundaries

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

Root agent-file pointer block:

```markdown
## AI Coding Workflow

Workflow instructions for agents live in `.agents/workflow/`.

Load only the workflow file needed for the current action.

- Output locations: `.agents/workflow/output-locations.md`
- Feedback commands: `.agents/workflow/feedback-commands.md`
- Context loading: `.agents/workflow/context-loading.md`
- Agent boundaries: `.agents/workflow/agent-boundaries.md`
```

**Possible sizes:** Quick setup for a small repository; standard setup for an active project; full setup for multi-agent, tracker-heavy, or poorly documented projects.

**Verification:** Future steps can locate output sources, feedback commands, context-loading rules, tracker conventions, and agent boundaries without asking again.

**Human gate:** Validate persistent setup decisions and draft files before they are written.
