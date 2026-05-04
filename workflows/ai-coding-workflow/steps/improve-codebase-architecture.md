# Improve Codebase Architecture

**Skill:** `improve-codebase-architecture`

**Status:** On-demand step.

**Role:** Identify architectural friction and deepening opportunities that make code more testable, local, and navigable by agents.

**When to use:** Ball of mud, shallow modules, hard-to-write tests, duplicated logic, structural refactor, missing regression seam after `Diagnose`, or regular maintenance of a fast-evolving codebase with agents.

**Possible inputs:** repository, code area, `CONTEXT.md`, `CONTEXT-MAP.md`, `docs/decisions/`, existing tests, recent bugs, maintenance pain points.

**Actions:**

- read domain language and relevant decisions
- organically explore areas where understanding requires too many jumps between modules
- apply the deletion test to suspicious modules
- look for shallow modules, misplaced seams, unnecessary adapters, tests coupled to details, and scattered logic
- classify dependencies: in-process, local-substitutable, remote-owned, true external
- propose only the 3 to 5 most actionable deepening candidates
- rank candidates by impact, effort, risk, and confidence
- start a design discussion on the selected candidate and document durable terms or decisions when needed

**Output:** deepening candidates with affected files/modules, problem, proposed solution, leverage/locality benefits, test impact, risks, and next step.

**Artifact publication:** By default, present candidates in session and ask which candidate deserves an initiative. If a parent issue exists, propose a summary comment. Create an issue, PRD, Tech Design, or ADR only after a human chooses a candidate and validates the need for durable tracking.

**Output contents:**

Required content:

- numbered candidates
- observed architectural problem
- prose solution
- locality and leverage benefits
- impact, effort, risk, and confidence
- interface-based test strategy
- possible conflicts with existing decisions
- recommendation for `Tech Design`, ADR, or refactor task

Avoid:

- exhaustive inventory of every imperfection
- forcing the final interface before design discussion
- starting a large refactor without an Execution Contract

**Human gate:** choose the candidate to explore, validate the structural interface, and decide whether the refactor deserves an initiative.

**Important:** This skill proposes first. It must not start a large refactor without a human gate and an Execution Contract.

Useful dependency classification: `in-process` can be deepened directly and tested through the module interface; `local-substitutable` prefers a local substitute in tests; `remote-owned` justifies a port at the seam with production and test adapters; `true external` justifies an injected port and a targeted mock adapter.
