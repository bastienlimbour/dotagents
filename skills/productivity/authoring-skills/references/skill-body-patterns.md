# Skill body patterns

Read this file ONLY when shaping the body of a skill.

## Contents

- [Choose the lightest body shape that works](#choose-the-lightest-body-shape-that-works)
- [Common sections](#common-sections)
- [Writing rules](#writing-rules)
- [Concision rules](#concision-rules)
- [Workflow patterns](#workflow-patterns)
- [High-value content patterns](#high-value-content-patterns)
- [Calibrate control](#calibrate-control)
- [Content hygiene](#content-hygiene)

## Core rule

The body is a prompt. Tell the agent what to do next. Do not explain the topic at length.

## Choose the lightest body shape that works

- **Simple instructions**: a narrow task that fits in a few direct commands
- **Workflow-based**: a multi-step process
- **Task-based**: a tool collection or grouped capabilities
- **Reference-based**: the task depends on standards, schemas, or domain knowledge

## Common sections

Use only the sections that help the agent act:

- `Overview`: one or two lines on the job and goal
- `When to Use`: triggers and exclusions
- `Quick Start`: fastest path to value
- `Process`, `Workflow`, or `Steps`: the main process
- `[Specific task / use case]`: a sub-workflow for one scenario
- `Rules`: defaults, constraints, exceptions
- `Output`: artifact, response shape, schema, or target length
- `Troubleshooting` or `Gotchas`: common failures and fixes
- `Verification` or `Validation`: how to prove the result is correct

## Writing rules

- Use imperative instructions
- Lead with the default path, not a menu of options
- Prefer reusable procedures over single-instance answers
- Aim for moderate detail: enough to guide, not enough to drown the task
- Keep examples short and concrete

## Concision rules

- Add only context the agent is unlikely to already know

For each piece of context, ask yourself:

- Does this earn its token cost?
- Would removing this change the agent's behavior?

## Workflow patterns

### Sequential workflow

Use ordered steps when the work must happen in sequence:

````markdown
## Workflow

1. Analyze the input
2. Produce a draft
3. Validate the draft
4. Fix issues and repeat until validation passes
````

### Feedback loop

For quality-sensitive work, use this pattern:

1. do the work
2. run validation
3. fix issues
4. repeat until validation passes

For long or fragile workflows, give the agent a copyable checklist:

````markdown
## Workflow

Copy this checklist and update it as you go:

- [ ] Analyze input
- [ ] Draft output
- [ ] Validate
- [ ] Fix issues
````

### Conditional workflow

Use a decision point when the path changes materially:

````markdown
1. Determine the task type:
   - New document -> follow creation workflow
   - Existing document -> follow editing workflow
````

## High-value content patterns

### Gotchas

Add only facts that correct likely mistakes:

```markdown
## Gotchas

- The `users` table uses soft deletes. Filter on `deleted_at IS NULL`.
- The health endpoint is shallow. Use `/ready` for full service checks.
```

### Templates

Use templates when output shape matters. Keep short ones inline. Move longer or optional ones to `assets/`.

- Use a strict template when format is non-negotiable
- Use a flexible template when adaptation is useful

### Examples

Use input/output examples only when they improve formatting, style, or judgment. Do not add examples that just restate obvious instructions.

### Default path with escape hatch

Give one default path. Add one explicit fallback only when it solves a real edge case.

```markdown
Use `pdfplumber` by default.
For scanned PDFs, use `OCR` instead.
```

### Old patterns

Keep legacy guidance in a separate section instead of writing time-sensitive instructions inline.

```markdown
## Current method

Use the v2 API.

## Old patterns

The v1 API is deprecated and should only be referenced for migration work.
```

## Calibrate control

### High freedom

Use when multiple approaches are valid and context decides the best path:

```markdown
1. Check boundary validation
2. Review auth checks
3. Confirm errors do not leak internals
```

### Medium freedom

Use when a preferred pattern exists but some variation is acceptable:

```markdown
Use this template and adapt sections as needed for the task.
```

### Low freedom

Use when the work is fragile, exact, or safety-critical:

```markdown
Run exactly this command:

`python scripts/migrate.py --verify --backup`
```

Do not over-constrain exploratory work, and do not under-specify dangerous work.

## Content hygiene

- Use one term consistently for the same concept
- Avoid time-sensitive wording when a durable description will do
- Do not duplicate the same instruction in multiple files
- Use forward slashes in paths
- Keep examples and templates short unless detail is essential
