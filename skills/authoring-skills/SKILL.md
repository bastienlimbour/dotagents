---
name: authoring-skills
description: Creates, edits, improves, and audits agent skills (SKILL.md files with optional bundled resources). Use when creating new skills, working on existing skills or when the user asks to write a new skill, refactor or improve an existing skill, review a skill for quality, or needs help with skill structure, metadata, content organization, or any skill related task. Don't use for general documentation, writing AGENTS.md or README.md files, or writing scripts unrelated to a skill's bundled resources.
---

# Authoring Skills

## When to use this skill

- Writing a new skill
- Editing, refactoring or improving an existing skill
- Reviewing a skill for quality
- Helping with skill structure, metadata, content organization, or any skill related task

## When not to use this skill

- General documentation writing that isn't a skill
- Writing `AGENTS.md` rules or `.cursorrules` files
- Writing scripts unrelated to a skill's bundled resources

## Quick start

1. Read [skills-overview.md](references/skills-overview.md) to understand what are skills and how they work.
2. Read [skills-best-practices.md](references/skills-best-practices.md) to understand the best practices for authoring skills.
3. Determine the mode (create, edit/improve, audit)
4. Follow the matching workflow.

| Mode | Trigger | Workflow entry point |
| ---- | ------- | ----------- |
| **Create** | User wants a new skill | Step 1 → full workflow |
| **Edit / Improve** | User wants to change or improve an existing skill | Read existing skill + all bundled files → Step 1 → full workflow |
| **Audit** | User wants a quality review of an existing skill | Read existing skill + all bundled files → Step 7 → Step 9 |

## Workflow

Track progress with this todolist:

```text
Skill authoring progress:
- [ ] Step 1: Gather requirements
- [ ] Step 2: Decide on bundled resources
- [ ] Step 3: Design the trigger surface (frontmatter)
- [ ] Step 4: Plan the skill architecture
- [ ] Step 5: Write bundled resources (if any)
- [ ] Step 6: Write SKILL.md
- [ ] Step 7: Quality check
- [ ] Step 8: Test triggering and execution (if possible)
- [ ] Step 9: Review and refine with the user
```

### Step 1: Gather requirements

Clarify these before writing anything:

- **Task**: What specific job does this skill perform?
- **Use cases**: Define 2-3 concrete use cases, each with trigger phrases the user might say and the expected outcome.
- **Domain**: What domain knowledge is involved?
- **Scope**: What is in and out of scope? One job per skill.
- **Success criteria**: What does a good result look like?
- **Inputs**: What does the agent receive (files, prompts, context)?
- **Outputs**: What does the agent produce?

If the request is underspecified, ask clarifying questions.

For **edit** mode, read the existing skill and all bundled files first to understand current state.

### Step 2: Decide on bundled resources

Determine if the skill needs bundled resources (references, scripts, assets, quality checklist).

Default: no bundled resources. Add them only when needed.

If anything is unclear about the bundled resources requirements, ask the user for clarification before continuing.

### Step 3: Design the trigger surface (frontmatter)

1. Choose a `name`.
2. Write a `description`.
3. Create the skill directory matching the `name`.
4. Create `SKILL.md` with the YAML frontmatter.

Litmus test: "If an agent sees a hundred skill descriptions, would this one activate for the right tasks and stay silent for the wrong ones?"

### Step 4: Plan the skill architecture

Choose the simplest body type that reliably solves the task:

- **Workflow-based**: multi-step processes with sequential steps and validation loops.
- **Task-based**: grouped capabilities or tool collections.
- **Reference-based**: standards, specifications, or domain knowledge.

Decide the progressive disclosure strategy: what goes inline in SKILL.md vs. in reference files. Keep references one level deep from SKILL.md.

### Step 5: Write bundled resources (if needed)

Write resources **before** SKILL.md so the main file can reference them accurately.

For each resource file:

- Keep it focused on a single topic
- Use a descriptive filename
- Add a table of contents if longer than ~100 lines
- Include only content the agent cannot reliably produce on its own

For reference files that contain workflows, procedures, decision trees, or other instructions the agent will follow, apply prompt engineering best practices: clear objectives, explicit constraints, uncertainty handling, output contracts when needed, and verification steps.

### Step 6: Write or update SKILL.md

Write the body of the skill in `SKILL.md`.

The body is an instruction set an LLM agent will follow, so it is also a prompt. Apply prompt engineering best practices to the skill body: objective, constraints, output contract, uncertainty handling, and verification.

Follow the best practices in [skills-best-practices.md](references/skills-best-practices.md) and structure the body with:

1. A top-level heading matching the skill name
2. "When to use" and "When not to use" scope boundaries
3. A quick start section (the shortest path to value)
4. The core workflow or instructions
5. References to bundled files with clear "when to read" guidance

Keep the body under 500 lines. Move detailed content to reference files.

### Step 7: Quality check

Read and evaluate against the [skills checklist](references/skills-checklist.md). Verify every applicable item.

Also verify that the instructions in `SKILL.md` body and any instruction-like reference files follow the prompt-engineering best practices.

Organize findings as:

- **Pass** — items meeting quality standards
- **Fail** — items that need fixing, with specific recommendations
- **N/A** — items that don't apply to this skill

For **create** and **edit/improve** modes, iterate until the quality checklist is passing.

For **audit** mode, present the findings and recommendations.

### Step 8: Test triggering and execution (if possible)

If the environment allows testing, verify:

- **Triggering**: Does the skill activate for expected queries and stay silent for unrelated ones?
- **Execution**: Does the skill produce correct, complete output on a real or simulated use case?

Skip this step if the environment doesn't support live testing.

### Step 9: Review and refine with the user

Present the result with:

- Summary of what was created, changed, or found
- The completed quality checklist (pass/fail/n/a for each item)
- Trade-offs or decisions worth noting

Iterate based on feedback until the user is satisfied. When refining, read agent execution traces (not just final outputs) to identify vague instructions that cause unproductive steps, instructions that don't apply to the task at hand, or options presented without a clear default.

## Troubleshooting and Error Handling

- **Request is underspecified**: Ask targeted questions before drafting the skill. Do not invent domain expertise, hidden constraints, or success criteria.
- **Bundled file is missing or mismatched**: Stop and fix the broken path, filename, or reference before continuing. Keep `SKILL.md` and bundled resources in sync.
- **Guidance conflicts across files**: Prefer the stricter runtime or checklist constraint, then update the conflicting reference files so the skill teaches one consistent rule.
- **Environment cannot support live testing**: Mark trigger or execution checks as not tested, state the limitation explicitly, and use a concrete simulated example when possible.
- **The skill is getting too large or vague**: Split the content into smaller focused references, tighten the scope, or recommend multiple composable skills instead of one broad skill.
