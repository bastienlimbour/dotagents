# AI Workflow for Software Project Development

Modular, human-centered AI coding workflow. It covers framing, slicing, implementation, review, and validation without trying to automate the entire software lifecycle. It is designed to become a set of focused agent skills backed by clear working memory.

> [!NOTE]
> This workflow is not designed for Vibe Coding. You must understand software development fundamentals and your project's architecture to use it effectively.

---

## Glossary

- **Skill / Agent skill:** reusable filesystem-based resource that gives AI agents focused instructions, workflows, domain knowledge, or project conventions. See [agentskills.io](https://agentskills.io/) for details.
- **Initiative:** unit of work tracked through the workflow, such as a feature, refactor, bug fix, MVP, sensitive release, or takeover.
- **Step:** workflow stage with a role, inputs, process, output, and human gate. Each step is self-contained and intended to map to one or more future skills.
- **Output:** document, issue, comment, code change, summary, or durable doc update produced by a step.
- **Artifact:** temporary initiative-specific output such as brainstorming notes, brief, validation, Technical Design, Spec, task specs, QA, or prototypes.
- **Brief:** optional product-direction artifact that captures the problem, users, value proposition, solution direction, scope, hypotheses, and open questions before validation or specification.
- **Technical Design:** optional technical clarification artifact used before or during Spec drafting when technical decisions need focused exploration, comparison, or user validation.
- **Spec:** parent initiative source of truth, usually an issue body, that combines accepted product behavior, technical decisions, testing decisions, scope boundaries, and enough context to split work safely.
- **Task Spec:** child issue or local task artifact for one vertical slice. It is the task-level Execution Contract, not the parent initiative source of truth.
- **Durable documentation:** long-term project memory, versioned in the repository when useful.
- **AFK | HITL:** `AFK` means a clear, testable, unblocked task that an agent can self-approve; `HITL` means human judgment is required before or during execution. Classification rubric lives in `Slice`.
- **Human gate:** decision point where the human validates, arbitrates, or blocks further progress.
- **Feedback loop:** reliable signal that proves a change state. Examples: test, typecheck, lint, build, CI, reproduction, dev server, browser verification, profiler, or release check.
- **Vertical slice:** smallest user-visible end-to-end behavior that produces a useful feedback signal, including only the layers it actually needs (data, logic, API, minimal UI, tests).
- **Tracer-bullet slice:** vertical slice intentionally chosen first to surface integration risk, technical feasibility, or end-to-end ambiguity early, even when it is not the most user-valuable slice.
- **Execution Contract:** minimum content an agent needs to implement a task safely (defined in [Step Anatomy § Definition of Ready](#definition-of-ready))

---

## Workflow Principles

- **Frame before coding:** formalize just enough based on scope, risk, and uncertainty.
- **Separate concerns:** `brief.md`, `technical-design.md`, `spec.md`, and `tasks/*.md` answer different questions.
- **Consolidate initiative truth:** the Spec is the parent source of truth for an initiative. Upstream discovery artifacts and Technical Design outputs feed the Spec; they should not remain competing truth once accepted decisions are integrated.
- **Make technical decisions explicit:** codebase changes need technical decisions somewhere. Keep simple decisions inline in the Spec; use Technical Design when stack, architecture, data, API, migration, integration, security, performance, or testing decisions need focused exploration.
- **Build verifiable vertical slices:** every task should produce a useful end-to-end signal.
- **Keep humans on judgment:** product, UX, architecture, security, review, QA, and release decisions remain `HITL` when stakes are real.
- **Rely on feedback loops:** tests, typecheck, lint, build, CI, and reproduction define the achievable quality ceiling.
- **Capitalize only what lasts:** temporary artifacts must not become stale project truth, durable `docs/*` is the project's long-term memory.

---

## Overview

The workflow is intention-driven: use steps as needed, not mechanically. The canonical flow plus the most useful loopbacks looks like this:

```text
Setup     : [workflow-setup]
Discovery : [brainstorm] -> [brief] -> [validate]
Clarify   : [grill-me | grill-with-docs | technical-design] as needed before Spec or Slice
Planning  :  spec -> [slice]
Execution : build -> [code-simplify] -> [review] -> [qa] -> [capitalize]
Release   : [ship-readiness]

Loopbacks :
  review --> build                               (when changes requested)
  qa     --> build | diagnose                    (when defects found)
  build  --> spec | technical-design | slice     (when execution contract is insufficient)
  build  --> capitalize                          (when implementation invalidates upstream artifacts)

Specialization (used on demand, never inserted as a fixed link in the canonical flow):
  [project-baseline]              - durable understanding of an existing project
  [zoom-out]                      - map a code area before editing
  [diagnose]                      - isolate and fix a bug through disciplined diagnosis
  [improve-codebase-architecture] - rank structural refactor candidates
  [prototype-ui]                  - disposable UI exploration
```

Brackets indicate optional or contextual steps. `Grill Me`, `Grill With Docs`, and `Technical Design` can be inserted wherever unresolved decisions block the next artifact. Operational details live in `steps/`; this document explains how to choose a path, where outputs belong, and what each step must contain.

---

## Workflow Router

Choose the smallest path that gives enough clarity and feedback for the risk. Earlier discovery or clarification steps can be skipped when the current prompt, issue, Spec, or task already contains a sufficient Execution Contract.

| Scenario | Minimum useful path |
| --- | --- |
| First use in a repository | `Workflow Setup -> [Project Baseline]` |
| Existing project, weak docs | `Workflow Setup -> Project Baseline -> [Zoom Out] -> Spec or Technical Design` |
| Legacy or abandoned project | `Workflow Setup -> Project Baseline -> [Spec] or [Technical Design]` |
| Trivial fix or hotfix | `Build -> [Review]` |
| Small clear feature | `Minimal Spec or Execution Contract -> Build -> [Review] -> [QA if user-facing]` |
| Medium feature | `Spec -> [Slice if multi-task] -> per-task(Build -> [Review]) -> [QA] -> [Capitalize]` |
| Large feature on an existing project | `[Brief] -> [Validate] -> [Grill Me or Grill With Docs as needed] -> [Technical Design] -> Spec -> Slice -> per-task(Build -> Review) -> [QA] -> [Capitalize]` |
| Risky technical change | `[Technical Design] -> Spec -> Slice or Build (mode: tdd) -> Review -> [QA] -> [Ship Readiness]` |
| Hard bug or performance regression | `Diagnose -> Review -> [QA] -> [Capitalize]` |
| Unknown code area | `Zoom Out` |
| Structural refactor | `[Zoom Out] -> Improve Codebase Architecture -> [Grill With Docs] -> Technical Design -> Spec -> Slice -> per-task(Build -> Review) -> [QA] -> Capitalize` |
| Hard-to-read code after a build | `Build -> Code Simplify -> Review` |
| Uncertain UI | `[Prototype UI] -> [Brief if direction unclear] -> Spec or Build -> [Review] -> [QA]` |
| Idea exploration | `Brainstorm -> [Brief] -> [Validate]` |
| Large initiative or MVP from scratch | `[Brainstorm] -> Brief -> Validate -> [Grill Me] -> [Technical Design] -> Spec -> Slice -> per-task(Build -> Review) -> [QA] -> [Capitalize]` |
| Sensitive release | `... -> Review -> [QA] -> Ship Readiness` |
| Agent output keeps drifting | `Workflow Setup -> [Project Baseline] -> resume current step` |

Use optional steps for the uncertainty they remove, not because a path looks more complete: Brainstorm expands options, Brief converges product direction, Validate reduces product or business uncertainty, Grill resolves decision trees, Grill With Docs aligns intent with code and durable vocabulary, and Technical Design resolves material technical uncertainty.

---

## Step List

Detailed definitions live in `steps/`. Filenames in `steps/` use a numeric prefix (`001-…` to `009-…`) for the canonical planning and execution order. Optional steps can still be skipped when their trigger does not fire. `workflow-setup.md` and specialization steps stay unnumbered because they don't have a fixed position in the canonical flow.

### Core Workflow

- **[Brief](steps/001-brief.md)** - `brief` - core, optional. Converges rough product context into a lightweight direction.
- **[Validate](steps/002-validate.md)** - `validate` - core, optional. Reduces uncertainty from the brief before deeper specification.
- **[Technical Design](steps/003-technical-design.md)** - `technical-design` - core, optional. Resolves material technical uncertainty before accepted decisions are integrated into the Spec.
- **[Spec](steps/004-spec.md)** - `spec` - core, required for initiatives except trivial direct work. Creates the parent source of truth combining product behavior, technical decisions, testing decisions, and scope.
- **[Slice](steps/005-slice.md)** - `slice` - core, required (for multi-task initiatives). Splits work into vertical, verifiable tasks and classifies each as `AFK | HITL`.
- **[Build](steps/006-build.md)** - `implement` (with `direct` and `tdd` modes) - core, required. Implements one task from a sufficient Execution Contract.
- **[Review](steps/007-review.md)** - `review` - core, recommended. Performs a cold review focused on bugs, risks, and contract deviations.
- **[QA](steps/008-qa.md)** - `qa` - core, recommended (when manual validation is useful). Produces a manual QA plan and may record observed results.
- **[Capitalize](steps/009-capitalize.md)** - `capitalize` - core, recommended (when durable information changed). Updates durable docs, ADRs, follow-ups, or reports that no durable update is useful.

### On-Demand Steps

- **[Workflow Setup](steps/workflow-setup.md)** - `workflow-setup` - on-demand. Establishes repo-level agent rules and `AGENTS.md` pointers.
- **[Brainstorm](steps/brainstorm.md)** - `brainstorm` - on-demand. Opens the option space without converging too early.
- **[Grill Me](steps/grill-me.md)** - `grill-me` - on-demand. Interviews the user one question at a time to resolve important decisions.
- **[Grill With Docs](steps/grill-with-docs.md)** - `grill-with-docs` - on-demand. Aligns intent with domain language, docs, ADRs, and existing code.
- **[Prototype UI](steps/prototype-ui.md)** - `prototype-ui` - on-demand. Explores disposable frontend directions before clean integration.
- **[Diagnose](steps/diagnose.md)** - `diagnose` - on-demand. Fixes a complex bug through disciplined diagnosis.
- **[Zoom Out](steps/zoom-out.md)** - `zoom-out` - on-demand. Maps an unknown code area before modification.
- **[Improve Codebase Architecture](steps/improve-codebase-architecture.md)** - `improve-codebase-architecture` - on-demand. Identifies structural refactor opportunities.
- **[Code Simplify](steps/code-simplify.md)** - `code-simplify` - on-demand. Simplifies recently changed code while preserving behavior.
- **[Project Baseline](steps/project-baseline.md)** - `project-baseline` - on-demand. Establishes durable understanding of an existing project.
- **[Ship Readiness](steps/ship-readiness.md)** - `ship-readiness` - on-demand. Optional release gate before sensitive delivery.

---

## Step Anatomy

Steps in `steps/` are the specifications for future agent skills of the workflow. Each step is **self-contained**: it describes its own work, conditions, and output without naming other steps as routing destinations. Step ordering and loopbacks live in this document, not in step files.

Future skills should not use the same shape as the step specifications; they should use the smallest and simplest shape that works for each skill.

When converting a step into a skill, extract only what the skill needs to run well: trigger, required context, stop conditions, minimum output, and verification. Keep long templates or rare examples in references instead of inflating the skill body.

Every future skill of the workflow should pick the smallest useful size before writing. Prefer `lite` until scope, risk, or uncertainty justifies more.

### Gate Strength

Human gates should state the decision and its approval strength when useful:

- **Self-approvable:** clear `AFK` work, low risk, no product judgment, no public interface change, no migration, no security/privacy impact, and no irreversible or externally visible action.
- **Async:** human review is useful, but work can continue without committing to irreversible, externally visible, or high-risk decisions.
- **Blocking:** stop for human validation before product scope changes, UX judgment, architecture boundaries, migrations, public APIs, security/privacy decisions, destructive actions, external publication, deployment, or accepted release risk.

### Definition of Ready

A task is ready for `Build` step when it has a sufficient "Execution Contract".

The "Execution Contract" is not a new document. It is the minimum content an agent must have available in its context to implement a task. It can live in the session history, prompt, Spec, Technical Design, task spec, issue, or any other source of truth loaded into the agent's context.

Minimum content:

- scope (what should be built)
- expected behavior (what results are observable by user or system)
- task-level acceptance criteria (testable criteria)
- edge cases
- non-goals
- verification
- verification commands or feedback commands if known
- `blocked-by` dependencies when applicable
- `AFK | HITL` type when useful
- technical constraints, without a detailed implementation plan

If the Execution Contract is incomplete, route back to `Spec`, `Technical Design`, `Slice`, `Grill Me`, or `Grill With Docs`.

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
- `CONTEXT.md` (optional): durable domain vocabulary and shared terms used in the project.
- `CONTEXT-MAP.md` (optional): bounded context map if the project has several.
- `AGENTS.md`: agent-specific rules and trigger-based pointers to `.agents/rules/*`.
- `README.md`: project entry point and reference guide for humans and agents.

Create durable docs only when there is real information to maintain.

### Artifacts (Initiative Outputs)

Artifacts are temporary initiative-specific working materials generated during the workflow. Examples: brainstorming, brief, validation, Technical Design, Spec, task specs, QA, etc.

Step files own their default output targets. Repository-specific mechanics for local artifacts and tracker publication belong in `.agents/rules/output-locations.md`.

Every artifact, publication, or durable-doc write outside normal code implementation requires explicit user confirmation after the draft exists. If the user does not confirm, keep the output in the session only.

#### Local Markdown Artifacts

Local Markdown is useful for temporary, solo, exploratory, or local-first initiative work. The standard path is `.initiatives/001-initiative-slug/`, with kebab-case initiative and task slugs. Ask before adding `.initiatives/` to `.gitignore` when local artifacts should stay untracked and the repository does not already ignore them.

Recommended structure for local Markdown artifacts:

```text
/
├─ README.md
├─ AGENTS.md
├─ CONTEXT.md                    (durable domain glossary, optional)
├─ CONTEXT-MAP.md                (if several bounded contexts, optional)
├─ .agents/                      (optional agent rules)
│  └─ rules/
│     ├─ output-locations.md
│     ├─ feedback-commands.md
│     ├─ context-sources.md
│     └─ agent-boundaries.md
├─ .initiatives/                 (gitignored by default)
│  ├─ 001-<initiative>/
│  │  ├─ brainstorming.md        (optional)
│  │  ├─ brief.md                (optional)
│  │  ├─ validation.md           (optional)
│  │  ├─ technical-design.md     (optional)
│  │  ├─ spec.md
│  │  ├─ qa.md                   (optional)
│  │  └─ tasks/
│  │     ├─ 001-<task>.md
│  │     └─ ...
│  └─ 002-<initiative>/
│     └─ spec.md
├─ docs/
│  ├─ architecture.md
│  ├─ conventions.md
│  ├─ testing-strategy.md
│  └─ decisions/
│     └─ 001-*.md                (ADRs / durable decisions)
└─ apps/, packages/, scripts/    (project-specific folders)
```

Naming rules:

- one folder per initiative, in kebab-case, prefixed with `001-`, `002-`, etc.
- `tasks/` exists only if the initiative has multiple tasks
- one file per task, in kebab-case, prefixed with `001-`, `002-`, etc.

#### Issue Tracker Publication

Tracker publication is GitHub-first but adaptable to Gitlab, Linear, Jira, or another tracker through the official CLI or an MCP server. A step should draft the content first, then ask before each tracker write or update.

GitHub Issues conventions:

- Spec: parent issue body owns the initiative source of truth, including accepted product behavior, technical decisions, testing decisions, and scope boundaries
- Technical Design: publish as a parent issue comment or local artifact only when focused technical clarification has standalone value; integrate accepted decisions into the Spec before slicing
- Tasks / Slices: create one normal task issue per vertical slice; each task issue references the parent Spec issue; add a parent issue comment that links the task issues after confirmation
- Review, QA, Diagnose, Ship Readiness, and similar outputs: publish comments when coordination, auditability, or handoff value justifies it

#### Artifacts Lifecycle

When an initiative closes, associated artifacts should be archived, closed, deleted, or consolidated into durable documentation. Old artifacts should not become implicit source of truth for agents.

Evolution rules:

- keep completed initiative history intact
- if constraints, scope, or future tasks change without a major pivot: update the active initiative
- if the work becomes independent, opens a major pivot, or the previous initiative is historical: open a new initiative
- if shipped behavior must change: create a new task or initiative
- if implementation invalidates future tasks: draft Spec, Technical Design, and upcoming task spec updates promptly, then ask before writing or publishing them

#### Output Format

Each step should produce the smallest useful output for the current decision, execution, or validation.

Guidelines:

- choose the size level before writing the output
- only include sections that change a decision, remove ambiguity, or support execution
- omit empty sections
- link source material instead of copying it
- finish with decisions made, blocking open questions, and the recommended next step when relevant

### Workflow Rules for Agents

Workflow-related agent guidance lives in `.agents/rules/`, with trigger-based pointers from `AGENTS.md`. These files are agent-oriented operational rules, not a centralized workflow registry.

The `Workflow Setup` step owns the concrete rule-file templates and `AGENTS.md` pointer block. Step specs and future skills should not tell agents to check, load, or read `.agents/rules/*` files; agents decide when rules are needed from the `AGENTS.md` pointer block.

Lifecycle rules for the workflow:

- Rerun `Workflow Setup` when repo-level agent rules or `AGENTS.md` pointers should change.
- Rerun `Project Baseline` when architecture, conventions, testing strategy, domain vocabulary, or durable decisions become stale.
- If `Project Baseline` creates, moves, or renames durable docs, it may update `.agents/rules/context-sources.md` pointers after explicit confirmation.
- If durable agent guidance changes during an initiative, `Capitalize` may update `.agents/rules/*` after explicit confirmation.

If these docs do not exist, agents continue silently unless the user asks to set them up or the current task exposes a real need. Durable project knowledge belongs in project docs such as `README.md`, `docs/*`, `CONTEXT.md`, `CONTEXT-MAP.md`, or `docs/decisions/*`.

---

## Global Rules

### Feedback Loops

- Without reliable feedback, the agent codes blind.
- Document real project commands in `.agents/rules/feedback-commands.md`, `README.md`, `AGENTS.md`, `docs/testing-strategy.md`, or equivalent.
- Minimal useful feedback: typecheck, build, lint, automated tests, formatting, and fast CI.
- Advanced feedback: accessible dev server, browser verification, targeted e2e tests, verifiable migrations, reproducible seeds.
- When test, build, CI, or runtime breaks, resolve or document the blocker before expanding scope.
- For a bug, the feedback loop is the main product of diagnosis.

### Context Engineering

- Load useful context, not the whole repository.
- Keep artifacts, files, and patterns relevant to the task.
- Use `Zoom Out` before modifying an unknown or hard-to-locate area.
- Prefer `/clear` over `/compact` between major steps or before review.
- Use Specs, task specs, issues, docs, and tests as external memory instead of full chat history.
- Keep the system prompt and pushed instructions as short as possible.
- Create `CONTEXT.md`, `CONTEXT-MAP.md`, or ADRs only when a real term or decision has stabilized.

### Source-Driven Decisions

- Check official documentation when a decision depends on a framework or library.
- Report conflicts between official docs and repository patterns before deciding.
- Use durable vocabulary in issue titles, Specs, tests, hypotheses, and plans.
- Use `Grill With Docs` when required terms are missing or contradict code usage.
- Report conflicts with durable decisions explicitly.

---

## Delivery

This workflow covers framing, slicing, implementation, review, and validation;

Commit, PR, CI, release, and deployment remain team or project responsibilities, with `ship-readiness` as an optional gate before sensitive delivery. Build, Review, QA, and Ship Readiness outputs should still preserve enough verification, blocker, contract-drift, and risk context for a clean handoff.

## Credits

A huge thanks to [@mattpocock](https://github.com/mattpocock) for sharing his workflow and agent skills; it greatly inspired this one.
