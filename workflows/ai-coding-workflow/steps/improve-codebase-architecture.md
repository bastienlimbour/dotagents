# Improve Codebase Architecture

**Skill name:** `improve-codebase-architecture`

**Step type:** On-demand step.

**Role:** Identify structural improvement candidates that make code more local, testable, navigable, and agent-friendly.

**When to use:** Ball of mud, shallow modules, hard-to-write tests, duplicated logic, structural refactor, missing regression seam after `Diagnose`, or maintenance of a fast-evolving codebase with agents.

**Possible inputs:** Repository, scoped code area, `CONTEXT.md`, `CONTEXT-MAP.md`, ADRs, existing tests, recent bugs, review findings, maintenance pain points, performance or reliability issues.

**Process:**

1. Bound the review area or maintenance goal.
2. Read relevant domain language and durable decisions before judging module shape.
3. Explore areas where understanding requires too many jumps between modules.
4. Apply the deletion test to suspicious modules: useful modules keep complexity local; shallow modules push complexity into callers.
5. Look for shallow modules, misplaced seams, unnecessary adapters, tests coupled to details, scattered logic, and missing regression seams.
6. Classify dependencies as `in-process`, `local-substitutable`, `remote-owned`, or `true external` when it affects test strategy.
7. Propose the 3 to 5 most actionable candidates.
8. Rank candidates by impact, effort, risk, and confidence.
9. Recommend whether the selected candidate needs `Tech Design`, ADR, PRD, or a refactor task.

**Rules:**

- This step proposes candidates first.
- Structural implementation needs a selected candidate and a sufficient Execution Contract.
- Start interface design only after the user chooses a candidate.
- Ground candidates in observed friction, not abstract architectural preference.
- Use project vocabulary and report conflicts with durable decisions.

**Output:** Ranked architecture improvement candidates grounded in observed friction, with impact, risk, test strategy, and recommended next step.

**Output location:** Check `.agents/workflow/output-locations.md` when it exists. Recommended default: session candidate list. If a parent issue exists, publish a summary comment after user validation. Create a new initiative only after a candidate is selected.

**Output template:**

```markdown
## Architecture Improvement Candidates

## Scope
<!-- Required. Paragraph, 1-3 sentences: code area, maintenance goal, or pain point reviewed. -->
<Scope reviewed.>

## Candidates
<!-- Required. Numbered subsections. Keep to 3-5 candidates. -->

### 1. <Candidate title>
- **Observed problem:** <Architectural friction grounded in code.>
- **Proposed direction:** <Prose solution, not final interface design.>
- **Locality / leverage benefit:** <Why this improves change and test locality.>
- **Test impact:** <New or improved test seam.>
- **Impact:** Low / Medium / High
- **Effort:** Low / Medium / High
- **Risk:** Low / Medium / High
- **Confidence:** Low / Medium / High
- **Decision conflicts:** <ADR or convention conflict, if any.>
- **Recommended next step:** <Tech Design / ADR / refactor task / no action>

## Recommendation
<!-- Required. Paragraph, 1-3 sentences: candidate to discuss first and why. -->
<Recommendation.>
```

**Possible sizes:** Quick candidate scan for one module; standard architecture review for one subsystem; full candidate discovery for a legacy or fast-changing codebase.

**Verification:** Candidates are grounded in observed friction, use project vocabulary, explain locality/test benefits, and can become separate Execution Contracts if selected.

**Human gate:** Choose the candidate to explore, validate the structural interface, and decide whether the refactor deserves an initiative.
