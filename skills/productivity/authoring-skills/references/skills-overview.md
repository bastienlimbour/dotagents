# Skills Overview

Read this file ONLY if you are unfamiliar with agent skills.

## What a skill is

Agent Skills extend AI agents with specialized knowledge, domain expertise, workflows, and capabilities. A skill is a folder with a `SKILL.md` plus optional bundled files. The frontmatter in `SKILL.md` (`name` and `description`) handles discovery, the body tells the agent what to do.

## Directory structure

Standard directory structure:

```text
skill-name/
├── SKILL.md          # Required: frontmatter + instructions
├── references/       # Optional: documentation, additional files
├── scripts/          # Optional: executable code
├── assets/           # Optional: templates, resources
└── ...               # Any additional files or directories
```

Do NOT include additional files like `README.md`, `CONTRIBUTING.md`, `LICENSE`, etc. inside the skill folder. All documentation belongs in `SKILL.md` or `references/`.

## How skills work (progressive disclosure)

Skills load content in three stages to manage context efficiently:

1. **Discovery**: At startup, agent loads `name` and `description` from every skill (few tokens)
2. **Activation**: When a task matches a skill's `description`, agent loads `SKILL.md` (moderate tokens)
3. **Execution**: Agent loads referenced files only when needed (many tokens)

This is called **progressive disclosure**, it keeps agents fast while giving them access to the relevant context when needed.

To make this work:

- write strong descriptions
- keep `SKILL.md` focused
- move rare detail into bundled files
- tell the agent when to load each file

## SKILL.md file

`SKILL.md` is the only required file. It has two parts:

- **YAML frontmatter**: `name` and `description`
- **Markdown body**: the skill instructions

The body can be short instructions or a structured workflow. There is no single required shape.

## Optional directories

`SKILL.md` should stay short and focused. If the skill needs additional context, put it in the optional directories:

- `references/`: for detailed documentation, domain knowledge, API details, etc.
- `scripts/`: for executable helpers (when code is more reliable than instructions). Running a script is often cheaper than loading its contents into context.
- `assets/`: for templates, images, tables, and static resources. Do not put core instructions in assets.

## File references

Reference bundled files from `SKILL.md` using relative paths:

````markdown
- See [the reference guide](references/REFERENCE.md) for details.
- Run the extraction script: `python scripts/extract.py`
````

Avoid deep reference chains, keep it one level deep.

## Example

````markdown
---
name: writing-release-notes
description: Generates release notes from git history and changelog entries. Use when the user asks to draft or update release notes.
---

# Writing Release Notes

## Workflow

1. Identify the version range
2. Collect commits and changelog entries
3. Group changes by category

## Advanced cases

For release formatting rules, read [release-format.md](references/release-format.md).
````
