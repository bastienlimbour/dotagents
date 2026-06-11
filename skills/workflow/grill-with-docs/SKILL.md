---
name: grill-with-docs
description: Runs a grill-me session with project documentation awareness. Use when the user wants to stress-test a plan or design while checking domain language, CONTEXT.md, CONTEXT-MAP.md, docs/agents/documentation.md, or ADRs only as secondary support.
---

# Grill With Docs

## Overview

Run the `grill-me` skill as the primary workflow with documentation awareness layered in only when useful. The job is shared understanding first; documentation updates are secondary and only follow resolved language or durable decisions.

## Core Priority

`grill-me` is the authority. Documentation supports the interview; it must not take over the session.

## Workflow

### 1. Start Grilling

Immediately follow the `grill-me` workflow: identify the target, build the decision tree, ask exactly one question at a time, and wait for each answer.

### 2. Use Documentation As Evidence

Inspect documentation only when it can answer a question, reveal a contradiction, or prevent language drift.

Prefer these sources when present:

- `docs/agents/documentation.md`.
- Root `CONTEXT-MAP.md`.
- Relevant `CONTEXT.md`.
- Root or contextual `docs/decisions/`.
- Nearby README/domain docs, code, tests, schemas, routes, APIs, or config.

If these files do not exist, proceed silently.

During the interview:

- Call out conflicts with `CONTEXT.md`, ADRs, docs, or code as soon as they matter.
- If a term is vague, overloaded, or absent from the glossary but material, propose a precise term and ask whether it is correct.
- Stress-test unclear domain relationships with concrete scenarios and edge cases.
- Keep contradictions inside the one-question-at-a-time rhythm.

### 3. Offer Documentation Updates Sparingly

Only consider updates after a branch is resolved or a contradiction blocks the next question.

| Situation | Default action |
| --- | --- |
| Domain term, avoided synonym, relationship, example, or ambiguity is resolved | Offer to update the relevant `CONTEXT.md` |
| Multiple contexts may be affected | Ask which context owns the term |
| No `CONTEXT.md` exists and a real domain term is resolved | Offer the smallest useful `CONTEXT.md` |
| Decision is hard to reverse, surprising without context, and trade-off based | Offer an ADR |
| Useful notes are broad but not canonical glossary or ADR material | Suggest `capture` |

Before writing documentation, show the exact path and concise content change, then wait for explicit confirmation. Create files lazily; never create empty, speculative, or placeholder docs.

### 4. Write Safely When Confirmed

- Keep `CONTEXT.md` focused on canonical domain language: approved terms, terms to avoid, relationships, examples, and resolved ambiguities.
- Do not put implementation details, specs, task lists, brainstorming, status, or architecture decisions in `CONTEXT.md`.
- Use existing structure when present; otherwise use `Canonical Terms`, `Terms To Avoid`, `Domain Relationships`, `Examples`, and `Resolved Ambiguities`.
- Put ADRs in the relevant `docs/decisions/` using existing style; for new numbered ADR directories, use the next `NNNN-short-slug.md`.
- Keep ADRs short unless alternatives or consequences are useful to future readers.
- Do not include secrets, credentials, raw personal data, sensitive customer data, or confidential material.

After writing, return to the active grilling branch unless the user asks to stop.

## Guardrails

- Do not let documentation discovery become a documentation audit.
- Do not stop grilling just because documentation could improve.
- Do not update docs merely because a term was mentioned; update only when the meaning is resolved and useful as future source of truth.
- Do not create product briefs, specs, task issues, local initiative artifacts, or capture notes unless the user explicitly invokes that workflow.
- If the user declines documentation updates, continue grilling without pressure.

## Output

During the session, ask one decision question at a time with relevant evidence, options, and a recommendation.

End with:

- Resolved, deferred, or still-open branches.
- Clarified domain terms.
- Docs or ADRs created or suggested.
- Remaining contradictions or source-of-truth gaps.

## Validation

Before finishing, verify:

- `grill-me` stayed primary.
- Docs answered questions or surfaced contradictions instead of replacing the interview.
- Existing documentation conventions were respected.
- No docs were created without confirmation.
- `CONTEXT.md` stayed domain-language-only.
- ADRs met the durability criteria.
- No unrelated artifacts or sensitive data were introduced.
