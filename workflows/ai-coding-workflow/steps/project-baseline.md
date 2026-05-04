# Project Baseline

**Skill:** `project-baseline`

**Status:** On-demand step.

**Role:** Establish a reliable baseline for an existing project: product docs, project docs, architecture, conventions, testing strategy, risk areas.

**When to use:** Legacy onboarding, abandoned project, poorly documented codebase, takeover of an existing project.

**Possible inputs:** existing repository, existing docs, README, scripts, tests, architecture, tickets, user context.

**Actions:**

- bound the baseline scope before exploration
- explore the repository and existing documentation
- identify actual architecture, conventions, and testing strategy
- detect risk areas and inconsistencies
- update useful durable documentation instead of creating a mega-document

**Output:** direct updates to project documentation.

**Artifact publication:** `Project Baseline` updates durable documentation instead of creating a temporary artifact. Explicitly propose the durable files to edit before editing. If an onboarding issue or tracker item exists, propose a summary comment with updated docs and follow-ups.

**Output contents:**

Required content:

- documentation files updated
- current architecture
- observed conventions
- actual testing strategy
- risk areas
- inconsistencies

Conditional content:

- inspected sources
- unknown or uncovered areas
- proposed follow-ups

Avoid:

- isolated artifact such as `current-state.md` without durable use
- exhaustive file tree
- creating durable docs without real information to maintain

**Possible sizes:** quick baseline for onboarding, full baseline for a legacy repository.

**Human gate:** validate what becomes project source of truth.

**Important:** This does not necessarily produce an isolated artifact such as `current-state.md`. It updates the project's durable documentation.
