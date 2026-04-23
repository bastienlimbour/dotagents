# Skills Overview

## What is a skill

Agent Skills extend AI agents with specialized knowledge, domain expertise, workflows, and capabilities. Each skill is a folder containing a `SKILL.md` (with YAML frontmatter: `name` and `description`) and Markdown instructions to perform a specific task or work on a domain. Optional files (scripts, references, assets) can be included. Skills may be simple instructions or full structured workflows.

## Directory structure

A skill is a directory containing a `SKILL.md` file, and optional bundled files. The standard directory structure is:

```text
skill-name/
├── SKILL.md          # Required: metadata + instructions
├── references/       # Optional: documentation, additional files
├── scripts/          # Optional: executable code
├── assets/           # Optional: templates, resources
└── ...               # Any additional files or directories
```

Do NOT include additional files like `README.md`, `CONTRIBUTING.md`, `LICENSE`, etc. inside the skill folder. All documentation belongs in `SKILL.md` or `references/`.

## How skills work (progressive disclosure)

Skills load content in three stages to manage context efficiently:

1. **Discovery**: At startup, agents load the YAML frontmatter (`name` and `description`) from every skill (~100 tokens).
2. **Activation**: When a task matches a skill's `description`, the agent loads the full `SKILL.md` body (< 5000 tokens).
3. **Execution**: The agent follows instructions from `SKILL.md` and optionally loads referenced files as needed from `scripts/`, `references/`, `assets/` (unlimited tokens).

This approach keeps agents fast while giving them access to more context on demand.

To make this approach effective, we need to:

- Write good descriptions
- Keep `SKILL.md` under 500 lines
- Move detailed content to separate reference files

## SKILL.md file

`SKILL.md` is the single required file in every skill. It contains two parts:

- A **YAML frontmatter** with `name` and `description` metadata used for discovery.
- A **Markdown body** with the skill's instructions.

Skills may be simple instructions or full structured workflows — the body has no format restrictions.

## Optional directories

### `references/`

Documentation too detailed for the main `SKILL.md` — long workflows, domain rules, schemas, API details, etc.

Keep individual files focused and small. Agents load them on demand, so smaller files mean less context usage.

### `scripts/`

Executable code agents can run. Use scripts when executable logic improves reliability — validation, parsing, deterministic transforms, repetitive operations, etc.

Supported languages depend on the agent implementation. Common options include Python, Bash, and JavaScript.

Do NOT add scripts just because code is possible. Add them when code is the more reliable path.

### `assets/`

Static resources used in outputs: templates, images, data files, tables, schemas. Assets should not carry core instructions.

## File references

Reference bundled files using relative paths from the `SKILL.md` file:

````markdown
- See [the reference guide](references/REFERENCE.md) for details.
- Run the extraction script: `python scripts/extract.py`
````

Bundled files must be referenced from `SKILL.md`. Avoid deeply nested reference chains.

## Example

A minimal, complete `SKILL.md` example:

```markdown
---
name: writing-release-notes
description: Generates release notes from git history and changelog entries. Use when the user asks to write, draft, or update release notes, or mentions a new release.
---

# Writing Release Notes

## When to use

**Use this skill when:**

- Drafting release notes for a new version
- Summarizing changes from git history or a changelog

**Do NOT use this skill when:**

- Writing general documentation or blog posts

## Process

1. Identify the version range (previous tag to current HEAD)
2. Collect commits and changelog entries
3. Group changes by category (features, fixes, breaking changes)
4. Write release notes following the template in [release-template.md](references/release-template.md)
5. Review with the user before finalizing

## Rules

- ALWAYS use the release template
- ALWAYS write the release notes in english

## Output

The output is a markdown file containing the release notes. The file is named `release-notes-<version>.md` and is placed in the `output/` directory. It must follow the [release template](references/release-template.md) format.
```
