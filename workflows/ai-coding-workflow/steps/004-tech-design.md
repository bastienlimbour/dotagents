# 004 - Tech Design

**Skill:** `tech-design`

**Status:** Core step when technical impact is non-trivial.

**Role:** Technical source of truth. Tech Design defines how to build the product and formalizes structural decisions.

**When to use:** Non-trivial technical impact: architecture, data model, integration, migration, security, performance, scalability, observability, structural refactor, durable stack or library choice.

**Possible inputs:** `prd.md`, `grill-me` or `grill-with-docs` summary, repository context, existing architecture, existing technical docs, ADRs, conventions, external services, stack constraints, non-functional requirements.

**Actions:**

- choose the useful Tech Design depth: lite or full
- explore the repository and existing patterns
- read `CONTEXT.md`, `CONTEXT-MAP.md`, and relevant decisions when available
- verify official documentation when a decision depends on a framework or library
- document relevant current state, constraints, and technical requirements
- propose architecture, modules, and patterns
- identify possible deep modules: simple interface, encapsulated behavior, clear test boundary
- apply the deletion test to suspicious modules: if deleting the module removes the complexity, it was probably shallow; if complexity reappears in callers, it provides locality
- make seams and adapters explicit only when they map to real variation
- separate technical decisions from the immediate implementation plan
- decide stack, libraries, services, data model, interfaces/API, migrations, and test strategy
- identify impact on existing behavior, risks, rollback, and possible debt
- compare alternatives and formalize trade-offs
- create or reference ADRs when needed

**Output:** Tech Design summary in the parent issue by default, detailed comment when needed, or local `tech-design.md` when local Markdown mode is selected, with ADRs if needed.

**Artifact publication:** If a parent issue exists, propose consolidating a Tech Design Lite section into its body. For non-trivial Tech Design, propose a detailed comment linked from the canonical body. In local Markdown mode, propose `.initiatives/<initiative>/tech-design.md`. Durable decisions should be proposed as ADRs or project documentation, not only as comments.

**Output contents:**

Required content:

- technical context and relevant current state
- constraints and non-functional requirements
- approach or target architecture
- key technical decisions
- modules touched or created
- technical testing strategy
- technical risks
- open questions

Conditional content:

- stable interfaces, seams, and adapters when relevant
- test boundaries and test surface
- opportunities for depth, leverage, and locality
- integrations and external services
- data model
- interfaces/API
- migrations and compatibility
- security
- performance and scalability
- accessibility if technically impacted
- observability, monitoring, logs
- rollback plan when relevant
- alternatives considered
- accepted trade-offs
- ADRs to create or update

Avoid:

- rewriting the PRD
- file-by-file code plan
- exhaustive repository inventory
- security, performance, or observability sections without real impact

**Possible sizes:** Tech Design Lite for a limited change, full Tech Design for architecture, migration, or structural initiative.

**Human gate:** validate technical trade-offs, module boundaries, and structural interfaces before `Slice` or `Build`.

**Important:** By default, Tech Design comes after PRD. If technical feasibility is the main uncertainty, run a lightweight spike before PRD, then complete Tech Design after PRD.

An ADR is useful only when the decision is hard to reverse, surprising without context, and based on a real trade-off.

Recommended vocabulary: `module`, `interface`, `implementation`, `seam`, `adapter`, `depth`, `leverage`, `locality`. Here, an interface is not only a type signature: it is everything a caller must know to use the module correctly.

Depth is an interface property: a lot of useful behavior behind little surface area to learn. The interface is also the test surface; if a test must bypass the interface, the module shape is probably wrong.

Locality keeps changes, bugs, and knowledge in one place instead of scattering them across callers. A single seam or adapter often indicates a hypothetical abstraction; two real variants justify the seam better.
