# Zoom Out

**Skill:** `zoom-out`

**Status:** On-demand step.

**Role:** Move up one abstraction level to understand how a code area fits into the system before editing it.

**When to use:** Unknown code area, stack trace crossing multiple modules, imminent refactor, domain onboarding, uncertainty about callers or seams.

**Possible inputs:** file, directory, symbol, stack trace, issue, PRD, task spec, modification intent, `CONTEXT.md`, durable decisions.

**Actions:**

- limit the map to the requested intent or area
- read domain vocabulary and relevant decisions when available
- map relevant modules, callers, data flows, seams, and adapters
- explain responsibilities in domain language rather than only file names
- flag coupling, ambiguity, or risk areas
- indicate confidence level and remaining unknowns when needed
- recommend the next step: `Build`, `Grill With Docs`, `Tech Design`, `Diagnose`, or `Improve Codebase Architecture`

**Output:** concise area map, relevant modules and callers, seams to preserve, risks, and recommended next step.

**Artifact publication:** By default, keep the map in session. If it supports an active initiative, propose a comment on the parent issue or relevant sub-issue; in local Markdown mode, propose a file in `.initiatives/<initiative>/` only if the map will be reused during the initiative.

**Output contents:**

Required content:

- area studied
- main responsibilities in domain language
- relevant callers, callees, or flows
- seams, adapters, or interfaces to preserve
- risks, coupling points, or ambiguities
- recommended next step

Conditional content:

- applicable domain terms or durable decisions
- external dependencies or known ownership
- confidence level and remaining unknowns

Avoid:

- full repository map unrelated to the intent
- detailed implementation plan
- proposed refactor without human gate

**Human gate:** confirm that the map matches the intent before a sensitive change.

**Important:** `Zoom Out` does not implement. It reduces the risk of modifying an area without understanding its system context.
