# Grill With Docs

**Skill:** `grill-with-docs`

**Status:** On-demand step.

**Role:** Challenge an intent or plan against domain language, durable docs, ADRs, and existing code.

**When to use:** Existing project, ambiguous business vocabulary, plan touching multiple modules, structural refactor, need to align product and codebase before `PRD` or `Tech Design`.

**Possible inputs:** intent, `brief.md`, `grill-me` summary, draft PRD, draft Tech Design, `CONTEXT.md`, `CONTEXT-MAP.md`, `docs/decisions/`, existing architecture, relevant code.

**Actions:**

- inspect `CONTEXT.md`, `CONTEXT-MAP.md`, ADRs, project docs, and relevant code
- limit analysis to sources useful for the given intent
- distinguish observed facts, recommendations, and decisions to validate
- immediately challenge vague, overloaded, or inconsistent terms
- ask questions one at a time when code or docs are insufficient
- provide a recommendation for each question
- resolve conflicts between plan vocabulary, code vocabulary, and existing decisions
- update durable vocabulary inline when a term is stabilized, or explicitly propose the update if it needs validation
- create `CONTEXT.md`, `CONTEXT-MAP.md`, or `docs/decisions/` only at the first real need
- propose an ADR only for a decision that is hard to reverse, surprising without context, and based on a real trade-off

**Output:** session summary, updates to `CONTEXT.md` or `CONTEXT-MAP.md`, proposed or created ADRs, integration into `PRD`, `Tech Design`, or an active artifact location.

**Artifact publication:** If an active initiative exists, propose integrating decisions into the parent issue, PRD, or Tech Design instead of creating a separate artifact. If a term or decision becomes durable, propose updating `CONTEXT.md`, `CONTEXT-MAP.md`, or `docs/decisions/`; create or modify these docs only with stabilized information.

**Output contents:**

Required content:

- clarified decisions
- selected domain terms
- resolved vocabulary conflicts
- remaining ambiguities

Conditional content:

- cited code/docs sources when they justify a decision
- durable docs updated or to update
- proposed ADRs when needed

Avoid:

- exhaustive codebase map
- creating durable docs without a stabilized term or decision
- proposing an ADR without a real durable trade-off

**Possible sizes:** micro-alignment on a term or interface, or full pre-PRD session on an existing project.

**Human gate:** validate terms, durable decisions, and ADRs before they become source of truth.

**Important:** `grill-with-docs` does not replace `Review`. It aligns language and decisions before construction. It succeeds the former `domain-model` skill.
