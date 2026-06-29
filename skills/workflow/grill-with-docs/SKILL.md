---
name: grill-with-docs
description: Runs a "grill-me" session with "domain-modeling" support. Use when the user wants to stress-test a plan while checking project domain language, documentation contradictions, or durable decisions.
---

# Grill With Docs

Run `grill-me` as the primary workflow and invoke `domain-modeling` only when domain language, source-of-truth conflicts, or durable decisions materially affect the interview.

## Core Priority

`grill-me` is the authority. `domain-modeling` supports the interview; it must not take over the session.

## Workflow

### 1. Start with grill-me

Immediately follow the `grill-me` workflow: establish the target, build the material decision tree, ask exactly one question at a time, and wait for each answer.

### 2. Bring in domain-modeling when useful

Use `domain-modeling` when it can:

- Resolve or challenge a domain term.
- Prevent language drift against `CONTEXT.md` or `CONTEXT-MAP.md`.
- Surface a contradiction with docs, ADRs, code, tests, schemas, routes, APIs, or config.
- Clarify ownership across multiple contexts.
- Record a resolved domain term, relationship, ambiguity, avoided synonym, or durable architecture decision.

Keep all domain-modeling work inside the one-question-at-a-time rhythm. If domain-modeling produces a contradiction, ask the next single decision question needed to resolve it.

### 3. Return to grilling

After the domain-modeling branch is resolved, documented, deferred, or no longer material, return to the active `grill-me` branch unless the user asks to stop.

## Guardrails

- Do not let documentation discovery become a documentation audit.
- Do not stop grilling just because documentation could improve.
- If the user declines documentation updates, continue grilling without pressure.
