# Skill content design

Design guidance for writing the Markdown body of `SKILL.md` and organizing its bundled resources. Use this during Step 3 (designing the skill content).

## Table of contents

- [SKILL.md body](#skillmd-body)
- [Context optimization](#context-optimization)
- [Calibrating control](#calibrating-control)
- [Progressive disclosure patterns](#progressive-disclosure-patterns)
- [Organizing reference files](#organizing-reference-files)
- [Workflows and feedback loops](#workflows-and-feedback-loops)
- [Common patterns](#common-patterns)
- [Content guidelines](#content-guidelines)

## SKILL.md body

Choose the simplest body type that reliably solves the task:

- **Simple text instruction**: Best for simple tasks that can be described in a few sentences.
- **Workflow-based**: Best for multi-step processes.
- **Task-based**: Best for tool collections or grouped capabilities.
- **Reference-based**: Best for standards, specifications, and domain knowledge.

There are no format restrictions for the `SKILL.md` body. Feel free to mix, adapt, or combine the above body types as needed to match the task requirements.

Use the sections that fit the skill. Common useful sections you can pick from are:

- **Overview** (1-2 sentences explaining what this skill does and why it matters)
- **When to use** (list 2-5 use cases for using this skill and 2-5 use cases for when not to use it)
- **Quick start** (the shortest path to value)
- **Process / Workflow / Steps** (for more complex workflows with numbered steps or phases)
- **[Specific task / use case / pattern]** (detailed guidance for a specific task, use case, or pattern)
- **Rules** (defaults, constraints, exceptions, rules of thumb)
- **Output** (the exact shape of the expected output, artifact, format, schema, or length)
- **Troubleshooting** (common errors, causes, and fixes)
- **Gotchas** (environment-specific facts that defy reasonable assumptions)
- **Verification / Validation** (how to verify the output is correct)

The body is a prompt. Apply prompt engineering best practices. It should answer: "Now that this skill has triggered, what should the agent do first, and where should it go next?"

## Context optimization

The context window is shared with the system prompt, conversation history, other active skills, and the user's request. Every token in a skill competes for the agent's attention with everything else in that window.

### Only add missing or unknown context

Only add context the agent doesn't already have or is unlikely to already know.

**Default assumption: the agent is already highly capable.** Challenge each piece of information:

- Does the agent really need this explanation?
- Does the agent need this to succeed?

**Prefer concise examples over verbose explanations:**

**Good example** — Concise (~50 tokens):

````markdown
## Extract PDF text

Use pdfplumber for text extraction:

```python
import pdfplumber

with pdfplumber.open("file.pdf") as pdf:
    text = pdf.pages[0].extract_text()
```
````

**Bad example** — Too verbose (~150 tokens):

```markdown
## Extract PDF text

PDF (Portable Document Format) files are a common file format...
There are many libraries available for PDF processing, but pdfplumber is
recommended because... First, you'll need to install it using pip...
```

### Aim for moderate detail

Favor concise, stepwise guidance over exhaustive documentation. Overly detailed skills can confuse the agent and distract from the main task. Include a focused example and leave room for the agent's own judgment on edge cases rather than documenting every possibility.

### Use progressive disclosure for large skills

Keep `SKILL.md` focused — under 500 lines, featuring only essential instructions. Move detailed guides and reference material to separate `references/` files. Direct the agent to load specific files only when needed (e.g., "See `references/api-errors.md` if the API returns a non-200 status code") rather than referencing all details up front. This helps agents use extra context only when relevant, improving efficiency and clarity.

## Calibrating control

### Set appropriate degrees of freedom

Match instruction specificity to how fragile or variable the task is.

**High freedom** (text-based instructions) — multiple valid approaches, context-dependent decisions:

```markdown
## Code review process

1. Check all database queries for SQL injection (use parameterized queries)
2. Verify authentication checks on every endpoint
3. Look for race conditions in concurrent code paths
4. Confirm error messages don't leak internal details
```

**Low freedom** (specific scripts, few or no parameters) — fragile operations, consistency critical, specific sequence required:

````markdown
## Database migration

Run exactly this sequence:

```bash
python scripts/migrate.py --verify --backup
```

Do not modify the command or add additional flags.
````

Most skills have a mix. Calibrate each part independently. Do not over-constrain exploratory work, and do not under-specify dangerous work.

### Provide defaults, not menus

Provide one default approach with an escape hatch for edge cases, not a menu of alternatives:

**Bad example** — too many options (confusing):

```markdown
You can use pypdf, pdfplumber, PyMuPDF, or pdf2image
```

**Good example** — provide a default and an escape hatch:

````markdown
Use pdfplumber for text extraction:

```python
import pdfplumber
```

For scanned PDFs requiring OCR, use pdf2image with pytesseract instead.
````

### Favor procedures over declarations

A skill should teach the agent *how to approach* a class of problems, not *what to produce* for a specific instance. Procedures generalize; specific answers don't.

**Bad example** — specific answer, only useful for a single task:

```markdown
Join the `orders` table to `customers` on `customer_id`, filter where
`region = 'EMEA'`, and sum the `amount` column.
```

**Good example** — reusable method, works for any analytical query:

```markdown
1. Read the schema from `references/schema.yaml` to find relevant tables
2. Join tables using the `_id` foreign key convention
3. Apply filters from the user's request as WHERE clauses
4. Aggregate numeric columns as needed
```

Specific details like output format templates and constraints ("never output PII") are still valuable — the *approach* should generalize even when individual details are specific.

## Progressive disclosure patterns

`SKILL.md` serves as a table of contents pointing agents to detailed materials as needed.

### Pattern 1 — High-level guide with references

````markdown
# PDF Processing

## Quick start

Extract text with pdfplumber:
```python
import pdfplumber
with pdfplumber.open("file.pdf") as pdf:
    text = pdf.pages[0].extract_text()
```

## Advanced features

**Form filling**: See [forms.md](references/forms.md) for complete guide
**API reference**: See [api.md](references/api.md) for all methods
````

The agent loads `references/*.md` only when needed.

### Pattern 2 — Domain-specific organization

Split by domain to avoid loading irrelevant context:

```text
bigquery-skill/
├── SKILL.md (overview and navigation)
└── reference/
    ├── finance.md (revenue, billing metrics)
    ├── sales.md (opportunities, pipeline)
    └── product.md (usage analytics)
```

````markdown
# BigQuery Data Analysis

## Available datasets

**Finance**: Revenue, ARR, billing → See [finance.md](reference/finance.md)
**Sales**: Opportunities, pipeline, accounts → See [sales.md](reference/sales.md)
**Product**: API usage, features, adoption → See [product.md](reference/product.md)
````

When the user asks about revenue, the agent reads only `reference/finance.md`.

### Pattern 3 — Conditional details

Show basic content and link to more detailed reference files when needed:

```markdown
# DOCX Processing

## Creating documents

Use docx-js for new documents. See [DOCX-JS.md](DOCX-JS.md).

## Editing documents

For simple edits, modify the XML directly.

**For tracked changes**: See [REDLINING.md](REDLINING.md)
**For OOXML details**: See [OOXML.md](OOXML.md)
```

## Organizing reference files

### When to add scripts

Add utility scripts when:

- The operation is deterministic (validation, formatting).
- The same code would be generated repeatedly.
- Errors need explicit handling.

### When to split files

Split into separate files when:

- `SKILL.md` exceeds 500 lines
- Content has distinct domains (e.g. finance vs sales schemas)
- Advanced features are rarely needed (e.g. rarely used API methods)
- Checklists are long enough to justify separate files (>= 15 checklist items)

### Keep references one level deep from `SKILL.md`

Deeply nested references (A → B → C) cause agents to partially read files or miss content:

**Bad example** — too deep:

```text
In SKILL.md : "See references/advanced.md"
In references/advanced.md : "See references/api-reference.md"
In references/api-reference.md : relevant information
```

**Good example** — flat:

```markdown
# SKILL.md
**Basic usage**: [inline instructions]
**Advanced features**: See [advanced.md](references/advanced.md)
**API reference**: See [api-reference.md](references/api-reference.md)
```

### Avoid vague file names

Use descriptive names (`form-validation-rules.md`, NOT `doc-2.md`).

### Use relative paths from the skill root

When referencing other files in `SKILL.md`:

```markdown
- **API error handling**: See [api-error-handling.md](references/api-error-handling.md)
```

### Add a table of contents

Add a table of contents to reference files longer than ~500 lines so agents can see the full scope with partial reads:

```markdown
# API Reference

## Table of contents
- [Authentication and setup](authentication-and-setup.md)
- [Core methods](core-methods.md)
- [Advanced features](advanced-features.md)
- [Error handling patterns](error-handling-patterns.md)

## Authentication and setup

## Core methods

...
```

## Workflows and feedback loops

### Sequential workflows

Break complex operations into clear steps. For multi-step workflows, provide a checklist — it helps the agent track progress and avoid skipping steps:

```markdown
## PDF form filling workflow

Follow the steps and track your progress with this todolist:

- [ ] Step 1: Analyze the form (run analyze_form.py)
- [ ] Step 2: Create field mapping (edit fields.json)
- [ ] Step 3: Validate mapping (run validate_fields.py)
- [ ] Step 4: Fill the form (run fill_form.py)
- [ ] Step 5: Verify output (run verify_output.py)

**Step 1: Analyze the form**
Run: `python scripts/analyze_form.py input.pdf`
This extracts form fields and their locations, saving to `fields.json`.

**Step 2: Create field mapping**
Edit `fields.json` to add values for each field.

**Step 3: Validate mapping**
...
```

Clear steps prevent agents from skipping critical validation.

### Feedback loops

The pattern **do the work → run validator → fix issues → repeat until validation passes** greatly improves output quality.

```markdown
## Editing workflow

1. Make your edits
2. Run validation: `python scripts/validate.py output/`
3. If validation fails:
   - Review the error message
   - Fix the issues
   - Run validation again
4. Only proceed when validation passes
```

This also works without scripts — use a reference document as the "validator" and have the agent compare against it.

## Common patterns

These are reusable techniques for structuring skill content. Not every skill needs all of them — use the ones that fit the task.

### Gotchas pattern

A list of environment-specific facts that defy reasonable assumptions is often the highest-value content in a skill. These are concrete corrections to mistakes the agent will make without being told otherwise — not generic advice like "handle errors appropriately."

```markdown
## Gotchas

- The `users` table uses soft deletes. Queries must include
  `WHERE deleted_at IS NULL` or results will include deactivated accounts.
- The user ID is `user_id` in the database, `uid` in the auth service,
  and `accountId` in the billing API. All three refer to the same value.
- The `/health` endpoint returns 200 even if the database is down.
  Use `/ready` to check full service health.
```

Keep gotchas in `SKILL.md` where the agent reads them before encountering the situation. When an agent makes a mistake during use, add the correction to the gotchas section — this is one of the most direct ways to improve a skill iteratively.

### Template pattern

Use concrete templates to specify output formats; agents follow them better than prose descriptions. Place short templates inline in `SKILL.md`, and store longer or optional ones in `assets/` and reference as needed.

````markdown
## Report structure

Use this template, adapting sections as needed for the specific analysis:

```markdown
# [Analysis Title]

## Executive summary
[One-paragraph overview of key findings]

## Key findings
- Finding 1 with supporting data
- Finding 2 with supporting data

## Recommendations
1. Specific actionable recommendation
2. Specific actionable recommendation
```
````

You can tell the agent to adapt the template as needed with instructions like "Use this sensible default format — adapt as needed".

### Examples pattern

Provide input/output pairs when output quality depends on seeing examples:

````markdown
## Commit message format

Follow this style: type(scope): brief description, then detailed explanation.

**Example 1:**
Input: Added user authentication with JWT tokens
Output:
```
feat(auth): implement JWT-based authentication

Add login endpoint and token validation middleware
```

**Example 2:**
Input: Fixed bug where dates displayed incorrectly in reports
Output:
```
fix(reports): correct date formatting in timezone conversion

Use UTC timestamps consistently across report generation
```
````

### Conditional workflow pattern

Guide agents through decision points:

```markdown
## Document modification workflow

1. Determine the modification type:
   **Creating new content?** → Follow "Creation workflow" below
   **Editing existing content?** → Follow "Editing workflow" below

2. Creation workflow:
   - Use docx-js library
   - Build document from scratch
   - Export to .docx format

3. Editing workflow:
   - Unpack existing document
   - Modify XML directly
   - Validate after each change
   - Repack when complete
```

If workflows become large, push them into separate reference files and direct the agent to the right one.

## Content guidelines

### Use consistent terminology

Pick one term and stick with it throughout the skill:

- Good: always "API endpoint", always "field", always "extract"
- Bad: mixing "API endpoint" / "URL" / "API route" / "path"

### Avoid time-sensitive information

Don't include information that will become outdated. Instead, describe current and legacy methods without dates:

```markdown
## Current method
Use the v2 API endpoint: `api.example.com/v2/messages`

## Legacy method (deprecated)
The v1 API used `api.example.com/v1/messages` and is no longer supported.
```

### Avoid duplication

Do not duplicate the same instructions or guidelines in both `SKILL.md` and reference files.

### Avoid Windows-style paths

Always use forward slashes for file paths (`scripts/helper.py`, not `scripts\helper.py`).

### Use examples only when they improve judgment

Examples are valuable when they teach format, style, edge-case handling, or decision quality.

Do not add examples that merely restate obvious instructions.
