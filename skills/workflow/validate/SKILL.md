---
name: validate
description: Reduces uncertainty around a product, technical, market, or business hypothesis through evidence, risks, confidence, red flags, and next validation experiments. Use when the user needs confidence before investing in a feature, solution, market direction, or implementation; not for specs, task splitting, prototyping, or implementing code.
---

# Validate

## Overview

Validate an idea, solution, feature, technical direction, market bet, or business hypothesis before deeper investment. The job is to make evidence, uncertainty, risks, confidence, and the cheapest useful next test explicit without deciding for the user.

## When To Use

- The user asks to validate, de-risk, assess confidence in, or sanity-check a product, technical, market, cost, legal, UX, distribution, or business hypothesis.
- A brief, brainstorming note, research note, issue, spec draft, conversation, codebase, or documentation needs to be turned into a validation report.
- The next useful step depends on whether evidence supports `Go`, `No-Go`, `Pivot`, or `Needs More Research`.

Do not use this skill for broad brainstorming, writing a product brief, creating a spec, splitting tasks, prototyping, implementing code, ordinary Q&A, or research that is not tied to a specific validation target.

## Core Principle

Evidence over optimism. Prefer real behavior, commitments, observable workarounds, repo/docs facts, and cited sources over opinions, analogies, assumptions, or polite interest.

## Workflow

### 1. Resolve Validation Report Target

Resolve the initiative and `validation.md` artifact before writing. Use this step only to identify create/update/conversation-only mode and the report target; collect substantive evidence in later steps.

- Start from any user-provided initiative, artifact path, issue, brief, or existing validation report.
- If the user is updating an existing validation report, inspect that artifact before drafting and preserve useful content.
- If nothing matches, propose a new initiative and `.initiatives/<id>/validation.md`, unless the project conventions use a different local artifact path.
- Use `docs/research/<slug>.md` only when the validation is reusable beyond the current initiative or affects the project broadly.
- If validation must be attached to an issue tracker, respect the project's tracker conventions; use GitHub Issues via `gh` by default when GitHub is the chosen tracker.
- Ask for confirmation before creating an initiative, selecting an artifact path, publishing, or commenting. This target confirmation does not approve the report content.

If the user explicitly declines an artifact, provide the report in conversation only.

### 2. Establish The Validation Question

Read the current conversation and provided artifacts enough to identify what is being validated.

Extract or clarify:

- Problem.
- Target user or segment.
- Current workaround, alternative, competitor, manual process, or status quo.
- Proposed solution, feature, direction, or hypothesis.
- Riskiest assumption: the assumption that would most weaken or invalidate the idea if false.

Ask one targeted question at a time only when missing or conflicting information would materially change the validation design.

### 3. Choose Scope And Depth

Select the relevant validation axes. The report must list every canonical axis in `Axis Coverage`, but detailed findings are needed only for axes that are `Covered` or `Partial`.

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

State the intended depth in plain language, such as lightweight, focused, or deeper analysis. Do not turn these into formal workflow modes.

Ask for confirmation before external research, deep analysis, or parallel research by axis. Use sub-agents and parallel research if axes are independent enough to benefit from separation, then condense everything into one validation report.

### 4. Gather And Classify Evidence

Use available sources before guessing or asking. If validation is technical, inspect relevant code, tests, docs, ADRs, issues, schemas, routes, configuration, or existing behavior before asking the user. Cite important sources when available.

Classify material explicitly:

- Facts: verified observations, source-backed claims, repo/docs evidence, measurements, or direct user behavior.
- Hypotheses: plausible but unproven beliefs.
- Weak signals: interest, analogies, indirect evidence, or partial observations.
- Interpretations: what the evidence suggests and what would change the conclusion.
- Unknowns: missing evidence that could materially affect the verdict.

Rank evidence strength from strongest to weakest:

1. Payment, contract, preorder, repeated usage, or committed design partner.
2. Direct conversations about current behavior, pains, budgets, and workarounds.
3. Observable behavior such as reviews, forums, search patterns, public complaints, job postings, or visible workarounds.
4. Market data, benchmarks, competitors, repo/docs observations, or verifiable external sources.
5. Founder claims, analogies, unsupported assumptions, opinions, or polite interest.

### 5. Analyze Confidence And Risks

For each covered or partially covered axis, state the finding, evidence, interpretation, confidence, risks or unknowns, and next signal to seek.

Use `High`, `Medium`, or `Low` confidence. Keep confidence proportional to evidence quality. Red flags should cap confidence even when the story sounds attractive.

Common red flags:

- Target user is vague.
- Problem is not painful, frequent, recognized, or costly enough.
- No current workaround, budget, time cost, or alternative is identifiable.
- Differentiation is marginal versus direct alternatives, indirect alternatives, or the status quo.
- Adoption requires a major workflow change without a clearly superior benefit.
- Business model or unit economics appear weak.
- Legal, regulatory, ethical, privacy, or security risk is material.
- Core technical feasibility is unproven.
- Validation relies mostly on friendly opinions or polite interest.

### 6. Draft And Save The Report

Use `assets/templates/validation.md` for new reports and as a structural guide for updates. Replace all placeholders with concrete content; use `Not known yet` when evidence is missing.

Show the draft in conversation and wait for explicit content approval before saving, publishing, or commenting. Do not publish, comment, or create tracker artifacts without explicit confirmation. If the user declined an artifact, deliver the report in conversation only.

## Guardrails

- Do not decide for the user. A verdict is a recommendation, not a final product decision.
- Do not present a verdict as certainty.
- Do not recommend moving to spec or implementation when evidence is weak; use `Needs More Research` and propose the next test.
- Do not update product briefs, specs, tasks, issues, ADRs, or global documentation unless the user explicitly asks and confirms the target action.
- Do not create separate research files per axis by default; condense validation into one report.
- Do not impose Lean Canvas, SWOT, PESTLE, weighted scoring, mandatory interviews, triage labels, autonomous loops, or unsupported trackers in v1.
- Do not store secrets, credentials, raw personal data, sensitive customer exports, or confidential material that should not be visible to someone with repo access.

## Output

End with a concise summary containing:

- Validation target and riskiest assumption.
- Sources or evidence used.
- Strongest evidence, weakest evidence, and main gaps.
- Verdict when useful: `Go`, `No-Go`, `Pivot`, or `Needs More Research`.
- Recommended lowest-cost validation experiment.
- Files or tracker artifacts created or updated, if any.

## Validation

Before finishing, verify:

- [ ] The validation target and riskiest assumption are explicit.
- [ ] The validation report target was confirmed or explicitly declined before writing or publishing.
- [ ] Repo/docs evidence was inspected before asking the user when the repo could answer.
- [ ] External research, deep analysis, artifact writing, or tracker publishing was confirmed before it happened.
- [ ] A report draft was shown and explicitly approved before saving, publishing, or commenting.
- [ ] Facts, hypotheses, weak signals, interpretations, and unknowns are not blurred together.
- [ ] Evidence quality is summarized and confidence is proportional to the evidence.
- [ ] `Axis Coverage` includes every canonical axis with `Covered`, `Partial`, or `Not covered`.
- [ ] Detailed findings exist only for axes marked `Covered` or `Partial`.
- [ ] Red flags are visible and reflected in the verdict.
- [ ] At least one actionable validation experiment is proposed when uncertainty remains material.
- [ ] The verdict, if provided, is one of `Go`, `No-Go`, `Pivot`, or `Needs More Research` and does not overstate certainty.
