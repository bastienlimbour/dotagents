# 001 - Brief

**Skill:** `brief`

**Status:** Optional core step.

**Role:** Turn one or more ideas into a clear product direction. The brief is a lightweight opportunity note before investing in a PRD.

**When to use:** After brainstorming, for a new product, a large feature, an unclear idea, or when the opportunity needs framing. Skip it for a clear, bounded feature.

**Possible inputs:** Raw idea, notes, transcript, `brainstorming.md`, user signals, business or product context.

**Actions:**

- choose the useful brief depth: lightweight or full
- select and converge promising ideas or directions
- clarify the problem, target users, and value proposition
- describe the proposed solution at a high level, without technical details
- frame the expected scope: MVP, V1, Later, Excluded
- make assumptions, risks, constraints, non-goals, and open questions explicit
- recommend the next gate: `Grill Me`, `Grill With Docs`, `Validate`, or `PRD`

**Output:** session summary, optional local `brief.md`, or integration into the upcoming PRD.

**Artifact publication:** By default, keep the brief in the session/chat or in gitignored `.initiatives/<initiative>/brief.md`. Do not create the parent GitHub issue at the brief stage; create it at the PRD stage unless the user explicitly asks otherwise.

**Output contents:**

Required content:

- problem
- target users
- value proposition
- solution direction
- expected scope
- non-goals
- assumptions, risks, or open questions that affect the next step

Conditional content:

- main use cases
- important capabilities
- scope framing: `MVP / V1 / Later / Excluded`
- constraints
- recommended next gate

Avoid:

- technical details
- exhaustive list of rejected ideas
- raw duplication of brainstorming notes

**Possible sizes:** lightweight brief, or full brief for a new product / large initiative.

**Human gate:** confirm direction and initial scope before `Grill Me`, `Grill With Docs`, `Validate`, or `PRD`.

**Important:** The brief converges toward a clear product direction, but does not replace the PRD, external validation, or Tech Design.
