# AI Workflow for Software Project Development

Lightweight, modular, human-centered AI coding workflow. It covers framing, slicing, implementation, review, and validation without trying to automate the entire software lifecycle. It is designed to become a set of focused agent skills backed by clear working memory.

> [!NOTE]
> This workflow is not designed for Vibe Coding. You must understand software development fundamentals and your project's architecture to use it effectively.

---

## Glossary

- **Skill / Agent skill:** reusable filesystem-based resource that gives AI agents focused instructions, workflows, domain knowledge, or project conventions. See [agentskills.io](https://agentskills.io/) for details.
- **Initiative:** unit of work tracked through the workflow, such as a feature, refactor, bug fix, MVP, sensitive release, or takeover.
- **Step:** workflow stage with a role, inputs, process, output, and human gate. Each step is intended to map to one or more future skills.
- **Output:** document, issue, comment, code change, summary, or durable doc update produced by a step.
- **Artifact:** temporary initiative-specific output such as brainstorming notes, brief, validation, PRD, Tech Design, task specs, QA, or prototypes.
- **Durable documentation:** long-term project memory, versioned in the repository when useful.
- **AFK / HITL:** `AFK` means a clear, testable, unblocked task; `HITL` means human judgment is required.
- **Human gate:** decision point where the human validates, arbitrates, or blocks the next step.
- **Feedback loop:** reliable signal that proves a change state: test, typecheck, lint, build, CI, bug reproduction, dev server, browser verification, or release check.

---

## Workflow Principles

- **Frame before coding:** formalize just enough based on scope, risk, and uncertainty.
- **Separate concerns:** `prd.md`, `tech-design.md`, and `tasks/*.md` answer different questions.
- **Build verifiable vertical slices:** every task should produce a useful end-to-end signal.
- **Keep humans on judgment:** product, UX, architecture, security, review, QA, and release decisions remain `HITL` when stakes are real.
- **Rely on feedback loops:** tests, typecheck, lint, build, CI, and reproduction define the achievable quality ceiling.
- **Capitalize only what lasts:** temporary artifacts must not become stale project truth.

---

## Overview

The workflow is intention-driven: use steps as needed, not mechanically. The nominal flow looks like this:

```text
Setup     : [workflow-setup]
Discovery : [brainstorm] -> [brief] -> [validate] -> [grill-me | grill-with-docs]
Product   : prd
Technical : [tech-design]
Execution : [slice] -> build/tdd -> [code-simplify] -> review -> qa -> capitalize
Release   : [ship-readiness]
```

Brackets indicate optional or contextual steps. Operational details live in `steps/`; this README explains how to choose a path, where outputs belong, and what each step must contain.

---

## Choose a Path

### Setup and Onboarding

- **First use in a repository:** `Workflow Setup -> [Project Baseline]`.
- **Existing project with weak docs:** `Workflow Setup -> Project Baseline -> [Zoom Out] -> PRD or Tech Design`.
- **Agent output keeps drifting:** `Workflow Setup -> [Project Baseline] -> resume current step`.

### Exploration and Framing

- **Idea exploration:** `Brainstorm -> Brief -> Validate -> [Grill Me]`.
- **Large project or MVP from scratch:** `[Brainstorm] -> Brief -> Validate -> [Grill Me] -> PRD -> Tech Design -> Slice -> per-task(Build -> Review -> [QA]) -> [Capitalize]`.
- **Uncertain UI:** `[Prototype UI] -> Brief or PRD -> Build -> [Review] -> [QA]`.

### Feature and Build

- **Large feature on an existing project:** `[Brief] -> [Validate if uncertain] -> [Grill Me or Grill With Docs] -> PRD -> [Tech Design] -> Slice -> per-task(Build -> Review) -> [QA] -> [Capitalize]`.
- **Medium multi-task feature:** `[Grill Me or Grill With Docs] -> PRD -> [Tech Design Lite] -> Slice -> per-task(Build -> Review) -> [QA] -> [Capitalize]`.
- **Small feature:** `Minimal PRD -> [Grill Me if ambiguous] -> Build -> [Review] -> [QA]`.
- **Simple fix or hotfix:** `Build -> [Review] -> [QA]`.
- **Works but became hard to read:** `Build -> Code Simplify -> Review`.

### Investigation, Refactor, and Takeover

- **Complex bug:** `Diagnose -> Build or TDD -> Review -> [QA]`.
- **Unknown code area:** `Zoom Out`.
- **Structural refactor:** `Zoom Out -> Improve Codebase Architecture -> [Grill With Docs] -> Tech Design -> Slice -> per-task(Build -> Review) -> [QA] -> Capitalize`.
- **Legacy or abandoned project:** `Workflow Setup -> Project Baseline -> [PRD] or [Tech Design]`.
- **Important release:** `... -> Review -> [QA] -> Ship Readiness`.

---

## Step List

Detailed definitions live in `steps/`.

### Core Workflow

- **[Brief](steps/001-brief.md)** - `brief` - optional. Converges a rough idea into product direction. Recommended default output: local `.initiatives/<initiative>/brief.md`.
- **[Validate](steps/002-validate.md)** - `validate` - optional. Tests major assumptions before investing further. Recommended default output: local `.initiatives/<initiative>/validation.md`.
- **[PRD](steps/003-prd.md)** - `prd` - required except for trivial changes. Defines expected product behavior. Recommended default output: parent tracker issue body, or local `.initiatives/<initiative>/prd.md`.
- **[Tech Design](steps/004-tech-design.md)** - `tech-design` - required when technical impact is non-trivial. Defines the technical approach and trade-offs. Recommended default output: parent issue section/comment, or local `.initiatives/<initiative>/tech-design.md`.
- **[Slice](steps/005-slice.md)** - `slice` - required for multi-task initiatives. Splits work into vertical, verifiable tasks. Recommended default output: sub-issues, or local `.initiatives/<initiative>/tasks/*.md`.
- **[Build](steps/006-build.md)** - `implement` or `implement-tdd` - required. Implements one task from a sufficient Execution Contract. Recommended default output: code changes and session verification summary.
- **[Review](steps/007-review.md)** - `review` - recommended. Performs a cold review focused on bugs, risks, and contract deviations. Recommended default output: session feedback or PR/tracker review comment.
- **[QA](steps/008-qa.md)** - `qa` - on demand. Produces a manual QA plan and may record observed results. Recommended default output: local `.initiatives/<initiative>/qa.md`.
- **[Capitalize](steps/009-capitalize.md)** - `capitalize` - when durable information changed. Updates durable docs, ADRs, follow-ups, or reports that no durable update is useful.

### On-Demand Steps

- **[Workflow Setup](steps/workflow-setup.md)** - `workflow-setup`. Establishes repo-level workflow configuration: output locations, tracker conventions, feedback commands, context-loading instructions, and agent boundaries.
- **[Brainstorm](steps/brainstorm.md)** - `brainstorm`. Opens the option space without converging too early. Recommended default output: local `.initiatives/<initiative>/brainstorming.md`.
- **[Grill Me](steps/grill-me.md)** - `grill-me`. Interviews the user one question at a time to resolve important decisions. Recommended default output: session decision log.
- **[Grill With Docs](steps/grill-with-docs.md)** - `grill-with-docs`. Aligns intent with domain language, docs, ADRs, and existing code. Recommended default output: session alignment summary.
- **[Prototype UI](steps/prototype-ui.md)** - `prototype-ui`. Explores disposable frontend directions before clean integration. Recommended default output: local prototype files and session summary.
- **[Diagnose](steps/diagnose.md)** - `diagnose`. Isolates a complex bug before fixing. Recommended default output: root-cause summary, fix, regression signal, and verification.
- **[Zoom Out](steps/zoom-out.md)** - `zoom-out`. Maps an unknown code area before modification. Recommended default output: session area map.
- **[Improve Codebase Architecture](steps/improve-codebase-architecture.md)** - `improve-codebase-architecture`. Identifies structural refactor opportunities. Recommended default output: ranked candidate list.
- **[Code Simplify](steps/code-simplify.md)** - `code-simplify`. Simplifies recently changed code while preserving behavior. Recommended default output: cleaner code and verification summary.
- **[Project Baseline](steps/project-baseline.md)** - `project-baseline`. Establishes durable understanding of an existing project: purpose, architecture, conventions, testing strategy, domain vocabulary, risks, and documentation gaps. Recommended default output: durable project docs updates.
- **[Ship Readiness](steps/ship-readiness.md)** - `ship-readiness`. Optional release gate before sensitive delivery. Recommended default output: `Go / No-Go` verdict.

---

## Step Anatomy

Steps in `steps/` are the specifications for future agent skills of the workflow.

Future skills should not use the same shape as the step specifications, but should use the smallest and simplest shape that works for each step.

Recommended sections for each step in `steps/` (not in future skills):

- **Step type:** core, optional, recommended, or on-demand.
- **Skill name:** future skill name.
- **Role:** what the step does in the workflow.
- **When to use:** when to use the step.
- **Possible inputs:** artifacts, files, issues, docs, commands, or user context worth loading.
- **Process:** numbered, chronological steps the agent must follow from context loading to production of the output.
- **Rules:** persistent guardrails, boundaries, non-goals, escalation rules, and instructions the agent must keep in mind while using the step.
- **Output:** what is produced: Markdown artifact, tracker issue/comment, code, docs update, or session summary.
- **Output location:** where to put it; check `.agents/workflow/output-locations.md` when it exists and state the recommended default.
- **Output template:** only for structured Markdown artifacts or comments; specify expected syntax such as paragraph, bullet list, checklist, metadata list, definition list, or single-line verdict.
- **Possible sizes:** concrete size levels such as minimal, standard, full, or task-specific variants.
- **Verification:** evidence that proves the step succeeded.
- **Human gate:** decision reserved for the user after the step is completed.

Every future skill of the workflow should pick the smallest useful size before writing. Prefer minimal/lite until scope, risk, or uncertainty justifies more.

### Definition of Ready

A task is ready for `Build` when it has a sufficient [Execution Contract](#execution-contract). `Definition of Ready` is the gate; `Execution Contract` is the content that satisfies the gate.

If the Execution Contract is incomplete, route back to `PRD`, `Tech Design`, `Slice`, `Grill Me`, or `Grill With Docs`.

### Definition of Done

A task is done when the change is implemented and useful feedback loops have spoken.

Minimum done state:

- implementation matches the `Execution Contract`
- relevant tests, typecheck, lint, build, browser checks, or other verification passed, or blockers are documented
- behavior changes, deviations, and remaining risks are reported
- unrelated work was not modified
- durable decisions or doc changes are routed to `Capitalize`

---

## Workflow Memory

### Durable Documentation

Durable documentation is the project's long-term memory. It is versioned in the repository when useful.

Examples:

- `docs/*`: project documentation, architecture, conventions, testing strategy, etc.
- `docs/decisions/*`: ADRs and durable decisions whose context is useful long term.
- `CONTEXT.md` (optional): durable domain vocabulary and shared terms.
- `CONTEXT-MAP.md` (optional): bounded context map if the project has several.
- `AGENTS.md`: root agent rules and pointers to workflow setup files.
- `README.md`: project entry point and reference guide.

Create durable docs only when there is real information to maintain.

### Initiative Outputs

Artifacts are temporary initiative-specific working materials generated during the workflow. Examples: brainstorming, brief, validation, PRD, Tech Design, task specs, QA, prototypes.

Before PRD, exploratory artifacts are local or session-first. Starting at PRD, the primary output location must be explicit: parent issue, equivalent tracker item, or local Markdown folder.

#### Output Locations

For `PRD`, `Tech Design`, `Slice`, and any publishable output, `.agents/workflow/output-locations.md` is the preferred source of truth when it exists. It should define where to read and publish parent initiatives, technical notes, task specs, comments, labels, statuses, and local Markdown paths.

If `.agents/workflow/output-locations.md` does not exist, use explicit user instruction or detected project convention for the current initiative. If no convention is discoverable, ask once before publishing PRD, Tech Design, or tasks.

Default locations by output type:

- `Brainstorm`: local `.initiatives/<initiative>/brainstorming.md`, updated during the session.
- `Brief`: local `.initiatives/<initiative>/brief.md`.
- `Validate`: local `.initiatives/<initiative>/validation.md`.
- `Grill Me` / `Grill With Docs`: session decision log; no file by default.
- `PRD`: `.agents/workflow/output-locations.md` location, parent issue body by default, or local `.initiatives/<initiative>/prd.md`.
- `Tech Design`: `.agents/workflow/output-locations.md` location, usually parent issue section/comment, or local `.initiatives/<initiative>/tech-design.md`.
- `Slice`: `.agents/workflow/output-locations.md` location, usually sub-issues, or local `.initiatives/<initiative>/tasks/*.md`.
- `Build`: code changes plus session verification summary.
- `Review`: session or PR/tracker review comment.
- `QA`: local `.initiatives/<initiative>/qa.md` by default.
- `Capitalize`: durable docs, ADRs, follow-ups, or no-op summary.

#### Primary Output Location

An initiative must have one active primary output location. Secondary locations may point to it, summarize it, or automate around it, but should not duplicate the primary content.

Practical recommendation:

- default: GitHub Issues or equivalent tracker
- collaborative or multi-agent work: GitHub Issues or equivalent tracker
- solo or local-first work: gitignored local Markdown in `.initiatives/<initiative>/`

If the location is external to the repo, the agent should access it through the official CLI or an MCP server.

#### GitHub Issues Mode

Create the parent issue at PRD time. Brainstorming, brief, and validation notes stay local or in chat until consolidated.

Parent issue body should contain the current execution truth:

- short context from brief or validation
- current PRD: problem, users, use cases, product behavior, requirements, out-of-scope, and open questions
- Tech Design summary when technical impact is non-trivial
- links to detailed Tech Design comments, sub-issues, durable docs, and ADRs
- status, blocking open questions, and accepted decisions

Recommended comments:

- dated decision log and trade-offs
- validation summary when it justifies `Go / Pivot / No-Go`
- detailed Tech Design when too long for the body
- QA plan or QA report when tracker publication helps coordination
- scope change or important clarification

Sub-issues:

- one sub-issue per vertical slice
- each sub-issue contains its own Execution Contract
- each sub-issue links to the parent issue
- parent scope changes trigger updates to future sub-issues

#### Local Markdown Mode

Local Markdown is acceptable when the primary output location is not a tracker. The recommended path is `.initiatives/<initiative>/`, gitignored by default.

Local artifacts are temporary. Decisions or information useful long term are consolidated into durable documentation.

Recommended structure:

```text
/
├─ README.md
├─ AGENTS.md
├─ CONTEXT.md                    (durable domain glossary, optional)
├─ CONTEXT-MAP.md                (if several bounded contexts, optional)
├─ .agents/                      (optional agent configuration)
│  └─ workflow/
│     ├─ output-locations.md
│     ├─ feedback-commands.md
│     ├─ context-loading.md
│     └─ agent-boundaries.md
├─ .initiatives/                 (gitignored by default)
│  ├─ 001-<initiative>/
│  │  ├─ brainstorming.md        (optional)
│  │  ├─ brief.md                (optional)
│  │  ├─ validation.md           (optional)
│  │  ├─ prd.md
│  │  ├─ tech-design.md          (optional)
│  │  ├─ qa.md                   (optional)
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

#### Initiative Index

An index is optional. If artifacts live in local Markdown, the recommended location is `.initiatives/index.md`. For a durable or collaborative view, prefer GitHub Projects, Linear, Jira, or `docs/product/initiatives.md`.

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

#### Artifact Lifecycle

When an initiative closes, associated artifacts should be deleted, archived, closed, or consolidated into durable documentation. Old artifacts should not become implicit source of truth for agents.

Evolution rules:

- if constraints, scope, or future tasks change without a major pivot, update the active initiative
- if the work becomes independent, opens a major pivot, or the previous initiative is historical, open a new initiative
- keep completed initiative history intact
- if shipped behavior must change, create a new task or initiative
- if implementation invalidates future tasks, update the PRD, Tech Design, and upcoming task specs immediately

#### Execution Contract

The Execution Contract is not a new document. It is the minimum content an agent must have available to implement a task. It can live in a prompt, PRD, task spec, issue, or any other medium.

Minimum content:

- scope
- behavior
- task-level acceptance criteria
- edge cases
- non-goals
- verification
- verification commands or feedback commands if known
- `blocked-by` dependencies when applicable
- `AFK | HITL` type when useful
- likely touchpoints, without a detailed implementation plan

#### Output Format

Each step should produce the smallest useful output for the current decision, execution, or validation.

Guidelines:

- choose the size level before writing
- include sections that change a decision, remove ambiguity, or support execution
- omit empty sections
- link source material instead of copying it
- finish with decisions made, blocking open questions, and the recommended next step when relevant

### Agent Configuration

On a multi-agent or issue-driven project, concise Markdown instructions can reduce ambiguity. Workflow setup usually lives in the repo under `.agents/workflow/`.

Recommended locations:

- `.agents/workflow/output-locations.md`: where to read and publish PRDs, Tech Designs, task specs, QA notes, comments, tracker links, and local initiative artifacts.
- `.agents/workflow/feedback-commands.md`: install, dev, test, typecheck, lint, build, browser, CI, migration, and known verification commands.
- `.agents/workflow/context-loading.md`: where durable docs live and when agents should load them. This file should point to durable docs, not duplicate their contents.
- `.agents/workflow/agent-boundaries.md`: stable agent operating boundaries such as always-do, ask-first, and never-do rules.
- `AGENTS.md`, `CLAUDE.md`, or equivalent root agent files: tiny pointer blocks to the workflow files above.

Loading rules:

- Load only the workflow setup file needed for the current action.
- Load `output-locations.md` before publishing workflow artifacts.
- Load `feedback-commands.md` before implementation, review, QA, diagnosis, or release checks.
- Load `context-loading.md` before choosing durable docs to read.
- Load `agent-boundaries.md` before persistent, risky, destructive, or externally visible changes.

Lifecycle rules:

- Rerun `Workflow Setup` when output locations, tracker conventions, feedback commands, context-loading pointers, or agent boundaries change.
- Rerun `Project Baseline` when architecture, conventions, testing strategy, domain vocabulary, or durable decisions become stale.
- If `Project Baseline` creates, moves, or renames durable docs, update `.agents/workflow/context-loading.md` pointers only.

If these docs do not exist, consuming skills continue silently. A real need for durable workflow configuration justifies creating them. Durable project knowledge belongs in project docs such as `README.md`, `docs/*`, `CONTEXT.md`, `CONTEXT-MAP.md`, or `docs/decisions/*`.

---

## Global Rules

### Feedback Loops

- Without reliable feedback, the agent codes blind.
- Document real project commands in `.agents/workflow/feedback-commands.md`, `README.md`, `AGENTS.md`, `docs/testing-strategy.md`, or equivalent.
- Minimal useful feedback: typecheck, automated tests, lint, formatting, build, and fast CI.
- Advanced feedback: accessible dev server, browser verification, targeted e2e tests, verifiable migrations, reproducible seeds.
- When test, build, CI, or runtime breaks, resolve or document the blocker before expanding scope.
- For a bug, the feedback loop is the main product of diagnosis.

### Context Engineering

- Load useful context, not the whole repository.
- Keep artifacts, files, and patterns relevant to the task.
- Use `Zoom Out` before modifying an unknown or hard-to-locate area.
- Prefer `/clear` over `/compact` between major steps or before review.
- Use PRDs, tasks, issues, docs, and tests as external memory instead of full chat history.
- Keep the system prompt and pushed instructions as short as possible.
- Create `CONTEXT.md`, `CONTEXT-MAP.md`, or ADRs only when a real term or decision has stabilized.

### Source-Driven Decisions

- Check official documentation when a decision depends on a framework or library.
- Report conflicts between official docs and repository patterns before deciding.
- Use durable vocabulary in issue titles, PRDs, tests, hypotheses, and plans.
- Use `Grill With Docs` when required terms are missing or contradict code usage.
- Report conflicts with durable decisions explicitly.

---

## Delivery

This workflow covers framing, slicing, implementation, review, and validation. Commit, PR, CI, release, and deployment remain team or project responsibilities, with `ship-readiness` as an optional gate before sensitive delivery.

## Credits

A huge thanks to [@mattpocock](https://github.com/mattpocock) for sharing his workflow and agent skills; it greatly inspired this one.
