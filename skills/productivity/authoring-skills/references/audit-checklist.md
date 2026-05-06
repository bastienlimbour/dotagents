# Audit Checklist

Use this reference for final review, quality checks, or audits of existing skills. Findings should be concrete and ordered by severity.

## Findings Format

For audits, report findings first:

```markdown
- Severity: `path:line` - Issue and impact. Suggested fix.
```

Then list open questions, residual risks, and optional improvements. Do not edit during an audit unless the user asks for changes.

## Frontmatter And Discovery

- `name` matches the directory.
- `name` is lowercase, hyphenated, portable, and specific.
- `description` is under 1024 characters.
- `description` says what the skill does and when to use it.
- Description front-loads important trigger terms.
- Near-miss exclusions are present when false triggers are likely.
- The skill does not trigger for unrelated prompts, docs, config, or adjacent skills.

## Scope And Value

- The skill covers one coherent repeatable job.
- It captures domain-specific expertise, workflow knowledge, gotchas, or project conventions the agent would not reliably know.
- It avoids generic best-practice filler.
- Inputs, outputs, non-goals, constraints, and success criteria are clear enough for the agent to act.
- The skill is not so narrow that several skills must always load together for one task.

## Body Quality

- The body is operational instruction, not tutorial prose.
- Workflow steps are ordered and actionable.
- The level of control matches task fragility.
- Defaults are clear and there are not too many equal options.
- Examples or templates exist where format or style matters.
- Gotchas cover likely mistakes and non-obvious facts.
- Verification steps exist for quality-critical work.

## Progressive Disclosure

- `SKILL.md` is concise and below 500 lines.
- Rare or long detail is moved to one-level references.
- Each bundled file is referenced from `SKILL.md` with a clear load condition.
- Important guidance is not hidden behind nested reference chains.
- Reference files over 100 lines have a short table of contents.
- Paths use forward slashes and are relative to the skill root.

## Scripts And Resources

- Scripts are justified by deterministic, repeated, fragile, or machine-verifiable work.
- Scripts are non-interactive and provide `--help`.
- Errors are helpful and outputs are structured when practical.
- Dependencies and runtime assumptions are documented.
- Assets and references are necessary and not dead weight.
- MCP or tool names are fully qualified when the target client requires it.

## Security

- Scripts and instructions do not access secrets or unrelated user data without explicit need.
- Network access, external downloads, and third-party content are disclosed and justified.
- Destructive operations require validation, dry run, confirmation, or clear user approval.
- Shell commands avoid unsafe interpolation of user-controlled input.
- Untrusted skill sources are audited before use.

## Evals And Iteration

- A lightweight eval plan exists, or there is a clear reason evals are unnecessary.
- Non-trivial skills include persistent eval artifacts.
- Trigger evals include both should-trigger and should-not-trigger near-misses.
- Output evals include realistic prompts, expected behavior, and assertions.
- Known failures from real usage have been folded back into the skill.

## Final Sanity Check

- The smallest correct change was made.
- The skill remains portable unless intentionally client-specific.
- Optional fields and bundled files are justified.
- The user-facing summary states what changed and how it was validated.
