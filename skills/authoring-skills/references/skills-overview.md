# Skills Overview

## Contents

- What is a skill
- Directory structure
- How skills work (progressive disclosure)
- SKILL.md file (structure, frontmatter, security restrictions, body, example)
- Optional directories (references, scripts, assets)
- File references

## What is a skill

Agent Skills are a lightweight, open format for extending AI agent capabilities with specialized knowledge, domain expertise, new capabilities, and repeatable workflows

A skill is a folder containing a `SKILL.md` file with YAML frontmatter (metadata) and Markdown instructions that gives an agent the knowledge and instructions to perform a specific task. Skills can also bundle scripts, reference files, and assets.

## Directory structure

A skill must have the following directory structure:

```text
skill-name/
├── SKILL.md          # Required: metadata + instructions
├── scripts/          # Optional: executable code
├── references/       # Optional: documentation
├── assets/           # Optional: templates, resources
```

Do not include additional files like `README.md`, `LICENSE`, `CONTRIBUTING.md`, etc. inside the skill folder. All documentation belongs in `SKILL.md` or `references/`.

Prefer the standard folders above. For complex workflows, store complex step-by-step guides in `references/` instead of creating ad hoc folders such as `steps/`.

Well-designed Skills are small, composable, and easy to discover.

## How skills work (progressive disclosure)

Skills load content in three stages to manage context efficiently:

1. **Discovery** (~100 tokens): At startup, agents load only `name` and `description` from every skill's frontmatter.
2. **Activation** (< 5000 tokens recommended): When a task matches, the agent reads the full `SKILL.md` body.
3. **Execution** (as needed): The agent follows instructions and loads referenced files (`scripts/`, `references/`, `assets/`) only when required.

Keep `SKILL.md` under 500 lines. Move detailed content to separate reference files.

This approach keeps agents fast while giving them access to more context on demand.

## `SKILL.md` file

### Structure

The `SKILL.md` file must contain YAML frontmatter followed by Markdown instructions.

### Frontmatter

The YAML frontmatter is required at the top of `SKILL.md` for discovery metadata: both `name` and `description` are required.

#### `name`

- 1–64 characters, lowercase alphanumeric and hyphens only (`a-z`, `0-9`, `-`)
- No leading, trailing, or consecutive hyphens
- Must match the parent directory name

Valid: `pdf-processing`, `data-analysis`, `code-review`
Invalid: `PDF-Processing` (uppercase), `-pdf` (leading hyphen), `pdf--processing` (consecutive hyphens)

#### `description`

- 1–1024 characters
- State what the skill does and when to use it
- Include keywords that help agents match tasks to this skill
- Write in third person

Good: `Extracts text and tables from PDF files, fills PDF forms, and merges multiple PDFs. Use when working with PDF documents or when the user mentions PDFs, forms, or document extraction. Do not use for other document types than PDF.`

Poor: `Helps with PDFs.`

Do NOT put long workflows, caveats, or examples in description.

#### Security restrictions

- No XML angle brackets (`<`, `>`) in frontmatter — frontmatter appears in the system prompt and could inject instructions.
- Names must not start with `claude`, `anthropic`, `openai`, `vercel`, etc. (reserved prefixes).

### Body

The Markdown body of the `SKILL.md` file contains the skill's instructions. There are no structural requirements — write whatever helps agents perform the task effectively.

Useful sections you can include in the body:

- When to use this skill (optional clarification if the body needs context, but do not rely on this for triggering)
- When not to use this skill (scope boundaries and nearby cases handled elsewhere)
- Expected inputs (files, prompts, context, schemas, or tools expected)
- Quick start (smallest working path)
- Workflow (ordered steps, branching logic, validation loops)
- Decision rules (defaults, constraints, exceptions)
- Resources (resources used in the skill, such as APIs, tools, or libraries)
- Examples (input/output pairs that demonstrate expected behavior)
- Troubleshooting (common errors, causes, and fixes)
- Outputs (expected artifact, format, or final handoff)

Not every skill needs every section, but strong skills usually make these concerns explicit.

Adjust the body type to fit the skill:

- **Workflow-based**: Best for multi-step processes.
- **Task-based**: Best for tool collections or grouped capabilities.
- **Reference-based**: Best for standards, specifications, and domain knowledge.

The body should answer: "Now that this skill has triggered, what should the agent do first, and where should it go next?"

### Example

A minimal, complete skill:

```markdown
---
name: writing-release-notes
description: Generates release notes from git history and changelog entries. Use when the user asks to write, draft, or update release notes, or mentions a new release.
---

# Writing Release Notes

## When to use this skill
- Drafting release notes for a new version
- Summarizing changes from git history or a changelog

## When not to use this skill
- Writing general documentation or blog posts

## Workflow

1. Identify the version range (previous tag to current HEAD)
2. Collect commits and changelog entries
3. Group changes by category (features, fixes, breaking changes)
4. Write release notes following the template in [release-template.md](references/release-template.md)
5. Review with the user before finalizing
```

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

Reference other skill files using relative paths from the skill root:

````markdown
See [the reference guide](references/REFERENCE.md) for details.

Run the extraction script: `python scripts/extract.py`
````

Keep references one level deep from `SKILL.md`. Avoid deeply nested reference chains.
