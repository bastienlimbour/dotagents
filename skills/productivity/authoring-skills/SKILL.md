---
name: authoring-skills
description: Creates, updates, improves, and audits portable Agent Skills. Use when creating or changing a SKILL.md, skill directory, skill description, bundled references, scripts, resources, or skill evals. Do not use for standalone prompts or non-skill agent configuration.
---

# Authoring Skills

## Overview

Use this skill to create, update, improve, or audit portable Agent Skills. Optimize for small, discoverable, testable skills that use progressive disclosure and only include context the agent would otherwise miss.

If the task is about a standalone prompt, AGENTS.md, hooks, MCP setup, app config, or other non-skill instruction artifact, do not use this skill unless the user explicitly wants that work packaged as an Agent Skill.

## Reference Loading

Load only the reference needed for the current decision:

- Skill format and frontmatter: [spec-and-structure.md](references/spec-and-structure.md)
- Names, triggers, and descriptions: [discovery-and-descriptions.md](references/discovery-and-descriptions.md)
- Body organization and progressive disclosure: [content-patterns.md](references/content-patterns.md)
- Evals and iteration: [evaluation.md](references/evaluation.md)
- Scripts, dependencies, and security: [scripts-and-security.md](references/scripts-and-security.md)
- Final review or audits: [audit-checklist.md](references/audit-checklist.md)

Do not preload all references.

## Workflow

For non-trivial work, track progress with the available todo or checklist tool.

1. Classify the task.
   - Creating a skill: run the full workflow.
   - Updating a skill: inspect the existing skill and edit only the parts needed for the requested change.
   - Improving a skill with vague goals: audit first, then fix the highest-value gaps.
   - Auditing a skill: report findings first and stop unless the user asks for edits.

2. Gather evidence before asking questions.
   - Inspect existing skill files, source material, real workflows, examples, previous failures, and adjacent skills when available.
   - Ask one targeted question at a time only when missing information would materially change the skill.
   - For substantial new skills or major rewrites, summarize the intended files and ask to proceed unless the user already approved that exact work.

3. Define the skill boundary.
   - Identify the repeatable job, users, inputs, outputs, constraints, non-goals, success criteria, and near-miss tasks that should not trigger it.
   - Prefer one coherent job over a broad toolbox.

4. Design the trigger surface.
   - Read [discovery-and-descriptions.md](references/discovery-and-descriptions.md).
   - Choose a portable lowercase hyphenated `name` that matches the directory.
   - Write a `description` that states what the skill does and when to use it. Front-load core trigger terms and include exclusions only when they prevent likely false positives.

5. Design the skill package.
   - Read [spec-and-structure.md](references/spec-and-structure.md) for required format.
   - Start with only `SKILL.md`. Add `references/`, `assets/`, `scripts/`, or `evals/` only when they earn their keep.
   - Use minimal frontmatter by default: `name` and `description`. Add optional fields only for concrete compatibility, licensing, metadata, or tool needs.

6. Write the skill body.
   - Read [content-patterns.md](references/content-patterns.md).
   - Write operational instructions for the agent, not explanatory documentation for humans.
   - Keep the main file concise. Move rare, long, or conditional detail to one-level reference files and say exactly when to load each one.

7. Decide on scripts and security.
   - Read [scripts-and-security.md](references/scripts-and-security.md) before adding scripts, external downloads, network calls, or third-party content.
   - Prefer instruction-only skills. Add scripts only for deterministic, repeated, fragile, or machine-verifiable work.
   - Perform the mandatory risk check when scripts, network access, or untrusted materials are involved.

8. Add evaluation guidance.
   - Read [evaluation.md](references/evaluation.md).
   - Every creation or material update must include a lightweight eval plan or a clear reason evals are unnecessary.
   - Add full eval files for non-trivial skills, risky workflows, scripts, complex activation boundaries, or repeated future use.

9. Review quality.
   - Read [audit-checklist.md](references/audit-checklist.md).
   - Fix checklist failures and re-check until the skill is valid, focused, and usable.
   - If auditing only, return findings ordered by severity with concrete fixes.

## Defaults

- Author portable Agent Skills first. When a local choice is needed in this workspace, prefer OpenCode-compatible `.agents/skills` conventions.
- Keep changes minimal. Do not add backward-compatibility or migration logic without persisted data, external consumers, shipped behavior, or explicit user need.
- Prefer concrete examples and gotchas over generic best-practice prose.
- Use forward-slash relative paths from the skill root.
- Avoid time-sensitive claims unless they are isolated as legacy context.

## Output

For creation or update tasks, return the files changed, the key design choices, and the eval or validation performed. For audits, return findings first, then suggested fixes. Keep summaries concise.
