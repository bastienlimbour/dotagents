# Naming and discovery

Read this file ONLY when designing `name`, `description`, and discovery boundaries.

The frontmatter drives skill activation. Put it at the top of `SKILL.md` and include both `name` and `description`.

## `name`

Rules:

- 1-64 characters
- lowercase letters, digits, and single hyphens only
- no leading, trailing, or consecutive hyphens
- must match the skill's root directory name exactly

Good (gerund):

- `processing-pdfs`
- `analyzing-spreadsheets`
- `writing-documentation`
- `reviewing-pull-requests`

Acceptable (noun):

- `pdf-processing`
- `spreadsheet-analysis`

Acceptable (action):

- `process-pdfs`
- `analyze-spreadsheets`

Be consistent within a skill collection.

Avoid vague names like `helper`, `utils`, `tools`, `documents`, or `data`.

## `description`

Rules:

- 1-1024 characters
- describe what the skill does
- describe when to use it
- include matching keywords
- write in third person
- do not include workflows, long caveats, or examples

`description` is the selection signal. It must help the agent pick this skill over many nearby skills.

Good:

- `Extracts text and tables from PDF files, fills forms, and merges documents. Use when working with PDF files or when the user mentions PDFs, forms, or document extraction.`
- `Generates commit messages from git diffs. Use when committing code or when the user asks for help writing a commit message or reviewing staged changes.`

Bad:

- `Helps with documents`
- `Processes data`
- `Does stuff with files`
- `I can help you process Excel files`

## Safety

- Do not use XML angle brackets (`<`, `>`) in YAML frontmatter

## Boundaries

State exclusions when nearby skills could overlap. Keep the short version in `description`. If needed, expand in `SKILL.md`:

```markdown
## When to use

**Use this skill when:**

- Working with PDF files
- User mentions PDFs, forms, or extraction

**Do NOT use this skill for:**

- Microsoft Word documents
- Non-PDF document work
```
