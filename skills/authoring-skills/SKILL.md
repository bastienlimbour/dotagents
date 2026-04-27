---
name: authoring-skills
description: Creates, edits, improves, and audits agent skills. Use when creating a new agent skill, editing, refactoring, or improving an existing skill, designing skill discovery, organizing bundled resources in a skill, reviewing or auditing a skill.
---

# Authoring Skills

## Overview

This skill outlines the process for creating, editing, improving, and auditing agent skills.

If unfamiliar with agent skills, read [skills-overview.md](references/skills-overview.md).

## When to use

**Use this skill when:**

- Creating a new agent skill
- Editing, refactoring, or improving an existing skill
- Designing a skill's trigger surface and discovery
- Organizing a skill's bundled resources
- Reviewing or auditing a skill for quality, structure, or discovery

**Do NOT use this skill for:**

- Standalone prompts that are not packaged as a skill
- General documentation, READMEs, or non-skill related content
- Agent rules, hooks, settings, or other non-skill config

## Process

Follow the process below and track progress with a checklist:

- [ ] Step 0: Determine the path
- [ ] Step 1: Gather context and requirements
- [ ] Step 2: Design the trigger surface
- [ ] Step 3: Design the skill content
- [ ] Step 4: Check quality

Load only the reference files named in the current step. Do NOT preload other references.

### Step 0: Determine the path

Confirm with the user (or infer) which path applies:

- **Creating a new skill**: Run steps 1 to 4 in order.
- **Modifying or improving an existing skill**: If gaps are known, run only relevant steps from step 1 to 3 and edit only the parts that need work. If gaps are unknown ("improve this skill"), run step 4 (to check quality and identify gaps) and then run steps 1 to 3 to fix them, then repeat step 4 to check again.
- **Auditing a skill**: Run step 4 (quality review), report issues and findings to the user, then propose changes to fix them and apply only if the user agrees.

Update the progress checklist to reflect the path and steps chosen.

### Step 1: Gather context and requirements

Before gathering context and requirements, read [scope-and-expertise.md](references/scope-and-expertise.md).

Clarify these key details:

- Task or domain to cover (preferably one clear repeatable job)
- Specific use cases or scenarios to handle
- Clear triggers and exclusions
- Expected inputs and outputs
- Constraints and non-goals
- Success criteria
- Real source material when available

If any of the above details are unclear, ask targeted questions to the user until every detail is clear.

### Step 2: Design the trigger surface

Before designing the trigger surface, read [naming-and-discovery.md](references/naming-and-discovery.md).

- choose a precise `name` that clearly describes the skill's purpose
- draft a `description` that states what the skill does and when to use it
- optimize `description` for correct activation, not completeness
For new skills:
- create the directory (matching the `name`)
- create the `SKILL.md` file and add frontmatter with the `name` and `description`

Litmus test: "If an agent sees a hundred skill descriptions, would this one activate for the right tasks and stay silent for the wrong ones?"

### Step 3: Design the skill content

Before writing the skill content, read [skill-body-patterns.md](references/skill-body-patterns.md).

Write the smallest skill that can do the job:

- pick the lightest body shape that fits the task
- write the SKILL.md body instructions as a prompt, not as documentation
- prefer numbered workflows, short rules, and explicit verification
- keep `SKILL.md` focused and move rare detail to `references/`, `scripts/`, or `assets/`
- do not force a default template; adapt the structure to the task

If the skill needs bundled files or `SKILL.md` is getting large, read [skill-files-and-disclosure.md](references/skill-files-and-disclosure.md).

If the skill uses MCP tools, read [mcp.md](references/mcp.md).

If the skill uses scripts, read [scripts.md](references/scripts.md).

### Step 4: Check quality

When creating or modifying a skill:

- check every relevant item in [checklist.md](references/checklist.md)
- fix failures and re-check until all items pass
- optionally test the skill on 2-3 representative tasks
- note misses in activation, file navigation, or output quality
- refine the skill and re-test until the issues are resolved

When auditing a skill:

- check every relevant item
- report gaps with suggested fixes
- stop unless the user asks for edits
