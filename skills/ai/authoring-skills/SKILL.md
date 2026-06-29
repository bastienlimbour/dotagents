---
name: authoring-skills
description: Creates, updates, improves, and audits Agent Skills. Use when the task directly involves creating or updating an agent skill, SKILL.md, skill description, skill directory, skill bundled files, or skill evals. Do not use for standalone prompts or if the current task is not directly related to authoring agent skills.
---

# Authoring Skills

Create, update, improve, and audit portable Agent Skills. Make agents reliably better at one repeatable job without bloating context or forcing unnecessary structure.

## When To Use

- Creating or updating an Agent Skill, `SKILL.md`, description, trigger surface, bundled files, scripts, or evals.
- Auditing a skill for structure, discovery, progressive disclosure, security, or eval coverage.

Do not use for standalone prompts, non-skill agent config, READMEs, or general writing unless the user wants that artifact packaged as a skill.

## Core Principle

Write the simplest and smallest skill that does the job. Add structure, examples, references, assets, scripts, or evals only when they improve the output quality or make the skill easier to discover, follow, verify, or maintain.

## Workflow

For non-trivial work, track your progress with a checklist.

### 1. Classify And Inspect

- Create: run the full workflow.
- Update: inspect the existing skill and edit only what the request requires.
- Vague improvement: audit first, then fix the highest-value gaps.
- Audit: return findings first and stop unless edits are requested.

Inspect existing skill files, source material, real workflows, examples, previous failures, and adjacent skills. Ask one targeted question at a time only when the answer would materially change the skill. For substantial new skills or major rewrites, summarize intended files and ask to proceed unless already approved.

### 2. Define The Boundary

Identify the repeatable job, users, inputs, outputs, constraints, non-goals, success criteria, and near-miss tasks. Prefer one coherent job; split or narrow broad toolboxes.

### 3. Design Discovery

Read [discovery-and-descriptions.md](references/discovery-and-descriptions.md).

Choose a portable lowercase hyphenated `name` that matches the directory. Write a `description` that states what the skill does and when to use it. Front-load core trigger terms and include exclusions only when they prevent likely false positives.

### 4. Shape The Package

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

### 5. Write The Body

Read [content-patterns.md](references/content-patterns.md).

Write operational instructions for the agent, not explanatory documentation for humans. Use a scannable structure that fits the skill instead of copying a fixed template.

Use sections only when they change behavior. Keep `Overview` short, `When To Use` focused on activation guidance, and optional sections such as examples, red flags, rationalizations, output, or verification proportional to risk.

### 6. Evaluate

Read [evaluation.md](references/evaluation.md).

Every creation or material update must include a lightweight eval plan or a clear reason evals are unnecessary. Add full eval files for non-trivial skills, risky workflows, scripts, complex activation boundaries, or repeated future use.

### 7. Review

Read [audit-checklist.md](references/audit-checklist.md).

Fix checklist failures and re-check until the skill is valid, focused, and usable. If auditing only, return findings ordered by severity with concrete fixes.

## Reference Map

Load only the reference needed for the current decision. Do not preload all references.

- Skill format and frontmatter: [spec-and-structure.md](references/spec-and-structure.md)
- Names, triggers, and descriptions: [discovery-and-descriptions.md](references/discovery-and-descriptions.md)
- Body organization and progressive disclosure: [content-patterns.md](references/content-patterns.md)
- Evals and iteration: [evaluation.md](references/evaluation.md)
- Scripts, dependencies, and security: [scripts-and-security.md](references/scripts-and-security.md)
- Final review or audits: [audit-checklist.md](references/audit-checklist.md)

## Rules

- Author portable Agent Skills first. When a local choice is needed, prefer Opencode-compatible `.agents/skills` conventions.
- Keep changes minimal. Do not add backward-compatibility or migration logic without persisted data, external consumers, shipped behavior, or explicit user need.
- Prefer concrete examples and gotchas over generic best-practice prose.
- Use forward-slash relative paths from the skill root.
- Avoid time-sensitive claims unless they are isolated as legacy context.
- Avoid "helps with" descriptions that do not name concrete triggers.
- If references exist, `SKILL.md` must say when to load them.
- If scripts exist, document interface, dependencies, and risk checks.

## Output

For creation or update tasks, return the files changed, the key design choices, and the eval or validation performed. For audits, return findings first, then suggested fixes. Keep summaries concise.

## Validation

Before finalizing, confirm:

- [ ] The skill covers one coherent repeatable job.
- [ ] The description triggers correctly and avoids likely false positives.
- [ ] The body is operational, scannable, and not a forced template.
- [ ] Bundled files are justified and referenced with load conditions.
- [ ] Scripts, network access, or third-party content received a risk check when present.
- [ ] Evals are included, or the reason they are unnecessary is explicit.
