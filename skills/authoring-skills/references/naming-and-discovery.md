# Naming and discovery best practices

The YAML frontmatter of `SKILL.md` drives skill discovery. This file is the single source of truth for everything that goes into the frontmatter: `name`, `description`, and security rules, plus the scope boundaries that support them.

The frontmatter must appear at the top of `SKILL.md` and must contain both `name` and `description`.

## Name

### Name rules

- Non empty, 1-64 characters
- Lowercase, alphanumeric characters and hyphens only (`a-z`, `0-9`, `-`)
- No leading, trailing, or consecutive hyphens
- Must match the skill directory name exactly

Valid: `pdf-processing`, `data-analysis`, `code-review`

Invalid: `PDF-Processing` (uppercase), `-pdf` (leading hyphen), `pdf--processing` (consecutive hyphens)

### Naming conventions

Use consistent naming patterns. Gerund form (verb + -ing) clearly describes the capability.

- Good (gerund): `processing-pdfs`, `analyzing-spreadsheets`, `writing-documentation`
- Acceptable (noun phrase): `pdf-processing`, `spreadsheet-analysis`
- Acceptable (action): `process-pdfs`, `analyze-spreadsheets`
- Avoid: `helper`, `utils`, `tools`, `documents`, `data`

Be consistent within a skill collection.

## Description

### Description rules

- Non empty, 1-1024 characters
- Describes what the skill does and when to use it
- Includes keywords that help agents match tasks to this skill
- Written in third person

Do NOT put long workflows, caveats, or examples in description.

### Writing effective descriptions

The `description` field is the primary trigger for agents to choose which skill to activate from potentially hundreds of available skills. It must provide enough signal for selection, and clearly state what the skill does and when to use it.

**Write in third person.** The description is injected into the system prompt; inconsistent point-of-view causes discovery problems.

- Good: "Processes Excel files and generates reports"
- Bad: "I can help you process Excel files"
- Bad: "You can use this to process Excel files"

**Be specific and include trigger keywords:**

```yaml
description: Extract text and tables from PDF files, fill forms, merge documents. Use when working with PDF files or when the user mentions PDFs, forms, or document extraction.
```

```yaml
description: Generates descriptive commit messages by analyzing git diffs. Use when committing code or when the user asks for help writing commit messages or reviewing staged changes.
```

Avoid vague descriptions: "Helps with documents", "Processes data", "Does stuff with files".

## Scope boundaries and anti-overlap

State when the skill should not be used, especially if nearby skills could also match. This reduces accidental triggering and helps composability. Scope boundaries belong in the `description` (short form) and, when the skill needs more room, in a `When to use` section inside the `SKILL.md` body:

```markdown
## When to use

**Use this skill when:**
- Working with PDF documents
- The user mentions PDFs, forms, or document extraction

**Do NOT use this skill when:**
- Working with Microsoft Word documents
- Working with other document types than PDF
```

## Security restrictions

- No XML angle brackets (`<`, `>`) in frontmatter. Frontmatter appears in the system prompt and could inject instructions.
