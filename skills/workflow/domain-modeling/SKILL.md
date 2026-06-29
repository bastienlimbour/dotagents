---
name: domain-modeling
description: Build and sharpen the project's domain model. Use when the user wants to pin down domain terminology or a ubiquitous language, record an architectural decision, or when another skill needs to maintain the domain model.
---

# Domain Modeling

Actively build and sharpen the project's domain model as you design. This is the active discipline: challenging terms, inventing edge-case scenarios, resolving source-of-truth conflicts, and recording canonical language or durable decisions when they crystallize.

Merely reading `CONTEXT.md` for vocabulary is not this skill. This skill is for updating and maintaining the model, not just consuming it.

When invoked by another skill, domain modeling supports that caller workflow. Do not take over the session; resolve the domain-modeling need, then return control to the caller.

## File structure

Single-context repo (most repos):

```
/
├── CONTEXT.md
├── docs/decisions/
│   ├── 0001-decision-short-slug.md
│   ├── 0002-event-sourced-orders.md
│   └── 0003-postgres-for-write-model.md
└── src/
```

If a `CONTEXT-MAP.md` exists at the root, the repo has multiple contexts. The map points to where each context lives:

```
/
├── CONTEXT-MAP.md
├── docs/decisions/             # system-wide decisions
└── src/
    ├── billing/
    │   ├── CONTEXT.md
    │   └── docs/decisions/     # context-specific decisions
    └── customers/
        ├── CONTEXT.md
        └── docs/decisions/
```

Create files lazily, only when you have something to write. Never create empty, speculative, or placeholder docs. If no `CONTEXT.md` exists, create the smallest useful one when the first term is resolved. If no `docs/decisions/` exists, create it when the first ADR is needed.

## During the session

### Challenge against the glossary

When the user uses a term that conflicts with the existing language in `CONTEXT.md`, call it out immediately: "The glossary defines 'cancellation' as X, but you seem to mean Y - which is it?"

Also call out conflicts with ADRs or docs as soon as they matter.

### Sharpen fuzzy language

When the user uses vague, absent, inconsistent, or overloaded terms, propose a precise canonical term: "You're saying 'account' - do you mean the Customer or the User? Those are different things."

### Discuss concrete scenarios

When domain relationships are being discussed, stress-test them with specific scenarios: Invent scenarios that probe edge cases and force the user to be precise about the boundaries between concepts.

### Cross-reference with code

When the user states how something works, check whether the code agrees. If you find a contradiction, surface it: "Your code cancels entire Orders, but you just said partial cancellation is possible - which is right?"

### Update CONTEXT.md when language resolves

If a domain term, avoided synonym, relationship, example, or ambiguity is resolved, update the relevant `CONTEXT.md` right there, close to the moment it resolves.

Don't batch many unrelated terms if that would lose precision, capture them as they happen. Follow the format in [context-format.md](./references/context-format.md).

Do not update docs merely because a term was mentioned. Update only when the meaning is resolved and useful as a future source of truth.

### Offer ADRs sparingly

When an architectural decision is made, offer to create an ADR.

Only offer to create an ADR when all three criteria are met:

1. **Hard to reverse** - the cost of changing your mind later is meaningful
2. **Surprising without context** - a future reader will wonder "why did they do it this way?"
3. **The result of a real trade-off** - there were genuine alternatives and you picked one for specific reasons

If any of the three is missing, skip the ADR.

Use the format in [adr-format.md](./references/adr-format.md).

Put ADRs in the relevant `docs/decisions/` using existing style. For new numbered ADR files, use the next `NNNN-short-slug.md`. Keep ADRs short unless alternatives or consequences are useful to future readers.

## Guardrails

- Do not let this skill take over the session; resolve the domain-modeling need, then return control to the caller.
- Do not include sensitive information like secrets, tokens, credentials, raw personal data, sensitive customer data, or confidential material.

## Return To Source Task

When this skill is used inside another task or skill, return to the source task after the domain-modeling action is handled.
