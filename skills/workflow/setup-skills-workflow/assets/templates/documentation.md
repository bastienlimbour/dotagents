# Documentation

How the workflow skills should consume this repo's documentation when exploring the codebase or working on a task.

## Before exploring or working on a task

- **If the domain language matters for the task at hand**: read relevant `CONTEXT.md` or `CONTEXT-MAP.md` at the repo root.
- **If some ADRs (in `docs/adr/` at the repo root or in any `**/docs/adr/` in the codebase) touch the area you're about to work on**: read them.

If any of these files don't exist, **proceed silently**. Don't flag their absence.

## Domain Context

`CONTEXT.md` is a glossary for canonical domain language only: approved terms, terms to avoid, domain relationships, examples, and resolved ambiguities.

When your output names a domain concept (issue title, generated code, refactor proposal, hypothesis, test name, or any other output), use the term as defined in `CONTEXT.md`. Don't drift to synonyms or terms the glossary explicitly avoids.

If the concept you need isn't in the glossary yet, that's a signal, either you're inventing language the project doesn't use (reconsider) or there's a real gap (flag it to the user).

## Context Map

`CONTEXT-MAP.md` is a routing document that points to the relevant `CONTEXT.md` when the repo has multiple domains, packages, apps, bounded contexts, or sub-projects. It's not an architecture map.

## ADRs

`docs/adr/` is a directory for durable architecture decisions (hard to reverse, surprising without context, and involves a real tradeoff between options).

If your output or a proposed change contradicts an existing ADR, flag the conflict explicitly to the user instead of silently overriding the decision.

## File Structure

Single domain context (most repos):

```text
/
├── CONTEXT.md
├── docs/adr/
│   ├── 0001-decision-short-slug.md
│   └── 0002-decision-short-slug.md
└── src/
```

Multi-domain context (presence of `CONTEXT-MAP.md` at the repo root):

```text
/
├── CONTEXT-MAP.md
├── docs/adr/             # system-wide decisions
└── src/
    ├── billing/
    │   ├── CONTEXT.md
    │   └── docs/adr/     # context-specific decisions
    └── customers/
        ├── CONTEXT.md
        └── docs/adr/
```

## Security And Privacy

NEVER include secrets, tokens, credentials, raw personal data, sensitive customer data, or confidential material in project documentation.
