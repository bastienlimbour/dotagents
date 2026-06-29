---
name: grill-me
description: Interview the user about a plan or design. Use when the user wants to stress-test a plan or uses any "grill-me" trigger phrases.
---

# Grill Me

Relentlessly interview the user about every aspect of their plan, idea, or design until shared understanding is reached. Walk down each branch of the design tree, resolving dependencies between decisions one-by-one.

## Workflow

1. Establish the target. If unclear, ask one clarifying question first.
2. Use available evidence before asking a question. Inspect codebase, docs, issues, specs, briefs, ADRs, or notes when they can answer.
3. Build the material decision tree: intent, scope, non-goals, constraints, alternatives, assumptions, dependencies, failure modes, reversibility, rollout, ownership, and downstream impact.
4. Ask exactly one question at a time and wait for the answer.
5. For each question, offer options and your recommended answer.
6. If an answer is vague, provisional, contradictory, or overloaded, stay on that branch and dig deeper.
7. Challenge hidden tradeoffs, unexamined alternatives, source-of-truth contradictions, optimistic assumptions, and hard-to-reverse decisions.
8. Summarize resolved branches briefly, then continue.
9. Stop only when all critical branches are answered, explicitly deferred, or no longer material, and the user agrees understanding is sufficient.

## Rules

- Handle dependent decisions in a coherent order.
- Keep recommendations advisory. The user decides.
- Do not batch questions. Context, options, and a recommendation are allowed, but ask only one decision question per turn.

## Validation

Before finishing, verify:

- Critical branches were answered or explicitly deferred.
- Important assumptions, alternatives, risks, and failure modes were surfaced.
- The user agrees the understanding is sufficient to proceed.
