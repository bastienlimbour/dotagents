---
name: grill-me
description: Interview the user relentlessly about a plan or design until reaching shared understanding, resolving each branch of the decision tree. Use when decisions contain unclear assumptions, hidden dependencies, or when user wants to stress-test a plan, get grilled on their design, or mentions "grill me".
---

## Overview

Relentlessly interview the user about every aspect of their plan, idea, or design until a shared understanding is reached. Walk down each branch of the design tree, resolving dependencies between decisions one-by-one.

## Workflow

1. Establish the target: identify the plan, idea or design being tested. If the target is unclear, ask one clarifying question first.
2. Use available evidence before asking. If codebase, documentation, issues, specs, briefs, ADRs, or notes can answer a question, inspect them instead of making the user restate known facts.
3. Build a decision tree of the material branches to test: intent, scope, non-goals, constraints, alternatives, assumptions, dependencies, failure modes, reversibility, rollout, ownership, and downstream impact.
4. Ask exactly one question at a time. Wait for the user's answer before continuing.
5. For each question, suggest multiple options and provide your recommended answer.
6. When an answer is vague, provisional, contradictory, or overloaded, stay on that branch and dig deeper before moving on.
7. Challenge hidden tradeoffs, unexamined alternatives, contradictions with existing sources of truth, optimistic assumptions, and decisions that would be expensive to reverse.
8. Briefly summarize a branch once it is resolved, then continue to the next material branch.
9. Stop only when you reach a shared understanding and a full alignment with the user and when all critical branches are answered, explicitly deferred, or no longer material to the user's goal.

## Rules

- Use code or documentation evidence when it can answer a question.
- Handle dependent decisions in a coherent order.
- Keep recommendations advisory. The user decides.
- Do not batch questions. Context, options, and a recommendation are allowed, but ask only one decision question per turn.

## Validation

Before finishing, verify:

- [ ] Critical branches were answered or explicitly deferred.
- [ ] Important assumptions, alternatives, risks, and failure modes were surfaced.
- [ ] The user agrees that the shared understanding is sufficient to proceed.
