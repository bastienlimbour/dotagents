# AI Workflow for Software Project Development

Lightweight, modular, human-centered AI coding workflow. It covers framing, slicing, implementation, review, and validation for a software project without trying to automate the entire lifecycle. It relies on specialized agent skills and flexible working memory.

> [!NOTE]
> This workflow is not designed for Vibe Coding. You must understand software development fundamentals and your projects' architecture to use it effectively.

---

## Glossary

- **Skill (or Agent skill):** reusable filesystem-based resource that provides AI agents with capabilities and expertise : instructions, workflows, domain-specific knowledge, best practices. See [agentskills.io](https://agentskills.io/) for details.
- **Initiative:** unit of work tracked in the workflow, e.g. add a feature, refactor a module, fix a bug, build an MVP, resume an abandoned project, plan a sensitive delivery, etc.
- **Step:** workflow stage with a role, inputs, outputs, and sometimes a human gate. Each step is linked to one or more skills.
- **Artifact:** temporary document, issue, or comment useful during an initiative, such as PRD, Tech Design, task specs, QA, or prototype.
- **AFK / HITL:** `AFK` (away from keyboard) means a clear, testable, unblocked task; `HITL` (human in the loop) means a task that requires human judgment.
- **Human gate:** decision point where the human validates, arbitrates, or blocks the next step.
- **Feedback loop:** reliable signal that proves the state of a change: test, typecheck, lint, build, CI, bug reproduction, dev server, or browser verification.

---

## Workflow Principles

- **Frame before coding:** formalize just enough based on scope and uncertainty.
- **Separate product, technical, and execution concerns:** `prd.md`, `tech-design.md`, and `tasks/*.md` have different roles.
- **Build verifiable vertical slices:** every task must produce a useful end-to-end signal.
- **Keep humans on judgment:** product, UX, architecture, sensitive security, review, QA, and final validation remain `HITL` when stakes are real.
- **Rely on reliable feedback loops:** tests, typecheck, lint, build, CI, or reproduction define the achievable quality ceiling.
- **Capitalize only what lasts:** temporary artifacts must not become a false source of truth.

---

## Overview

The workflow is intention-driven: use steps as needed, not mechanically. The nominal flow looks like this:

```text
Discovery : [brainstorm] -> [brief] -> [grill-me | grill-with-docs] -> [validate]
Product   : prd
Technical : [tech-design]
Execution : [slice] -> build/tdd -> review -> qa -> capitalize
```

Brackets indicate optional or contextual steps. Operational details for each step live in `steps/`; this README explains the workflow, how to choose a path, and where information belongs.

Core workflow steps progress from framing to execution. On-demand steps are contextual: open options, reduce ambiguity, understand a code area, diagnose a bug, prototype a UI, or verify a release.

---

## Choose a Path

### Exploration and Framing

- **Idea exploration:** `Brainstorm -> Brief -> [Grill Me] -> [Validate]`.
- **Large project or MVP from scratch:** `[Brainstorm] -> Brief -> [Grill Me] -> [Validate] -> PRD -> Tech Design -> Slice -> per-task(Build -> Review -> [QA]) -> [Capitalize]`.
- **Uncertain UI:** `[Prototype UI] -> Brief or PRD -> Clean Build -> [Review] -> [QA]`.

### Feature and Build

- **Large feature on an existing project:** `[Brief] -> [Grill Me or Grill With Docs] -> PRD -> [Tech Design] -> Slice -> per-task(Build -> Review -> [QA]) -> [Capitalize]`.
- **Medium multi-task feature:** `[Grill Me or Grill With Docs] -> PRD -> [Tech Design Lite] -> Slice -> per-task(Build -> Review) -> [QA] -> [Capitalize]`.
- **Small feature:** `Minimal PRD -> [Grill Me if ambiguous] -> Build -> [Review] -> [QA]`.
- **Simple fix or hotfix:** `Build -> [Review] -> [QA]`.

### Investigation, Refactor, and Takeover

- **Complex bug:** `Diagnose -> Build or TDD -> Review -> [QA]`.
- **Unknown code area:** `Zoom Out`.
- **Structural refactor:** `Zoom Out -> Improve Codebase Architecture -> [Grill With Docs] -> Tech Design -> Slice -> per-task(Build -> Review) -> [QA] -> Capitalize`.
- **Legacy or abandoned project:** `Project Baseline -> [PRD] or [Tech Design]`.
- **Important release:** `... -> Review -> [QA] -> Ship Readiness`.

---

## Step List

Detailed definitions live in `steps/`. Summary of steps and roles:

### Core Workflow

- **[Brief](steps/001-brief.md)** - `brief` - optional. Turns an idea into a clear product direction. Artifact: `brief.md` or tracker equivalent.
- **[Validate](steps/002-validate.md)** - `validate` - optional. Reduces external uncertainty before further investment. Artifact: `validation.md` or tracker equivalent.
- **[PRD](steps/003-prd.md)** - `prd` - required except for trivial changes. Defines expected product behavior. Artifact: `prd.md` or tracker equivalent.
- **[Tech Design](steps/004-tech-design.md)** - `tech-design` - required when technical impact is non-trivial. Formalizes architecture, interfaces, and trade-offs. Artifact: `tech-design.md` and ADRs when needed.
- **[Slice](steps/005-slice.md)** - `slice` - required for multi-task initiatives. Splits work into vertical, verifiable tasks ordered by dependencies. Artifact: `tasks/*.md` or tracker equivalent.
- **[Build](steps/006-build.md)** - `implement` or `implement-tdd` - required. Implements a task from a sufficient Execution Contract. Artifact: code + session report.
- **[Review](steps/007-review.md)** - `review` - recommended. Cold code review focused on bugs, risks, and contract deviations. Artifact: session feedback or review comment.
- **[QA](steps/008-qa.md)** - `qa` - on demand. Produces a manual test plan and may record observed results. Artifact: optional checklist or `qa.md`.
- **[Capitalize](steps/009-capitalize.md)** - `capitalize` - when there is a durable decision or maintained documentation. Updates durable docs and cleans temporary artifacts. Artifact: docs, ADRs, follow-ups, or non-capitalization note.

### On-Demand Steps

- **[Brainstorm](steps/brainstorm.md)** - `brainstorm`. Opens the option space without converging too early. Artifact: optional `brainstorming.md`.
- **[Grill Me](steps/grill-me.md)** - `grill-me`. Decision interview, one question at a time. Artifact: short decision log or integration into the next step.
- **[Grill With Docs](steps/grill-with-docs.md)** - `grill-with-docs`. Aligns intent with domain language, docs, ADRs, and existing code. Artifact: clarified decisions, durable vocabulary, or ADRs when needed.
- **[Prototype UI](steps/prototype-ui.md)** - `prototype-ui`. Explores disposable frontend directions before clean integration. Artifact: isolated prototypes + summary.
- **[Diagnose](steps/diagnose.md)** - `diagnose`. Isolates the root cause of a complex bug before fixing. Artifact: root cause, fix, regression test, and verification.
- **[Zoom Out](steps/zoom-out.md)** - `zoom-out`. Maps an unknown code area before modification. Artifact: concise map of modules, callers, seams, and risks.
- **[Improve Codebase Architecture](steps/improve-codebase-architecture.md)** - `improve-codebase-architecture`. Identifies deepening and structural refactor opportunities. Artifact: prioritized refactor candidates.
- **[Project Baseline](steps/project-baseline.md)** - `project-baseline`. Establishes the baseline of an existing project. Artifact: updated project docs.
- **[Ship Readiness](steps/ship-readiness.md)** - `ship-readiness`. Optional gate before a sensitive release. Artifact: checklist or `Go / No-Go` verdict.

---

## Workflow Memory

### Durable Documentation

Durable documentation is the project's long-term memory. It is versioned in the repository.

Examples:

- `docs/*`: project documentation, architecture, conventions, testing strategy, etc.
- `docs/decisions/*`: durable decisions (ADRs) whose context is useful long term.
- `CONTEXT.md` (optional): durable domain vocabulary and shared terms.
- `CONTEXT-MAP.md` (optional): bounded context map if the project has several.
- `AGENTS.md` (optional): rules and instructions for AI agents.
- `README.md` (optional): project entry point and reference guide (purpose, installation, usage for users, contributors, and AI agents).

Do not create a durable file before there is real information to store in it.

### Artifacts

Artifacts are temporary initiative-specific working materials generated by the AI agent during the workflow.

Examples: brainstorming, brief, validation, PRD, Tech Design, task specs, QA, prototypes.

The default strategy is **GitHub Issues + sub-issues**, or an equivalent tracker that can represent a parent initiative, child tasks, and links. Local Markdown remains fully acceptable, especially solo or local-first, if the lifecycle is respected.

Before PRD, highly exploratory artifacts such as brainstorming, brief, or validation notes can stay local or in chat. Starting at PRD, the primary artifact location must be explicit: parent issue, equivalent tracker item, or local Markdown folder.

#### Primary Artifact Support

An initiative must have one active primary artifact location. Secondary locations may point, comment, or automate, but must not duplicate the primary content.

Practical recommendation:

- default: GitHub Issues or equivalent tracker
- collaborative or multi-agent work: GitHub Issues or equivalent tracker
- solo or local-first work: gitignored local Markdown in `.initiatives/<initiative>/`

If the location is external to the repo, the agent must access it through the official CLI or an MCP server.

#### GitHub Issues Mode

Create the parent issue at PRD time. Brainstorming, brief, and validation notes stay local or in chat until consolidated. Only elements useful for execution or decision-making are integrated into the parent issue.

Parent issue:

- active source of truth for the initiative
- created when the PRD is ready to become the working location
- canonical body kept up to date
- links to sub-issues, important comments, durable docs, and ADRs

Recommended canonical body:

- short context from the brief or validation, without raw transcript
- current PRD: scope, behavior, edge cases, acceptance criteria, non-goals
- Tech Design summary if technical impact is non-trivial
- links to detailed Tech Design comment when needed
- links to vertical slice sub-issues
- status, blocking open questions, and accepted decisions

Recommended comments:

- dated decision log and trade-offs
- validation summary if it justifies `Go / No-Go / Pivot`
- detailed Tech Design when too long for the body
- QA plan or QA report
- scope change or important clarification

Consolidation rule: a comment may preserve history, but must not become a competing source of truth. If a decision in a comment changes current truth, consolidate it into the body, a sub-issue, durable docs, or an ADR.

Sub-issues:

- one sub-issue per vertical slice
- each sub-issue contains its own Execution Contract
- each sub-issue links to the parent issue
- do not copy the full PRD or full Tech Design into each sub-issue
- close or update sub-issues when parent scope changes

Recommended mapping:

- brainstorming: local/chat, never copied raw
- brief: local/chat, useful summary integrated into the PRD
- validation: local/chat or comment if it justifies a decision
- PRD: parent issue body
- Tech Design lite: short section in the body
- non-trivial Tech Design: summary in the body + detailed comment linked from the body
- tasks: sub-issues, one per vertical slice
- QA: comment on the parent issue or relevant sub-issue
- capitalization: durable docs, ADRs, local cleanup, and initiative closure

#### Local Markdown Mode

Local Markdown is acceptable when the primary artifact location is not a tracker. The recommended path is `.initiatives/<initiative>/`, gitignored by default.

Local artifacts are not versioned by default. Decisions or information useful long term are consolidated into durable documentation.

#### Artifact Lifecycle

When an initiative closes, associated artifacts must be deleted, archived, closed, or consolidated into durable documentation. An old PRD must not become an implicit source of truth for an agent.

Evolution rules:

- if constraints, scope, or tasks change without a major pivot: update the active initiative
- if the work becomes independent, there is a major pivot, or the previous initiative is historical: open a new initiative
- do not rewrite the history of a completed initiative
- do not retroactively edit an already implemented task spec to hide an error
- if shipped behavior must change, create a new task or initiative
- if an implementation invalidates future tasks, immediately update the PRD, Tech Design, and upcoming task specs

#### Recommended Markdown Structure

If the primary artifact location is local Markdown, this structure separates durable documentation from temporary artifacts grouped by initiative. The `.initiatives/` directory is gitignored by default.

```text
/
├─ README.md
├─ AGENTS.md
├─ CONTEXT.md                    (durable domain glossary, optional)
├─ CONTEXT-MAP.md                (if several bounded contexts, optional)
├─ .agents/                      (optional agent configuration)
│  ├─ issue-tracker.md
│  └─ domain.md
├─ .initiatives/                 (gitignored by default)
│  ├─ 001-<initiative>/
│  │  ├─ brainstorming.md     (optional)
│  │  ├─ brief.md             (optional)
│  │  ├─ validation.md        (optional)
│  │  ├─ prd.md
│  │  ├─ tech-design.md       (optional)
│  │  ├─ qa.md                (optional)
│  │  └─ tasks/
│  │     ├─ 001-<task>.md
│  │     └─ ...
│  └─ 002-<initiative>/
│     └─ prd.md
├─ docs/
│  ├─ architecture.md
│  ├─ conventions.md
│  ├─ testing-strategy.md
│  └─ decisions/
│     └─ 001-*.md                (ADRs / durable decisions)
└─ apps/, packages/, scripts/, ...
```

Naming rules:

- one folder per initiative, in kebab-case, prefixed with `001-`, `002-`, etc.
- `tasks/` exists only if the initiative has multiple tasks
- one file per task, in kebab-case, prefixed with `001-`, `002-`, etc.

#### Initiative Index (Optional)

An index is useful but optional. If artifacts live in local Markdown, the recommended location is `.initiatives/index.md`. For a durable or collaborative view, prefer GitHub Projects, Linear, Jira, or `docs/product/initiatives.md`. On a small project, the index may not exist.

Its role:

- list initiatives
- indicate their status
- point to PRDs, tasks, or tickets

Minimal example:

```text
In progress
- 003-team-collaboration - PRD validated, 2/5 tasks done

Upcoming
- 004-gamification - brainstorming only

Completed
- 001-mvp
- 002-dark-mode
```

#### Execution Contract

The Execution Contract is not a new document: it is the minimum content an agent must have available to implement a task. It can live in a prompt, PRD, task spec, issue, or any other medium.

The `Build` step must start only when a sufficient `Execution Contract` is available.

Minimum content:

- scope
- behavior
- acceptance criteria
- edge cases
- non-goals
- verification
- verification commands or feedback commands if known
- `blocked-by` dependencies when applicable
- `AFK | HITL` type if the task is intended for an agent
- likely touchpoints, without a detailed implementation plan

#### Output Format

The output content lists for each step or skill are not exhaustive checklists. Each skill must produce the smallest useful artifact for the decision, execution, or validation.

Rules:

- choose the `lite / standard / full` level before writing
- include only sections that change a decision, remove ambiguity, or directly support execution
- distinguish required content, conditional content, and content to avoid when output can grow
- omit sections without real signal
- avoid raw transcripts, long logs, exhaustive file inventory, copy-paste from the previous step, etc.
- finish with decisions made and blocking open questions

### Agent Configuration (Optional)

On a multi-agent or issue-driven project, configuration can help avoid ambiguity. It is versioned and usually lives in the repo under `.agents/`.

Recommended locations:

- `.agents/issue-tracker.md`: where to read and publish PRDs, task specs, etc.
- `.agents/domain.md`: how to read durable documentation, `CONTEXT.md`, `CONTEXT-MAP.md`, `docs/decisions/`, etc.
- `AGENTS.md` or `CLAUDE.md`: points to the configuration files above

If these docs do not exist, consuming skills or agents continue silently. They must not propose creating them upfront. Only a real need for durable configuration justifies creating them.

---

## Global Rules

### Feedback Loops and Stop-the-Line

- Without reliable feedback, the agent codes blind.
- Document real project commands in `README.md`, `AGENTS.md`, `docs/testing-strategy.md`, or equivalent.
- Minimal useful feedback: typecheck, automated tests, lint, formatting, build, and fast CI.
- Advanced feedback: accessible dev server, browser verification, targeted e2e tests, verifiable migrations, reproducible seeds.
- If test, build, CI, or runtime breaks, handle the issue or document the blocker before expanding scope.
- For a bug, the feedback loop is the main product of diagnosis: without a reliable pass/fail signal, do not expand hypotheses.

### Context Engineering

- Load useful context, not the whole repository.
- Keep artifacts, files, and patterns relevant to the task.
- Use `Zoom Out` before modifying an unknown or hard-to-locate area.
- Prefer `/clear` over `/compact` between major steps or before review.
- Use PRDs, tasks, issues, docs, and tests as external memory instead of the full chat history.
- Keep the system prompt and pushed instructions as short as possible.
- If `CONTEXT.md`, `CONTEXT-MAP.md`, or `docs/decisions/` do not exist, continue silently and create them only when a real decision or term is stabilized.

### Source-Driven Decisions

- Check official documentation when a decision depends on a framework or library.
- Report any conflict between official docs and repository patterns before deciding.
- Use `CONTEXT.md` vocabulary in issue titles, PRDs, tests, hypotheses, and plans.
- If a required term is missing or contradicts code usage, it is a signal for `Grill With Docs`.
- Explicitly report any conflict with a durable decision instead of silently overriding it.

---

## Delivery

This workflow covers framing, slicing, implementation, review, and validation. Commit, PR, CI, release, and deployment remain team or project responsibilities, with `ship-readiness` as an optional gate before sensitive delivery.

## Credits

A huge thanks to [@mattpocock](https://github.com/mattpocock) for sharing his workflow and agent skills; it greatly inspired this one.
