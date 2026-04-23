# Scope and expertise

Use this guide when gathering context and defining scope for a new or modified skill (Step 1).

## One job per skill

A strong skill owns one clear repeatable job. Do not use a single skill to cover an entire department, stack, or discipline unless the user explicitly wants a broad package and accepts weaker triggering.

**Good scope**: `writing-release-notes`, `reviewing-pull-requests`, `processing-pdfs`
**Weak scope**: `engineering-helper`, `document-tools`, `data-workflows`

When a workflow naturally splits into phases, prefer multiple composable skills over one giant skill.

## Start from real expertise

Effective skills are grounded in real expertise. The key is feeding domain-specific context into the creation process. When gathering requirements, push for real source material:

- **Extract from a hands-on task**: Complete the task in conversation first, noting corrections, preferences, and context provided along the way, then extract the reusable pattern into a skill. Pay attention to: the specific steps that worked, any corrections you made (e.g. "use library X instead of Y"), relevant input/output formats, and specific context or constraints you provided to the agent.
- **Synthesize from project artifacts**: Internal docs, runbooks, API specs, code review comments, issue trackers, version control history (especially patches and fixes), real-world failure cases and their solutions, etc. All capture domain knowledge the agent wouldn't have otherwise.

If the user cannot provide domain-specific context, the resulting skill will likely be vague and low-value. Flag this early and propose alternatives (co-perform the task once to extract a pattern, narrow the scope, or use existing artifacts).
