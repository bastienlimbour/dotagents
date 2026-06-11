---
name: grill-with-docs
description: Runs a grill-me session with project documentation awareness. Use when the user wants to stress-test a plan or design while checking domain language, CONTEXT.md, CONTEXT-MAP.md, docs/agents/documentation.md, or ADRs only as secondary support.
---

# Grill With Docs

## Overview

Run the `grill-me` skill as the primary workflow, with documentation awareness layered in only when needed. The job is to reach shared understanding first; documentation updates are secondary and happen only after useful domain language or durable decisions crystallize.

## Core Priority

`grill-me` is the authority. Documentation work supports the interview; it must not take over the session.

## Workflow

### 1. Start The Grilling Session

When this skill is activated, immediately load or invoke `grill-me` skill and follow it as the primary workflow.

- Identify the plan, idea, or design being tested.
- If the target is unclear, ask one clarifying question before exploring documentation.
- Build the decision tree using `grill-me` branches.
- Ask exactly one question at a time and wait for the user's answer.

### 2. Inspect Documentation Only When Useful

Use documentation as evidence when it can answer a question, reveal a contradiction, or prevent language drift.

Prefer these sources when present:

- `docs/agents/documentation.md` for the project's documentation conventions.
- Root `CONTEXT-MAP.md` when multiple domains, packages, apps, bounded contexts, or sub-projects may exist.
- The relevant `CONTEXT.md` for canonical terms, terms to avoid, domain relationships, examples, and resolved ambiguities.
- `docs/decisions/` at the repo root or relevant `**/docs/decisions/` directories for durable decisions.
- Nearby README files, domain docs, code, tests, schemas, routes, APIs, or configuration when they can answer factual questions.

If these files do not exist, proceed silently. Do not treat their absence as a setup problem during grilling.

### 3. Use Domain Language As Interview Evidence

During the interview:

- If the user uses a term that conflicts with `CONTEXT.md`, call out the conflict immediately and ask which meaning should win.
- If a term is vague, overloaded, or absent from the glossary but material to the plan, propose a precise canonical term and ask whether it is correct.
- If domain relationships are unclear, stress-test them with concrete scenarios and edge cases. Invent scenarios that probe edge cases and force the user to be precise about the boundaries between concepts.
- If code or docs contradict the user's claim, surface the contradiction before continuing.
- If an existing ADR constrains or contradicts the plan, name the conflict and ask before assuming the ADR should change.

Keep this inside the one-question-at-a-time rhythm. A contradiction can be the next question; it is not a reason to batch a documentation review.

### 4. Capture Documentation Updates Sparingly

Only consider documentation updates after a branch is resolved or a contradiction makes the next grilling question depend on a documented source of truth.

| Situation | Default action |
| --- | --- |
| A domain term, avoided synonym, relationship, example, or ambiguity is resolved | Offer to update the relevant `CONTEXT.md` |
| The repo has `CONTEXT-MAP.md` and the relevant context is clear | Update only that context's `CONTEXT.md` |
| Multiple contexts may be affected and routing is unclear | Ask which context owns the term before proposing edits |
| No `CONTEXT.md` exists and a real domain term has been resolved | Offer to create the smallest useful `CONTEXT.md` |
| A durable architecture decision is hard to reverse, surprising without context, and the result of a real trade-off | Offer to create or update an ADR |
| The session produced broad useful notes but no canonical glossary or ADR change | Suggest `capture` instead of writing global docs |

Before writing any documentation, show the exact proposed path and concise content change, then wait for explicit confirmation. Do not create empty, speculative, or placeholder documentation.

Create files lazily — only when you have something to write. If no `CONTEXT.md` exists, create one when the first term is resolved. If no `docs/decisions/` exists, create it when the first ADR is needed.

### 5. Write Documentation Safely When Confirmed

When the user confirms a documentation update:

- Keep `CONTEXT.md` focused on canonical domain language only: approved terms, terms to avoid, domain relationships, examples, and resolved ambiguities.
- Do not put implementation details, specs, task lists, open brainstorming, status updates, or architecture decisions in `CONTEXT.md`.
- Use the project's existing `CONTEXT.md` structure if present; otherwise use the workflow template shape: `Canonical Terms`, `Terms To Avoid`, `Domain Relationships`, `Examples`, and `Resolved Ambiguities`.
- Put ADRs in the relevant `docs/decisions/` directory using the project's existing style if present.
- For new ADRs, use the next sequential `NNNN-short-slug.md` filename when the directory already follows that convention.
- Keep ADRs short unless alternatives or consequences are genuinely useful to future readers.
- Never include secrets, credentials, raw personal data, sensitive customer data, or confidential material in documentation.

After the write, return to the active grilling branch unless the user asks to stop.

## Guardrails

- Do not let documentation discovery become a general documentation audit.
- Do not stop grilling just because documentation could be improved.
- Do not batch multiple interview questions behind a documentation summary.
- Do not update docs merely because a term was mentioned; update only when a meaning is resolved and useful as future source of truth.
- Do not create or update product briefs, specs, task issues, local initiative artifacts, or capture notes from this skill unless the user explicitly invokes the relevant workflow.
- If the user declines documentation updates, continue the grilling session without pressure.

## Output

During the session:

- Ask one decision question at a time.
- Include relevant evidence, options, and your recommended answer with each question.
- Surface contradictions with `CONTEXT.md`, ADRs, docs, or code as soon as they matter.
- Propose documentation updates only when they are secondary to a resolved grilling branch.

When ending the session, summarize:

- Critical branches resolved, deferred, or still open.
- Domain terms or ambiguities clarified.
- Documentation files created or updated, if any.
- ADRs created or suggested, if any.
- Remaining contradictions or source-of-truth gaps.

## Validation

Before finishing, verify:

- [ ] `grill-me` was loaded or its workflow was followed as the primary process.
- [ ] Exactly one grilling question was asked per turn.
- [ ] Documentation lookup answered questions or surfaced contradictions instead of replacing the interview.
- [ ] Existing `docs/agents/documentation.md`, `CONTEXT-MAP.md`, `CONTEXT.md`, and ADR conventions were respected when present.
- [ ] No documentation was created empty, speculatively, or without explicit confirmation.
- [ ] `CONTEXT.md` updates stayed focused on domain language, not implementation or planning.
- [ ] ADRs were offered only for hard-to-reverse, surprising, trade-off-based decisions.
- [ ] No secrets, credentials, sensitive data, unrelated artifacts, specs, briefs, tasks, or broad docs audits were introduced.
