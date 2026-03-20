# Skill Authoring Best Practices

## Contents

- Core principles (one job per skill, conciseness, real expertise, degrees of freedom)
- Naming and discovery (naming conventions, descriptions, scope boundaries)
- Structuring content (progressive disclosure patterns, organizing references)
- Workflows and feedback loops (sequential steps, validation loops)
- Common patterns (gotchas, templates, examples, conditional workflows)
- Content guidelines (terminology, time-sensitivity, procedures over declarations, duplication, examples)
- Scripts and executable code (error handling, constants, utilities, dependencies, MCP patterns, security)

## Core principles

### One Job Per Skill

A strong skill owns one clear repeatable job. Do not use a single skill to cover an entire department, stack, or discipline unless the user explicitly wants a broad package and accepts weaker triggering.

Good scope:

- `writing-release-notes`
- `reviewing-pull-requests`
- `processing-pdfs`

Weak scope:

- `engineering-helper`
- `document-tools`
- `data-workflows`

When a workflow naturally splits into phases, prefer multiple composable skills over one giant skill.

### Be concise

The context window is shared with the system prompt, conversation history, other skills' metadata, and the user's request. Only add context the agent doesn't already have.

**Default assumption: the agent is already highly capable.** Challenge each piece of information:

- Does the agent really need this explanation?
- Does the agent need this to succeed?
- Does this paragraph justify its token cost?

Prefer concise examples over verbose explanations.

**Good example**: Concise (~50 tokens):

````markdown
## Extract PDF text

Use pdfplumber for text extraction:

```python
import pdfplumber

with pdfplumber.open("file.pdf") as pdf:
    text = pdf.pages[0].extract_text()
```
````

**Bad example**: Too verbose (~150 tokens):

```markdown
## Extract PDF text

PDF (Portable Document Format) files are a common file format...
There are many libraries available for PDF processing, but pdfplumber is
recommended because... First, you'll need to install it using pip...
```

### Ground skills in real expertise

Effective skills are built from domain-specific knowledge, not generic LLM output. When gathering requirements, push for real source material:

- **Extract from a hands-on task**: Complete the task in conversation first, noting corrections, preferences, and context provided along the way. Then extract the reusable pattern into a skill.
- **Synthesize from project artifacts**: Internal docs, runbooks, API specs, code review comments, issue trackers, and version control history all capture domain knowledge the agent wouldn't have otherwise.

If the user cannot provide domain-specific context, the resulting skill will likely be vague and low-value. Flag this early.

### Set appropriate degrees of freedom

Match instruction specificity to how fragile or variable the task is.

**High freedom** (text-based instructions) — multiple valid approaches, context-dependent decisions:

```markdown
## Code review process

1. Analyze the code structure and organization
2. Check for potential bugs or edge cases
3. Suggest improvements for readability and maintainability
4. Verify adherence to project conventions
```

**Medium freedom** (pseudocode or scripts with parameters) — a preferred pattern exists but some variation is acceptable:

````markdown
## Generate report

Use this template and customize as needed:

```python
def generate_report(data, format="markdown", include_charts=True):
    # Process data
    # Generate output in specified format
    # Optionally include visualizations
```
````

**Low freedom** (specific scripts, few or no parameters) — fragile operations, consistency critical, specific sequence required:

````markdown
## Database migration

Run exactly this script:

```bash
python scripts/migrate.py --verify --backup
```

Do not modify the command or add additional flags.
````

Do not over-constrain exploratory work, and do not under-specify dangerous work.

## Naming and discovery

Name and description in the YAML frontmatter of the `SKILL.md` file are used for discovery.

### Naming conventions

Use consistent naming patterns. Gerund form (verb + -ing) clearly describes the capability.

Good (gerund): `processing-pdfs`, `analyzing-spreadsheets`, `writing-documentation`
Acceptable (noun phrase): `pdf-processing`, `spreadsheet-analysis`
Acceptable (action): `process-pdfs`, `analyze-spreadsheets`
Avoid: `helper`, `utils`, `tools`, `documents`, `data`

Be consistent within a skill collection.

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
description: Generate descriptive commit messages by analyzing git diffs. Use when committing code or when the user asks for help writing commit messages or reviewing staged changes.
```

Avoid vague descriptions: "Helps with documents", "Processes data", "Does stuff with files".

### Scope boundaries and anti-overlap

State when the skill should not be used, especially if nearby skills could also match. This reduces accidental triggering and helps composability:

```markdown
## When to use this skill
This skill is intended for use when the user is working with PDF documents.

