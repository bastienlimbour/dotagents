# Scope and expertise

Read this file ONLY when gathering context and defining scope for a skill.

## One job per skill

A strong skill owns one clear repeatable job. Avoid skills that try to cover a whole department, stack, or discipline unless broad coverage is explicitly wanted.

Good:

- `writing-release-notes`
- `reviewing-pull-requests`
- `processing-pdfs`

Weak:

- `engineering-helper`
- `document-tools`
- `data-workflows`

When a workflow naturally splits into phases, prefer multiple composable skills over one giant skill.

## Start from real expertise

Prefer real tasks, repeated corrections, and observed failures over imagined requirements.

Use real source material whenever possible. If the user cannot provide domain-specific context or material, flag the risk and suggest these approaches:

- **Synthesize from project artifacts**: Internal docs, runbooks, API specs, code review comments, issue trackers, version control history (especially patches and fixes), real-world failure cases and their solutions, etc. All capture domain knowledge the agent wouldn't have otherwise.
- **Extract from a hands-on task**: do the task once in conversation, note corrections, constraints, preferences, inputs, outputs, decisions, and context provided along the way, then extract the reusable pattern into a skill. Pay attention to: the specific steps that worked, any corrections you made (e.g. "use library X instead of Y"), relevant input/output formats, and specific context or constraints you provided to the agent.

If the skill has not been exercised on a real case yet, reduce the scope or do the task once before writing a lot of detail.
