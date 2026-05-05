# 002 - Validate

**Skill name:** `validate`

**Step type:** Core workflow step (optional).

**Role:** Test the assumptions that could change whether an initiative should proceed, pivot, or stop.

**When to use:** After a converged brief when product, market, feasibility, or business uncertainty could change the next investment decision.

**Possible inputs:** `brief.md`, grill summary, assumptions to test, open questions, business constraints, user constraints, external sources, repository constraints when feasibility matters.

**Process:**

1. Extract assumptions that could change the decision.
2. Define `Go / Pivot / No-Go` thresholds before researching when possible.
3. Choose validation depth and timebox based on risk and investment level.
4. Validate across relevant tracks: product, market, technical feasibility, and finances.
5. Grade evidence strength and confidence per track.
6. Challenge what changed from the brief.
7. Synthesize one decision memo with verdict, confidence, and recommended next step.

**Rules:**

- `Validate` tests a converged direction. It does not replace `Brief` or `PRD`.
- Prefer official, primary, recent, or directly observed sources when external facts matter.
- Do not overstate weak evidence; make confidence and uncertainty explicit.
- Use the smallest validation depth that can change the investment decision.

**Output:** Markdown validation note with tested assumptions, evidence synthesis, confidence, and `Go / Pivot / No-Go` verdict.

**Output location:** Check `.agents/workflow/output-locations.md` when it exists. Recommended default: local `.initiatives/<initiative>/validation.md`. If a parent issue already exists, publish only the decision summary when it changes current execution truth.

**Output template:**

```markdown
# <Initiative> Validation

## Verdict
<!-- Required. Metadata list plus one concise rationale sentence. -->
- **Decision:** Go / Pivot / No-Go
- **Confidence:** Low / Medium / High
- **Rationale:** <One-sentence synthesis.>

## Assumptions Tested
<!-- Required. Bullet list: one tested assumption per bullet. -->
- **<Assumption>:** <Why it matters and what would change.>

## Evidence by Track
<!-- Required. Keep each track to a short paragraph or 2-4 bullets. Omit a track only when irrelevant and state why. -->

### Product
<Observed signal, evidence strength, and conclusion.>

### Market
<Observed signal, evidence strength, and conclusion.>

### Technical Feasibility
<Observed signal, evidence strength, and conclusion.>

### Finances
<Observed signal, evidence strength, and conclusion.>

## What Changed
<!-- Required. Bullet list: what changed from the brief or initial belief. -->
- <Brief assumption confirmed, weakened, or revised.>

## Sources
<!-- Conditional. Bullet list: only sources used in the reasoning. -->
- <Useful source or observed signal.>

## Next Step
<!-- Required. One sentence: PRD / Brief revision / Brainstorm / stop, with rationale. -->
<Recommended next step and rationale.>
```

**Possible sizes:** Minimal validation for one risky assumption; standard four-track validation for a feature or MVP; full validation for a strategic, costly, or externally dependent initiative.

**Verification:** The verdict is traceable to tested assumptions, useful evidence, source quality, confidence, and explicit decision thresholds.

**Human gate:** Decide whether to continue, pivot, or stop.
