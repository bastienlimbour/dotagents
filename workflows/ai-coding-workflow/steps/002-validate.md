# 002 - Validate

**Skill:** `validate`

**Status:** Optional core step.

**Role:** Reduce external uncertainty before investing in a full PRD, Tech Design, or costly implementation.

**When to use:** Uncertainty about market, competition, users, external dependencies, business model, feasibility, or product risk. Skip it when the idea is safe or the stakes are low.

**Possible inputs:** `brief.md`, `grill-me` or `grill-with-docs` summary, assumptions to test, open questions, business or user constraints.

**Actions:**

- turn uncertainties into testable assumptions and decision thresholds
- timebox research based on the stakes
- perform deep web research and collect external signals
- analyze competition, alternatives, market, users, or business model when relevant
- challenge assumptions from the brief
- identify risks, external dependencies, and major constraints
- produce a reasoned `Go / No-Go / Pivot` verdict with confidence level

**Output:** validation summary in session, optional local `validation.md`, or tracker comment if an active initiative exists.

**Artifact publication:** By default, keep validation in the session/chat or in gitignored `.initiatives/<initiative>/validation.md`. If a parent issue already exists and validation justifies `Go / No-Go / Pivot`, propose a summary comment and consolidate the important decision into the PRD or canonical body.

**Output contents:**

Required content:

- assumptions tested
- method and useful sources
- key observed signals
- recommendations
- `Go / No-Go / Pivot` verdict and confidence level

Conditional content:

- market / competition / alternatives analysis
- user or business signals
- feasibility
- external dependencies
- risks and constraints

Avoid:

- encyclopedic market summary
- source list not used in the reasoning
- long excerpts copied from the web

**Possible sizes:** quick validation of a few assumptions, or full validation for a strategic initiative.

**Human gate:** continue, pivot, or stop.

**Important:** `Validate` tests a converged direction. It replaces neither `Brief` nor `PRD`.
