# 002 - Validate

**Skill name:** `validate`

**Step type:** Core, optional.

**Role:** Reduce uncertainty around the product direction before investing in Spec creation, slicing, or implementation.

**When to use:** After a Brief or converged product direction when product, market, competitor, feasibility, business, or user-signal uncertainty should be reduced before committing to a Spec.

**Possible inputs:** `brief.md`, grill summary, assumptions to test, open questions, business constraints, user constraints, external sources, repository constraints when feasibility matters, prototype summary, existing user signals.

**Process:**

1. Extract critical assumptions from the Brief or current product direction.
2. Choose the validation variant: assumption check, user signal, technical spike, business case, finance check, bug/performance reproduction, or full multi-track validation.
3. Define `Go / Pivot / No-Go` thresholds before researching when possible.
4. Choose validation depth and timebox based on risk and investment level.
5. Validate only the tracks or signals relevant to the chosen variant: problem, product, market, competition, technical feasibility, finances, observed user signal, reproduction, or business constraints.
6. Grade evidence strength and confidence per relevant track or signal.
7. Challenge what changed from the Brief or initial belief.
8. Synthesize one decision memo with verdict, confidence, and the conditions that would change the verdict.

**Rules:**

- `Validate` tests a converged direction. It does not replace `Brief` or `Spec`.
- Prefer official, primary, recent, or directly observed sources when external facts matter.
- Do not overstate weak evidence; make confidence and uncertainty explicit.
- Use the smallest validation depth that can meaningfully reduce uncertainty before Spec creation.
- Omit irrelevant tracks rather than filling template sections with weak or empty analysis.

**Output:** Markdown validation note with tested assumptions, evidence synthesis, confidence, what changed from the Brief, and `Go / Pivot / No-Go` verdict.

**Output location:** Recommended default: ask before writing or updating local `.initiatives/001-<initiative>/validation.md`. If a parent issue already exists, ask before publishing a decision-summary comment when it changes current execution truth. If the user does not confirm, keep the validation note in session only.

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

## Evidence by Track or Signal
<!-- Required. Keep each relevant track to a short paragraph or 2-4 bullets. Omit irrelevant tracks and state why when omission affects interpretation. -->

### Product
<Observed signal, evidence strength, and conclusion.>

### Market
<Observed signal, evidence strength, and conclusion.>

### Competition / Alternatives
<Observed alternatives, differentiation, evidence strength, and conclusion.>

### Technical Feasibility
<Observed signal, evidence strength, and conclusion.>

### Finances
<Observed signal, evidence strength, and conclusion.>

## What Changed
<!-- Required. Bullet list: what changed from the Brief or initial belief. -->
- <Brief assumption confirmed, weakened, or revised.>

## Sources
<!-- Conditional. Bullet list: only sources used in the reasoning. -->
- <Useful source or observed signal.>

## Decision Pending On
<!-- Required. One sentence: what would change the verdict, or state that the verdict is final. -->
<What would change the verdict, or "Verdict is final.">
```

**Possible sizes:** lite (one risky assumption, user signal, or bug/performance reproduction); standard (multi-track validation for a feature or MVP, technical spike, or business/finance check); full (strategic, costly, or externally dependent initiative).

**Verification:** The verdict is traceable to tested assumptions, useful evidence, source quality, confidence, and explicit decision thresholds.

**Human gate:** Decide whether to continue, pivot, or stop.
