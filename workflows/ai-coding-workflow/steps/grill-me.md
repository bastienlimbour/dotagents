# Grill Me

**Skill:** `grill-me`

**Status:** On-demand step.

**Role:** Interview the user one question at a time until there is shared understanding and the important branches of the decision tree are resolved.

**When to use:** Clear idea with implicit decisions, plan/design to challenge, dependencies between decisions, ambiguous Execution Contract, explicit request to "grill me".

**Possible inputs:** brief, PRD, Tech Design, task spec, plan, intent, repository context.

**Actions:**

- identify blocking or high-leverage questions
- ask questions one at a time
- provide a recommendation for each question, ideally as choices when possible
- explore the repository instead of asking when the answer is discoverable
- resolve dependencies in the right order
- stop when important decisions are resolved, explicitly left open, or marginal value becomes low

**Output:** session summary, or integration into `brief.md`, `prd.md`, `tech-design.md`, task specs, or an active artifact location.

**Artifact publication:** By default, keep the decision log in session and propose integrating it into the next artifact. If a parent issue or task issue already exists, propose a short comment or body update only for decisions that change current truth.

**Output contents:**

Short decision log:

- clarified decisions
- accepted recommendations
- resolved questions
- branches left open
- assumptions to integrate into the next step
- remaining ambiguities

Avoid:

- full interview transcript
- non-blocking questions that slow the next step
- requests for information discoverable in the repository or docs

**Possible sizes:** micro-interview on one decision, or full interview on one intent.

**Human gate:** answer questions and validate accepted decisions.

**Important:** Usually use `Grill Me` once per intent, at the most useful ambiguity point:

- after `Brief`: clarify direction before validation or PRD
- after `PRD`: challenge scope, behaviors, and acceptance criteria
- after `Tech Design`: challenge technical trade-offs
- before `Build`: only if the Execution Contract is ambiguous
