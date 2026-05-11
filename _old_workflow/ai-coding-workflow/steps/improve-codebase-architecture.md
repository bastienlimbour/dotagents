# Improve Codebase Architecture

**Skill name:** `improve-codebase-architecture`

**Step type:** On-demand.

**Role:** Identify structural improvement candidates that make code more local, testable, navigable, and agent-friendly.

**When to use:** Ball of mud, shallow modules, hard-to-write tests, duplicated logic, structural refactor, missing regression seam after a diagnosis, or maintenance of a fast-evolving codebase with agents.

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
9. Classify the follow-up type each candidate would need: design-needed, decision-needed, direct-refactor, or no-action.

**Rules:**

- This step proposes candidates first.
- Structural implementation needs a selected candidate and a sufficient Execution Contract.
- Start interface design only after the user chooses a candidate.
- Ground candidates in observed friction, not abstract architectural preference.
- Use project vocabulary and report conflicts with durable decisions.

**Output:** Ranked architecture improvement candidates grounded in observed friction, with impact, risk, test strategy, and follow-up classification.

**Output location:** Recommended default: session candidate list. If a parent issue exists, ask before publishing a summary comment after user validation. Ask before creating any new issue or local initiative artifact after a candidate is selected. If the user does not confirm, keep the candidate list in session only.

**Output template:**

```markdown
## Summary
<!-- Required. Paragraph, 1-3 sentences: scope reviewed and the candidate to discuss first. -->
<Architecture review summary.>

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
- **Follow-up type:** design-needed / decision-needed / direct-refactor / no-action

## Recommendation
<!-- Required. Paragraph, 1-3 sentences: candidate to discuss first and why. -->
<Recommendation.>
```

**Possible sizes:** lite (one module); standard (one subsystem); full (legacy or fast-changing codebase).

**Verification:** Candidates are grounded in observed friction, use project vocabulary, explain locality/test benefits, and can become separate Execution Contracts if selected.

**Human gate:** Choose the candidate to explore, validate the structural interface, and decide whether the refactor deserves an initiative.
