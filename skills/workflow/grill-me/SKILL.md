---
name: grill-me
description: Stress-test a plan, idea, design, or decision through relentless one-question-at-a-time interviewing until shared understanding is reached. Use when the user asks to be grilled, challenged, stress-tested, or when important assumptions and decision branches remain unresolved.
---
# Grill Me

## Overview

Interview the user rigorously about every aspect of a plan, idea, design, or decision until a shared understanding is reached and important assumptions, tradeoffs, risks, and downstream consequences are explicit.

## When To Use

- The user asks to be grilled, challenged, stress-tested, pushed, or interrogated about a plan.
- A design, product idea, technical approach, or decision contains unclear assumptions or hidden dependencies.
- A high-impact or hard-to-reverse decision should be examined before it becomes a spec, task, artifact, or implementation.

Do not use this skill for simple Q&A, code implementation, ordinary code review, or simple documentation updates.

## Workflow

1. Establish the target: identify the plan, idea, design, or decision being tested. If the target is unclear, ask one clarifying question first.
2. Use available evidence before asking. If codebase, documentation, issues, specs, briefs, ADRs, or notes can answer a question, inspect them instead of making the user restate known facts.
3. Build a decision tree of the material branches to test: intent, scope, non-goals, constraints, alternatives, assumptions, dependencies, failure modes, reversibility, rollout, ownership, and downstream impact.
4. Ask exactly one question at a time. Wait for the user's answer before continuing.
5. For each question, provide your recommended answer or default, clearly separated from the question.
6. When an answer is vague, provisional, contradictory, or overloaded, stay on that branch and dig deeper before moving on.
7. Challenge hidden tradeoffs, unexamined alternatives, contradictions with existing sources of truth, optimistic assumptions, and decisions that would be expensive to reverse.
8. Briefly summarize a branch once it is resolved, then continue to the next material branch.
9. Stop only when you reach a shared understanding with the user and the critical branches are answered, explicitly deferred, or no longer material to the user's goal.

## Rules

- Use code or documentation evidence when it can answer a question.
- Handle dependent decisions in a coherent order.
- Keep recommendations advisory. The user decides.
- Do not batch questions. Context, options, and a recommendation are allowed, but ask only one decision question per turn.
- Do not accept "we will figure it out later" unless the uncertainty is low-risk or the user explicitly chooses to defer it.
- Do not create files, publish issues, update docs, comment on trackers, or implement code during the grilling session unless the user explicitly asks or confirms a proposed capture.

## Output

Default output is the conversation itself: one question, options if relevant, recommendation, answer, and follow-up at a time.

## Validation

Before finishing, verify:

- [ ] Critical branches were answered or explicitly deferred.
- [ ] Important assumptions, alternatives, risks, and failure modes were surfaced.
- [ ] The user agrees that the shared understanding is sufficient to proceed, or remaining open questions are clearly listed.