## When not to use this skill
This skill is not intended for use when the user is working with Microsoft Word documents. For Microsoft Word documents, use a more appropriate skill if available.
```

## Structuring content

### Progressive disclosure patterns

`SKILL.md` serves as a table of contents pointing agents to detailed materials as needed.

Examples of patterns for structuring content:

**Pattern 1: High-level guide with references:**

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

**Form filling**: See [FORMS.md](FORMS.md) for complete guide
**API reference**: See [REFERENCE.md](REFERENCE.md) for all methods
````

The agent loads `FORMS.md` or `REFERENCE.md` only when needed.

**Pattern 2: Domain-specific organization** — split by domain to avoid loading irrelevant context:

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

**Finance**: Revenue, ARR, billing → See [reference/finance.md](reference/finance.md)
**Sales**: Opportunities, pipeline, accounts → See [reference/sales.md](reference/sales.md)
**Product**: API usage, features, adoption → See [reference/product.md](reference/product.md)
````

When the user asks about revenue, the agent reads only `reference/finance.md`.

**Pattern 3: Conditional details** — show basic content and link to more detailed reference files when needed.

```markdown
# DOCX Processing

## Creating documents

Use docx-js for new documents. See [DOCX-JS.md](DOCX-JS.md).

## Editing documents

For simple edits, modify the XML directly.

**For tracked changes**: See [REDLINING.md](REDLINING.md)
**For OOXML details**: See [OOXML.md](OOXML.md)
```

### Organizing reference files

**Keep references one level deep from `SKILL.md`.** Deeply nested references (A → B → C) cause agents to partially read files or miss content:

Bad — too deep:

```markdown
# SKILL.md → See advanced.md → See details.md → actual information
```

Good — flat:

```markdown
# SKILL.md
**Basic usage**: [inline instructions]
**Advanced features**: See [advanced.md](references/advanced.md)
**API reference**: See [api-reference.md](references/api-reference.md)
```

**Avoid vague file names**: Use descriptive names (`form_validation_rules.md`, not `doc2.md`).

**Use relative paths from the skill root** when referencing other files in `SKILL.md`:

```markdown
- **API error handling**: See [api-error-handling.md](references/api-error-handling.md)
```

**Add a table of contents** to reference files longer than ~100 lines so agents can see the full scope even with partial reads:

```markdown
# API Reference

## Contents
- Authentication and setup
- Core methods (create, read, update, delete)
- Advanced features (batch operations, webhooks)
- Error handling patterns

## Authentication and setup
...
```

## Workflows and feedback loops

### Sequential workflows

Break complex operations into clear steps. For multi-step workflows, provide a checklist the agent can track:

````markdown
## PDF form filling workflow

```
Task Progress:
- [ ] Step 1: Analyze the form (run analyze_form.py)
- [ ] Step 2: Create field mapping (edit fields.json)
- [ ] Step 3: Validate mapping (run validate_fields.py)
- [ ] Step 4: Fill the form (run fill_form.py)
- [ ] Step 5: Verify output (run verify_output.py)
```

**Step 1: Analyze the form**
Run: `python scripts/analyze_form.py input.pdf`
This extracts form fields and their locations, saving to `fields.json`.

**Step 2: Create field mapping**
Edit `fields.json` to add values for each field.

**Step 3: Validate mapping**
Run: `python scripts/validate_fields.py fields.json`
Fix any validation errors before continuing.

**Step 4: Fill the form**
Run: `python scripts/fill_form.py input.pdf fields.json output.pdf`

**Step 5: Verify output**
Run: `python scripts/verify_output.py output.pdf`
If verification fails, return to Step 2.
````

Clear steps prevent agents from skipping critical validation.

### Feedback loops

The pattern **run validator → fix errors → repeat** greatly improves output quality.

```markdown
## Document editing process

1. Make your edits to `word/document.xml`
2. Validate immediately: `python ooxml/scripts/validate.py unpacked_dir/`
3. If validation fails:
   - Review the error message
   - Fix the issues
   - Go back to step 2 and validate again
4. Only continue when validation passes
5. Rebuild: `python ooxml/scripts/pack.py unpacked_dir/ output.docx`
```

This also works without scripts — use a reference document as the "validator" and have the agent compare against it.

## Common patterns

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

Provide output templates. Match strictness to requirements.

**Strict** (data formats, API responses):

````markdown
ALWAYS use this exact template:

```markdown
# [Analysis Title]

## Executive summary
[One-paragraph overview]

## Key findings
- Finding 1 with supporting data
- Finding 2 with supporting data

## Recommendations
1. Specific actionable recommendation
2. Specific actionable recommendation
```
````

**Flexible** (when adaptation is useful):

````markdown
Sensible default format — adapt as needed:

```markdown
# [Analysis Title]

