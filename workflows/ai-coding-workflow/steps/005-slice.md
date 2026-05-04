# 005 - Slice

**Skill:** `slice`

**Status:** Core step for multi-task initiatives.

**Role:** Turn `PRD + optional Tech Design + repository context` into small, vertical, verifiable tasks.

**When to use:** Multi-task initiative. Skip it for a minimal single-task PRD with a sufficient Execution Contract.

**Possible inputs:** `prd.md`, `tech-design.md`, ADRs, repository context, product priorities, team constraints.

**Actions:**

- split the initiative into vertical slices
- build each slice as a verifiable end-to-end increment, even if minimal
- include the layers needed by the slice: data, logic, API/routes, minimal UI, and tests when relevant
- avoid horizontal tasks by technical layer (`DB -> API -> UI`)
- order tasks by real dependencies, as a graph rather than a linear plan
- keep each task behaviorally self-contained
- make each task independently grabbable by an agent
- seek end-to-end feedback early, even through a narrow tracer bullet
- avoid copying the PRD or Tech Design into every task
- classify each task as `AFK` or `HITL` when it helps execution
- map tasks to corresponding acceptance criteria
- reference the PRD and Tech Design with short links when useful
- present the slice breakdown to the human before publication: granularity, dependencies, merge/split decisions, `AFK | HITL` classification
- if the active artifact location is GitHub Issues or an equivalent tracker, propose one sub-issue per vertical slice in dependency order

**Output:** sub-issues per vertical slice by default, or one task spec per task in `tasks/` when local Markdown mode is selected.

**Artifact publication:** If a GitHub/tracker parent issue exists, propose creating one sub-issue per slice, each with its Execution Contract and a link to the parent issue. If the primary artifact location is local Markdown, propose `.initiatives/<initiative>/tasks/*.md`. After publication, propose updating the canonical parent issue body with links to the sub-issues.

**Output contents:**

Required content:

- id and title
- short context
- goal
- end-to-end behavior to build
- testable acceptance criteria
- expected verification

Conditional content:

- parent when derived from a PRD or parent issue
- useful edge cases
- local non-goals when useful
- PRD references
- Tech Design references when useful
- expected feedback commands when known
- `blocked-by` dependencies when applicable
- `AFK | HITL` type when useful
- likely touchpoints, without imposing a code plan

Avoid:

- copying the PRD or Tech Design
- detailed implementation plan
- horizontal tasks by technical layer

**Possible sizes:** minimal task spec for a simple task, detailed task spec for a critical or ambiguous task.

**Human gate:** validate granularity, verticality, order, dependencies, verifiability, and `AFK | HITL` classification.

**Important:** A task spec is not a detailed implementation plan. Exact files, commands, and code sequence remain in the `Build Preflight`. A blocked task must not be taken as AFK.

Prefer several small reviewable slices over one large task that becomes testable only at the end. A narrow slice that crosses the system is better than a batch of layer-separated tasks.

Do not implicitly close, rewrite, or modify the parent issue when creating slices.
