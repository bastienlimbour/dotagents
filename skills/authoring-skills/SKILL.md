---
name: authoring-skills
description: Creates, edits, improves, and audits agent skills (SKILL.md files with optional bundled resources). Use when creating new skills or working on existing skills (editing, refactoring, reviewing or improving an existing skill). Use when the user needs help with skill structure, metadata, content organization, or any skill related task.
---

# Authoring Skills

## When to use

**Use this skill when:**

- Creating a new agent skill
- Editing, refactoring, or improving an existing skill
- Reviewing or auditing a skill for quality
- Any agent skill related task

**Do NOT use this skill when:**

- Writing prompts that are not packaged as a skill
- Writing general documentation, README, or other non-skill related content
- Authoring agents rules, hooks, settings, or other non-skill configurations

## Process

Follow the steps and track your progress with this todolist:

- [ ] Step 0 - Determine intent
- [ ] Step 1 - Gather context and requirements
- [ ] Step 2 - Design the trigger surface
- [ ] Step 3 - Design the skill content
- [ ] Step 4 - Check quality

Each step loads its own reference files. Do not preload reference files from other steps.

### Step 0 - Determine intent

Read [skills-overview.md](references/skills-overview.md) if unfamiliar with agent skills.

Confirm with the user (or infer) which path applies:

- **Creating a new skill**: Run Steps 1 to 4 in order.
- **Modifying (editing or improving) an existing skill**: If gaps are known, run only relevant Steps 1 to 3, then Step 4. If gaps are unknown ("improve this skill"), start with Step 4 to identify gaps, address in Steps 1 to 3, then run Step 4 again.
- **Auditing a skill**: Quality review only. Run Step 4, report findings, then apply changes only if the user confirms.

Update the progress tracking todolist with the relevant steps.

### Step 1 - Gather context and requirements

Read [scope-and-expertise.md](references/scope-and-expertise.md) before gathering context and requirements.

1. Clarify the context and requirements:
    - What task or domain does the skill cover?
    - What specific use cases should it handle?
    - When should the skill be triggered and when should it not (in and out of scope)?
    - What inputs does the skill need to handle the task (prompts, data, files, context, etc.)?
    - What outputs does the skill produce (create/edit files, generate text, run commands, etc.)?
    - What are the constraints and non-goals (what must never happen, tools to avoid, style rules)?
    - What are the success criteria (expected outcome of the skill, what does a good result look like)?
    - What source material is available to create the skill (docs, runbooks, past conversations, code patterns, gotchas, preferred tools, output templates)?
2. If anything is unclear or underspecified, ask clarifying questions until everything is clear.
3. If the user cannot provide domain-specific context or material, flag the risk and propose alternatives (co-perform the task once to extract a pattern, narrow the scope, or use existing artifacts).

### Step 2 - Design the trigger surface

Read [naming-and-discovery.md](references/naming-and-discovery.md) before designing the trigger surface.

1. Choose a `name` that clearly describes the skill purpose.
2. Draft a `description` that states what the skill does and when to use it.
3. For new skills, create the skill directory matching the `name` (global skills in `~/.agents/skills/<name>/`, project skills in `.agents/skills/<name>/`).
4. Create the `SKILL.md` file and add the YAML frontmatter with the `name` and `description` fields.

Litmus test: "If an agent sees a hundred skill descriptions, would this one activate for the right tasks and stay silent for the wrong ones?"

### Step 3 - Design the skill content

Read [skills-content-design.md](references/skills-content-design.md) before designing the skill content.

1. Choose the simplest body type that reliably solves the task.
2. Write the `SKILL.md` Markdown body with concise instructions as a prompt: lead with objective, make constraints explicit, say what to do, handle uncertainty, define output, and include verification.
3. Decide on bundled resources and move detail out of `SKILL.md` as needed:
    - `references/`: Long workflows, domain rules, schemas.
    - `scripts/`: Add only when executable code is more reliable than instructions.
    - `assets/`: Templates, data files, or images used in outputs.

If the skill uses MCP tools, also read [mcp-best-practices.md](references/mcp-best-practices.md).

If the skill uses scripts or executable code, also read [scripts-best-practices.md](references/scripts-best-practices.md).

### Step 4 - Check quality

Run every applicable item in [skills-checklist.md](references/skills-checklist.md). Fix failures and re-check until all pass.

For audits, report failing items with suggested fixes and stop. Do not rewrite the skill unless the user confirms.