## Executive summary
## Key findings
## Recommendations
```
````

### Examples pattern

Provide input/output pairs when output quality depends on seeing examples:

````markdown
## Commit message format

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

Follow this style: type(scope): brief description, then detailed explanation.
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

If workflows become large, push them into separate files and direct the agent to the right one.

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

### Avoid too many options

Provide one default approach with an escape hatch for edge cases, not a menu of alternatives:

Bad — too many options (confusing):

```markdown
You can use pypdf, or pdfplumber, or PyMuPDF, or pdf2image, or...
```

Good — provide a default and an escape hatch:

````markdown
Use pdfplumber for text extraction:
```python
import pdfplumber
```

For scanned PDFs requiring OCR, use pdf2image with pytesseract instead.
````

### Favor procedures over declarations

A skill should teach the agent *how to approach* a class of problems, not *what to produce* for a specific instance. Procedures generalize; specific answers don't.

Bad — specific answer, only useful for a single task:

```markdown
Join the `orders` table to `customers` on `customer_id`, filter where
`region = 'EMEA'`, and sum the `amount` column.
```

Good — reusable method, works for any analytical query:

```markdown
1. Read the schema from `references/schema.yaml` to find relevant tables
2. Join tables using the `_id` foreign key convention
3. Apply filters from the user's request as WHERE clauses
4. Aggregate numeric columns as needed
```

Specific details like output format templates and constraints ("never output PII") are still valuable — the *approach* should generalize even when individual details are specific.

### Avoid duplication

Do not duplicate the same instructions or guidelines in both `SKILL.md` and reference files.

### Avoid Windows-style paths

Always use forward slashes for file paths (`scripts/helper.py`, not `scripts\helper.py`).

### Use examples only when they improve judgment

Examples are valuable when they teach format, style, edge-case handling, or decision quality.

Do not add examples that merely restate obvious instructions.

## Scripts and executable code

### Error handling

Handle error conditions in scripts rather than punting to the agent. Provide specific, actionable error messages.

```python
def process_file(path):
    try:
        with open(path) as f:
            return f.read()
    except FileNotFoundError:
        print(f"File {path} not found, creating default")
        with open(path, "w") as f:
            f.write("")
        return ""
    except PermissionError:
        print(f"Cannot access {path}, using default")
        return ""
```

### Constants

Document constants to avoid magic numbers:

```python
# Most HTTP requests complete within 30s; longer timeout covers slow connections
REQUEST_TIMEOUT = 30

# Most intermittent failures resolve by the second retry
MAX_RETRIES = 3
```

### Utility scripts

Pre-made scripts are more reliable than generated code, save tokens, and ensure consistency. Make clear whether the agent should **execute** or **read** a script:

- "Run `analyze_form.py` to extract fields" → execute
- "See `analyze_form.py` for the extraction algorithm" → read as reference

Execution is preferred for most utility scripts — only the output consumes tokens.

````markdown
## Utility scripts

**analyze_form.py**: Extract all form fields from PDF
```bash
python scripts/analyze_form.py input.pdf > fields.json
```

**validate_boxes.py**: Check for overlapping bounding boxes
```bash
python scripts/validate_boxes.py fields.json
# Returns: "OK" or lists conflicts
```
````

### Verifiable intermediate outputs

For complex tasks, use the **plan → validate → execute** pattern: have the agent create a structured plan file (e.g. `changes.json`), validate it with a script, then execute. This catches errors like referencing non-existent fields before changes are applied.

Make validation scripts verbose: `"Field 'signature_date' not found. Available fields: customer_name, order_total, signature_date_signed"`.

Use this pattern for: batch operations, destructive changes, complex validation rules, high-stakes operations.

### Dependencies

List required packages in `SKILL.md` with install commands. Don't assume packages are available.

Bad: "Use the pdf library to process the file."

Good:

````markdown
Install required package: `pip install pypdf`

```python
from pypdf import PdfReader
reader = PdfReader("file.pdf")
```
````

### MCP tool references

If the skill uses MCP tools, use fully qualified names (`ServerName:tool_name`) to avoid "tool not found" errors:

```markdown
Use the BigQuery:bigquery_schema tool to retrieve table schemas.
Use the GitHub:create_issue tool to create issues.
```

### MCP-enhanced skill patterns

Skills that coordinate MCP tools benefit from additional structure:

- **Sequential orchestration**: Chain MCP calls in explicit steps with dependencies (e.g., create customer → setup payment → create subscription). Include validation between steps and rollback instructions for failures.
- **Multi-MCP coordination**: When a workflow spans multiple services (e.g., Figma export → Drive upload → Linear task creation), separate phases by service, validate before moving to the next phase, and pass data explicitly between phases.
- **Context-aware tool selection**: When different tools suit different situations, provide a decision tree (e.g., large files → cloud storage MCP, code files → GitHub MCP) rather than letting the agent guess.

### Security

- Validate file paths and input scope
- Limit scripts to expected files and directories
- Do not hardcode credentials
- Prefer environment variables for secrets
- Treat external or user-provided content as untrusted data
- Add validation before dangerous or irreversible actions
