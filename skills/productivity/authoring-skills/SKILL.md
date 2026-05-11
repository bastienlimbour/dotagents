---
name: authoring-skills
description: Creates, updates, improves, and audits Agent Skills. Use when the task directly involves creating or updating an agent skill, SKILL.md, skill description, skill directory, skill bundled files, or skill evals. Do not use for standalone prompts or if the current task is not directly related to authoring agent skills.
---

# Authoring Skills

## Overview

Create, update, improve, and audit portable Agent Skills. The goal is to make agents reliably better at a repeatable job without bloating context or forcing unnecessary structure.

## When To Use

- Creating a new Agent Skill or `SKILL.md`
- Updating, refactoring, or improving an existing skill
- Designing a skill's name, description, trigger surface, or exclusions
- Organizing bundled skill files such as `references/`, `assets/`, `scripts/`, or `evals/`
- Auditing a skill for structure, discovery, progressive disclosure, scripts, security, or eval coverage

**When NOT to use:**

- Standalone prompts that are not being packaged as Agent Skills
- `AGENTS.md`, hooks, MCP setup, app config, or other non-skill agent configuration
- General documentation, READMEs, or writing tasks unrelated to skill authoring

If the user explicitly wants one of these artifacts packaged as a skill, use this skill for the packaging work.

## Core Principle

Write the simplest and smallest skill that does the job. Add structure, examples, references, assets, scripts, or evals only when they improve the output quality or make the skill easier to discover, follow, verify, or maintain.

## Workflow

For non-trivial work, track your progress with a checklist.

### Phase 1 - Classify

Determine the path before editing:

- Creating a skill: run the full workflow.
- Updating a skill: inspect the existing skill and edit only the parts needed for the requested change.
- Improving a skill with vague goals: audit first, then fix the highest-value gaps.
- Auditing a skill: report findings first and stop unless the user asks for edits.

### Phase 2 - Gather Evidence

Inspect existing skill files, source material, real workflows, examples, previous failures, and adjacent skills when available.

Ask one targeted question at a time only when missing information would materially change the skill. For substantial new skills or major rewrites, summarize the intended files and ask to proceed unless the user already approved that exact work.

### Phase 3 - Define The Boundary

Identify the repeatable job, users, inputs, outputs, constraints, non-goals, success criteria, and near-miss tasks that should not trigger the skill.

Prefer one coherent job over a broad toolbox. If the proposed skill covers unrelated jobs, split it or narrow the first version.

### Phase 4 - Design Discovery

Read [discovery-and-descriptions.md](references/discovery-and-descriptions.md).

Choose a portable lowercase hyphenated `name` that matches the directory. Write a `description` that states what the skill does and when to use it. Front-load core trigger terms and include exclusions only when they prevent likely false positives.

### Phase 5 - Shape The Package

Read [spec-and-structure.md](references/spec-and-structure.md) for required format.

Start with only `SKILL.md`. Add bundled files only when they earn their keep.

| Need | Default action |
| --- | --- |
| Core instructions every run | Keep in `SKILL.md` |
| Rare, long, or conditional detail | Move to `references/` |
| Static templates, sample files, schemas, or images | Put in `assets/` |
| Deterministic, repeated, fragile, or machine-verifiable work | Consider `scripts/` after risk review |
| Non-trivial activation or output quality | Add `evals/` or a lightweight eval plan |

Use minimal frontmatter by default: `name` and `description`. Add optional fields only for concrete compatibility, licensing, metadata, or tool needs.

### Phase 6 - Write The Body

Read [content-patterns.md](references/content-patterns.md).

Write operational instructions for the agent, not explanatory documentation for humans. Use a scannable structure that fits the skill instead of copying a fixed template.

Keep `Overview` to 1-2 sentences about what the skill does and why it matters. Keep `When To Use` focused on activation guidance. Use phase headings, tables, examples, red flags, rationalizations, or verification only when they improve behavior.

### Phase 7 - Evaluate

Read [evaluation.md](references/evaluation.md).

Every creation or material update must include a lightweight eval plan or a clear reason evals are unnecessary. Add full eval files for non-trivial skills, risky workflows, scripts, complex activation boundaries, or repeated future use.

### Phase 8 - Review

Read [audit-checklist.md](references/audit-checklist.md).

Fix checklist failures and re-check until the skill is valid, focused, and usable. If auditing only, return findings ordered by severity with concrete fixes.

## Reference Map

Load only the reference needed for the current decision:

- Skill format and frontmatter: [spec-and-structure.md](references/spec-and-structure.md)
- Names, triggers, and descriptions: [discovery-and-descriptions.md](references/discovery-and-descriptions.md)
- Body organization and progressive disclosure: [content-patterns.md](references/content-patterns.md)
- Evals and iteration: [evaluation.md](references/evaluation.md)
- Scripts, dependencies, and security: [scripts-and-security.md](references/scripts-and-security.md)
- Final review or audits: [audit-checklist.md](references/audit-checklist.md)

Do not preload all references.

## Defaults

- Author portable Agent Skills first. When a local choice is needed, prefer Opencode-compatible `.agents/skills` conventions.
- Keep changes minimal. Do not add backward-compatibility or migration logic without persisted data, external consumers, shipped behavior, or explicit user need.
- Prefer concrete examples and gotchas over generic best-practice prose.
- Use forward-slash relative paths from the skill root.
- Avoid time-sensitive claims unless they are isolated as legacy context.

## Common Rationalizations

| Rationalization | Reality |
| --- | --- |
| "This skill should include every best practice." | Skills should include only guidance that changes agent behavior for the target job. |
| "A fixed template will keep skills consistent." | Consistency helps, but unnecessary sections create noise. Choose sections by need. |
| "Evals are optional polish." | Every material skill change needs at least a lightweight eval plan or an explicit reason evals are unnecessary. |
| "A script would make this look more capable." | Scripts add maintenance and security risk. Add them only when they improve reliability. |

## Red Flags

- The description says "helps with" but does not name concrete triggers.
- The skill tries to cover multiple unrelated jobs.
- References exist but `SKILL.md` does not say when to load them.
- Scripts are present without a clear interface, dependency story, or risk check.
- A non-trivial skill has no eval plan.

## Output

For creation or update tasks, return the files changed, the key design choices, and the eval or validation performed. For audits, return findings first, then suggested fixes. Keep summaries concise.

## Verification

Before finalizing a created or modified skill, confirm:

- [ ] `Overview` explains what the skill does in 1-2 sentences.
- [ ] `When To Use` focuses on activation guidance and near-miss exclusions.
- [ ] The structure is scannable and adaptive, not a forced template.
- [ ] The description is specific enough to trigger correctly among many skills.
- [ ] Bundled files are justified and referenced with load conditions.
- [ ] Scripts, network access, or third-party content received a risk check when present.
- [ ] Evals are included or the reason they are unnecessary is explicit.
