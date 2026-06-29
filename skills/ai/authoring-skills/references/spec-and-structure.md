# Spec And Structure

Use this reference when creating or changing a skill package, frontmatter, directory layout, or bundled files.

## Minimal Skill Shape

A portable Agent Skill is a directory containing `SKILL.md` with YAML frontmatter and Markdown instructions.

```
skill-name/
├── SKILL.md
├── references/
├── scripts/
├── assets/
└── evals/
```

Only `SKILL.md` is required. Add other directories only when they solve a real need.

## Required Frontmatter

Use minimal frontmatter by default:

```md
---
name: skill-name
description: Does a specific job. Use when the user asks for the matching task or context.
---
```

`name` requirements:

- 1 to 64 characters.
- Lowercase letters, numbers, and hyphens only for portability.
- Must not start or end with a hyphen.
- Must not contain consecutive hyphens.
- Must match the parent directory name.
- Must not contain reserved or vendor-specific names unless required by that platform.

`description` requirements:

- 1 to 1024 characters.
- Non-empty and specific.
- States what the skill does and when to use it.
- Includes high-value trigger terms and likely user intent.
- Avoids first person such as "I can" or "my skill".

## Optional Frontmatter

Add optional fields only when they earn their space:

- `license`: when the skill will be shared or has explicit licensing terms.
- `compatibility`: when the skill needs a specific client, runtime, package manager, system dependency, network access, or shell environment.
- `metadata`: when a client or team process consumes extra key-value fields.
- `allowed-tools`: only when the target client supports it and pre-approved tools are useful.

Do not add optional fields just to look complete.

## Directory Decisions

Use these directories consistently:

- `references/`: markdown guidance the agent reads only for conditional detail.
- `scripts/`: executable utilities the agent runs for deterministic or repeated operations.
- `assets/`: templates, examples, static data, images, schemas, or other non-instruction resources.
- `evals/`: trigger queries, task evals, test fixtures, and expected behavior.

Keep paths relative to the skill root and use forward slashes.

## Portability Notes

- Avoid client-specific assumptions unless the skill is intentionally client-specific.
- If a local placement decision is needed in this workspace, use `.agents/skills` conventions.
- Do not rely on network access, installed packages, or interactive shells unless stated in `compatibility` or the body.
- Keep client-specific configuration in optional files only when the target client needs them.

## Creation Checklist

Before writing files, confirm or infer:

- Skill name and directory.
- Repeatable job and scope boundary.
- Trigger contexts and near-miss exclusions.
- Required inputs, outputs, tools, and source material.
- Whether scripts, references, assets, or evals are justified.
