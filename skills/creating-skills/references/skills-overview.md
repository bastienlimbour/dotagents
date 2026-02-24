# Skills Overview

## What Are Skills

Skills are modular, self-contained packages that extend an AI agent's capabilities by providing specialized knowledge, workflows, and tools. They act as on-demand "onboarding guides" for specific domains or tasks, transforming a general-purpose AI agent into a specialist equipped with procedural knowledge, domain expertise, and bundled resources that no AI model can fully possess.

**Key benefits:**

- **Specialize agents** for domain-specific tasks
- **Eliminate repetition** — create once, reuse automatically across conversations
- **Compose capabilities** — combine multiple Skills for complex workflows

### What Skills can provide

- **Specialized workflows**: Multi-step procedures for specific domains
- **Tool integrations**: Instructions for working with specific file formats or APIs
- **Domain expertise**: Company-specific knowledge, schemas, business logic
- **Bundled resources**: Scripts, references, and assets for complex or repetitive tasks

## How Skills Work

Skills leverage a filesystem-based architecture with **progressive disclosure**: content is loaded in stages as needed, not all at once.

### Three-Level Loading

| Level | When Loaded | Cost | Content |
| ------- | ------------ | ------ | --------- |
| **1. Metadata** | Always (at startup) | ~100 tokens | `name` and `description` from YAML frontmatter |
| **2. Instructions** | When skill triggers | <5k tokens | SKILL.md body |
| **3. Resources** | As needed | Effectively unlimited | Bundled files (scripts, references, assets) |

**How it works:**

1. **Startup** — Only metadata (name + description) from all installed skills is loaded into the system prompt. Many skills can coexist without context penalty.
2. **Trigger** — When a request matches a skill's description, the agent reads SKILL.md from the filesystem, bringing instructions into context.
3. **On-demand resources** — If instructions reference other files (references, scripts, assets), the agent reads or executes them only when needed. Scripts produce output without their source code entering context.

This ensures only relevant content occupies the context window at any given time.

## Skill Structure

### Directory Layout

```text
skill-name/
├── SKILL.md              (required — metadata + instructions)
└── Bundled Resources      (optional)
    ├── scripts/           Executable code (Python/Bash/etc.)
    ├── references/        Documentation loaded into context as needed
    └── assets/            Files used in output (templates, icons, fonts, etc.)
```

### SKILL.md (required)

Every SKILL.md has two parts:

**1. YAML Frontmatter** — Discovery metadata, always loaded at startup.

```yaml
---
name: skill-name-here
description: Brief description of what this skill does and when to use it.
---
```

- `name`: Required. Max 64 chars, lowercase letters/numbers/hyphens only.
- `description`: Required. Max 1024 chars. Must describe **what** the skill does and **when** to use it. Written in third person.

**2. Markdown Body** — Instructions and guidance, loaded only when the skill triggers.

```markdown
# Skill Name

## Quick start
[Core workflow and essential instructions]

## Advanced features
- **Feature A**: See [feature-a.md](references/feature-a.md)
- **Feature B**: See [feature-b.md](references/feature-b.md)
```

### Bundled Resources (optional)

#### Scripts (`scripts/`)

Executable code for tasks requiring deterministic reliability or frequently rewritten logic.

- Executed via bash — output enters context, source code does not
- Token-efficient and deterministic
- Example: `scripts/validate_form.py`

#### References (`references/`)

Documentation and reference material loaded into context as needed.

- Database schemas, API docs, domain knowledge, detailed workflow guides
- Keeps SKILL.md lean — move detailed info here, reference it from SKILL.md
- For large files (>10k words), include grep patterns in SKILL.md for targeted lookup

#### Assets (`assets/`)

Files used in output, not loaded into context.

- Templates, images, icons, fonts, boilerplate code
- Example: `assets/logo.png`, `assets/template.pptx`

### What NOT to Include

Do not create extraneous files: README.md, CHANGELOG.md, INSTALLATION_GUIDE.md, etc. A skill should only contain files that directly support the agent's task execution.
