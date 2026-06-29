---
name: validate
description: Reduces uncertainty around a product, technical, market, or business hypothesis through evidence, risks, confidence, red flags, and next validation experiments. Use when the user needs confidence before investing in a feature, solution, market direction, or implementation; not for specs, task splitting, prototyping, or implementing code.
---

# Validate

Validate an idea, solution, feature, technical direction, market bet, or business hypothesis before deeper investment. Make evidence, uncertainty, risks, confidence, and the cheapest useful next test explicit without deciding for the user.

## When To Use

- The user asks to validate, de-risk, assess confidence in, or sanity-check a product, technical, market, cost, legal, UX, distribution, or business hypothesis.
- A brief, brainstorming note, research note, issue, spec draft, conversation, codebase, or documentation should become a validation report.
- The useful next step depends on evidence for `Go`, `No-Go`, `Pivot`, or `Needs More Research`.

Do not use for broad brainstorming, product briefs, specs, task splitting, prototypes, implementation, or research without a specific validation target.

## Core Principle

Evidence over optimism. Prefer real behavior, commitments, observable workarounds, repo/docs facts, and cited sources over opinions, analogies, assumptions, or polite interest.

## Workflow

### 1. Resolve Target

Resolve create/update/conversation-only mode and the report target before collecting substantive evidence.

- Respect local artifact and tracker conventions already in context.
- If no local artifact convention exists, default to `.initiatives/<id>/validation.md` for initiative-specific validation and `docs/research/<slug>.md` only when reusable beyond the initiative.
- Start from any user-provided initiative, path, issue, brief, or existing validation report.
- If updating, inspect the report first and preserve useful content.
- If no target matches, propose one initiative and report path.
- Ask for confirmation before creating an initiative, selecting a path, publishing, or commenting.

Target confirmation does not approve report content. If the user declines an artifact, provide the report in conversation only.

### 2. Establish The Validation Question

Read available context enough to identify:

- Problem.
- Target user or segment.
- Current workaround or alternative.
- Proposed solution or hypothesis.
- Riskiest assumption.

Ask one targeted question at a time only when missing or conflicting information would materially change the validation design.

### 3. Choose Scope And Depth

Select relevant validation axes. The report must list every canonical axis in `Axis Coverage`, but detailed findings are needed only for `Covered` or `Partial` axes.

Canonical axes:

- User Problem.
- Demand And Commitment.
- Market And Competitors.
- Technical Feasibility.
- Costs And Business Model.
- Distribution And Acquisition.
- Legal Or Regulatory Risk.
- UX And Adoption.
- Differentiation.

State depth in plain language such as lightweight, focused, or deeper analysis; do not turn this into formal workflow modes.

Ask for confirmation before external research, deep analysis, tracker publication, or parallel research. Use subagents only when independent axes benefit from separation, then condense into one report.

### 4. Gather And Classify Evidence

Use available sources before guessing or asking. For technical validation, inspect relevant code, tests, docs, ADRs, issues, schemas, routes, config, or existing behavior before asking the user. Cite important sources.

Classify material as:

- Facts.
- Hypotheses.
- Weak signals.
- Interpretations.
- Unknowns.

Keep confidence proportional to evidence quality.

Evidence strength from strongest to weakest:

1. Payment, contract, preorder, repeated usage, or committed design partner.
2. Direct conversations about pains, budgets, and workarounds.
3. Observable behavior.
4. Market data, benchmarks, competitors, or repo/docs facts.
5. Founder claims, analogies, unsupported opinions, or polite interest.

### 5. Analyze Confidence And Risks

For each covered or partially covered axis, state finding, evidence, interpretation, confidence, risks/unknowns, and next signal to seek. Use `High`, `Medium`, or `Low` confidence.

Red flags should cap confidence:

- Vague target user.
- Weak pain, frequency, or cost.
- No workaround or budget.
- Marginal differentiation.
- Heavy workflow change.
- Weak business model.
- Material legal, privacy, or security risk.
- Unproven technical feasibility.
- Evidence mostly from friendly opinions.

### 6. Draft And Save

Use `assets/templates/validation.md` for new reports and as a structural guide for updates. Replace placeholders with concrete content; use `Not known yet` when evidence is missing.

Show the draft in conversation and wait for explicit content approval before saving, publishing, or commenting. If the user declined an artifact, deliver the report in conversation only.

## Guardrails

- Do not decide for the user; a verdict is a recommendation, not certainty.
- Do not recommend spec or implementation when evidence is weak; use `Needs More Research` and propose the next test.
- Do not update product briefs, specs, tasks, issues, ADRs, global docs, or separate research files unless the user explicitly asks and confirms.
- Do not impose Lean Canvas, SWOT, PESTLE, weighted scoring, mandatory interviews, triage labels, autonomous loops, or unsupported trackers.
- Do not include secrets, credentials, raw personal data, sensitive customer exports, or confidential material.

## Output

End with:

- Validation target and riskiest assumption.
- Sources or evidence used.
- Strongest and weakest evidence.
- Main gaps.
- Verdict if useful: `Go`, `No-Go`, `Pivot`, or `Needs More Research`.
- Lowest-cost validation experiment.
- Files or tracker artifacts created or updated.

## Validation

Before finishing, verify:

- Explicit target and riskiest assumption.
- Target confirmation or conversation-only choice.
- Confirmation for external research, deep analysis, tracker work, or parallel research.
- Explicit draft approval before saving, publishing, or commenting.
- Evidence classes are separated.
- Confidence is proportional to evidence.
- `Axis Coverage` is complete.
- Red flags are visible.
- Next experiment is actionable when uncertainty remains.
- Verdict is not overstated.
