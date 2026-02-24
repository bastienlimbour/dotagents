---
name: creating-skills
description: Guides through creating well-structured agent skills. Use when the user wants to create a new skill, write a SKILL.md, improve an existing skill, or asks about skill structure and best practices.
---

# Creating Skills

Guide for creating effective skills. Read the reference files based on what you need:

- **Skill concepts and structure**: See [skills-overview.md](references/skills-overview.md)
- **Authoring guidelines and best practices**: See [skills-guidelines.md](references/skills-guidelines.md)

## Workflow

Copy this checklist and track your progress:

```plaintext
Skill creation progress:
- [ ] Step 1: Gather Requirements
- [ ] Step 2: Plan the Skill Structure
- [ ] Step 3: Write the Skill
- [ ] Step 4: Review and Iterate
```

### Step 1: Gather Requirements

Understand what the skill should do through concrete examples:

1. **Purpose**: What specific task, domain, or workflow does this skill address?
2. **Trigger scenarios**: When should the agent apply this skill? What are 2-3 specific use cases or example requests?
3. **Domain knowledge**: What information does the agent need that it would not already know?
4. **Output expectations**: Are there specific formats, templates, or conventions required?
5. **Supporting assets**: Are reference files or utility scripts needed? Does it need executable scripts, reference materials, or output assets? Are there existing resources (docs, schemas, templates) to include?

If requirements are unclear, ask the user for clarification before proceeding.

Keep questions focused — avoid overwhelming the user. Start with the most important questions and follow up as needed.

### Step 2: Plan the Skill Structure

Analyze each use case and identify what reusable resources to include:

| If the use case involves... | Then include... |
| ---- | --- |
| Repeating the same code logic | `scripts/` with executable scripts |
| Needing domain knowledge or schemas | `references/` with documentation files |
| Producing output from templates/assets | `assets/` with template files |
| Only procedural guidance | Instructions in SKILL.md body only |

Decide what belongs in SKILL.md vs. separate files. Keep SKILL.md as the navigation hub — move detailed content to reference files.

### Step 3: Write the Skill

#### 3a. Create the directory structure

```text
skill-name/
├── SKILL.md
├── scripts/       (if needed)
├── references/    (if needed)
└── assets/        (if needed)
```

Only create directories that the skill actually needs.

#### 3b. Implement bundled resources first

Create any scripts, references, or assets identified in Step 2. Test scripts by running them.

If the user needs to provide resources (brand assets, schemas, policies), ask for them now.

#### 3c. Write SKILL.md

**Frontmatter** — The description is the sole trigger mechanism. It must include:

1. What the skill does (capabilities)
2. When to use it (triggers, keywords, file types, contexts)

Write in third person. Max 1024 chars. Do not put "when to use" info in the body — only the frontmatter description is available for trigger matching.

```yaml
---
name: skill-name
description: [What it does]. Use when [specific triggers, keywords, contexts].
---
```

**Body** — Choose the structure that fits the skill's purpose:

- **Workflow-based**: Sequential steps with decision points. Best for multi-step processes.
- **Task-based**: Grouped operations/capabilities. Best for tool collections.
- **Reference-based**: Standards, specifications, guidelines. Best for domain knowledge.

Combine patterns as needed. Always reference bundled files with clear instructions on when to read them.

**Degrees of Freedom**: Match specificity to the task's fragility (see skills guidelines).

```markdown
# Skill Title

## Quick start
[Minimal working example or core workflow]

## [Main sections based on chosen structure]
[Instructions, workflows, decision trees, code examples]

## Resources (if applicable)
- **[resource-name]**: See [path](relative/path) — use when [condition]
```

### Step 4: Review and Iterate

Verify against this checklist (only check items that are applicable):

- [ ] Description states what + when (specific triggers)
- [ ] Description written in third person
- [ ] SKILL.md body under 500 lines
- [ ] Only essential content in SKILL.md, details in reference files
- [ ] All bundled files referenced from SKILL.md with clear "when to read" guidance
- [ ] References are one level deep (no nested references)
- [ ] No extraneous files (README, CHANGELOG, etc.)
- [ ] No time-sensitive information
- [ ] No references to specific agents or models (no "Claude", "GPT", "Opencode", etc.)
- [ ] Consistent terminology throughout
- [ ] Concrete examples over abstract descriptions
- [ ] MCP tools are referenced using fully qualified names (ServerName:tool_name)
- [ ] Scripts tested and working (if applicable)
- [ ] Scripts have clear error handling and logging
- [ ] Scripts do not perform dangerous or irreversible actions without validation

Present the draft to the user and ask for feedback. Iterate based on real usage observations.
