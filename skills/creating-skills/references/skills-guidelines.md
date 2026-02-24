# Skills Authoring Guidelines

## Core Principles

### Conciseness Is Critical

The context window is shared across the system prompt, conversation history, skills' metadata, and the user request. Every token in your skill competes for space. Only include information the agent does not already know.

**Default assumption: the agent is already highly capable.** Only add context it cannot already infer. For each piece of content, ask:

- "Does the agent already know this?"
- "Does the agent need to know this?"
- "Does this justify its token cost?"

If the answer is no or the information is not essential to the Skill, do not include it in the Skill or consider if it can be combined with other information to reduce token usage.

Prefer concise examples over verbose explanations.

### Degrees of Freedom

Match instruction specificity to task fragility:

- **High freedom** (text instructions): Multiple valid approaches, context-dependent decisions. Example: code review guidelines.
- **Medium freedom** (pseudocode/parameterized scripts): Preferred pattern exists but variation is acceptable. Example: report generation templates.
- **Low freedom** (exact scripts, no parameters): Fragile operations where consistency is critical. Example: database migrations.

## Writing Effective Metadata

### Name

Use lowercase letters, numbers, and hyphens only (max 64 chars).

**Prefer gerund form** (verb + -ing) for clarity:

- `processing-pdfs`, `analyzing-spreadsheets`, `managing-databases`, `handling-errors`, `brainstorming-idea`

**Avoid** vague names (`helper`, `utils`, `tools`) and overly generic names (`documents`, `data`).

### Description

The description is the primary trigger for skill selection. It must clearly state **what** the skill does and **when** to use it. Max 1024 chars.

**Rules:**

- Write in **third person** (the description is injected into the system prompt)
- Be specific and include key terms the user might mention
- Include both capabilities and trigger conditions

**Good:**

```yaml
description: Extract text and tables from PDF files, fill forms, merge documents. Use when working with PDF files or when the user mentions PDFs, forms, or document extraction.
```

**Bad:**

```yaml
description: Helps with documents
```

## Progressive Disclosure

### Keep SKILL.md Lean

- Body under **500 lines** — split into separate files when approaching this limit
- SKILL.md acts as an overview and navigation hub pointing to detailed materials
- Information should live in **either** SKILL.md or reference files, not both

### Organizing Bundled Content

**Pattern 1 — High-level guide with references:**

```markdown
# PDF Processing

## Quick start
[Core code example]

## Advanced features
- **Form filling**: See [forms.md](references/forms.md)
- **API reference**: See [api-ref.md](references/api-ref.md)
```

**Pattern 2 — Domain-specific organization:**

```text
skill-name/
├── SKILL.md (overview + navigation)
└── references/
    ├── finance.md
    ├── sales.md
    └── product.md
```

The agent loads only the relevant domain file based on the user's request.

**Pattern 3 — Conditional details:**

```markdown
## Creating documents
Use library X. See [creation-guide.md](references/creation-guide.md).

## Editing documents
For simple edits, modify directly.
**For tracked changes**: See [redlining.md](references/redlining.md)
```

### Reference File Rules

- **Keep references one level deep** — all reference files must link directly from SKILL.md, not from other reference files
- **Add a table of contents** to reference files longer than 100 lines
- **Name files descriptively**: `form_validation_rules.md` not `doc2.md`
- **Use forward slashes** in all paths: `references/guide.md` not `references\guide.md`

## Workflows and Feedback Loops

### Structured Workflows

Break complex operations into clear sequential steps. For multi-step processes, provide a checklist the agent can track, for example:

````markdown
## Form filling workflow

```
- [ ] Step 1: Analyze the form
- [ ] Step 2: Create field mapping
- [ ] Step 3: Validate mapping
- [ ] Step 4: Fill the form
- [ ] Step 5: Verify output
```

**Step 1: Analyze the form**
Run: `python scripts/analyze_form.py input.pdf`
...
````

### Feedback Loops

Use a validate-fix-repeat pattern for quality-critical tasks:

```markdown
1. Make edits
2. Validate: `python scripts/validate.py output/`
3. If validation fails → fix issues → validate again
4. Only proceed when validation passes
```

## Content Guidelines

- **Avoid time-sensitive information** — don't reference specific dates or version timelines
- **Use consistent terminology** — pick one term per concept and use it throughout
- **Provide a default, not a menu** — recommend one approach; mention alternatives only when the default doesn't apply
- **Use concrete examples** over abstract descriptions

## Common Patterns

### Template Pattern

Provide output structure templates. Match strictness to requirements:

- **Strict** (data formats, APIs): "ALWAYS use this exact structure: ..."
- **Flexible** (reports, analysis): "Here is a sensible default, adapt as needed: ..."

### Examples Pattern

Provide input/output pairs when output quality depends on style:

````markdown
**Example:**
Input: Added user authentication with JWT tokens
Output:
```
feat(auth): implement JWT-based authentication
```
````

### Conditional Workflow Pattern

Guide through decision points:

```markdown
**Creating new content?** → Follow "Creation workflow"
**Editing existing content?** → Follow "Editing workflow"
```

If workflows grow large, move them to separate reference files.

## Skills with Executable Code

### Script Best Practices

- **Handle errors explicitly** in scripts — don't let them fail silently and force the agent to debug
- **Document constants** — no magic numbers without justification
- **Make execution intent clear** in SKILL.md:
  - "Run `analyze.py` to extract fields" (execute)
  - "See `analyze.py` for the extraction algorithm" (read as reference)

### Verifiable Intermediate Outputs

For complex or destructive operations, use a plan-validate-execute pattern:

1. Agent creates a structured plan file (e.g., `changes.json`)
2. Validation script checks the plan
3. Only then apply changes
4. Verify final output

Make validation scripts verbose with specific error messages to help the agent self-correct.

### Dependencies

List all required packages in SKILL.md. Don't assume packages are pre-installed — include installation instructions when relevant.

### MCP Tool References

Use fully qualified names: `ServerName:tool_name` (e.g., `GitHub:create_issue`).

### Security

- **Validate inputs**: Scripts should check that file paths are within expected directories to prevent path traversal.
- **Limit scope**: Scripts should only touch files relevant to the specific task.
- **Avoid obfuscation**: Code should be readable so the agent (and user) can verify safety.

## Evaluation and Iteration

1. **Identify gaps** — run tasks without the skill, document failures
2. **Create evaluations** — build test scenarios that cover those gaps
3. **Write minimal instructions** — only enough to address the gaps
4. **Test with real usage** — observe how agents actually navigate and use the skill
5. **Iterate** — refine based on observed behavior, not assumptions

**Watch for:**

- Missed references (links need to be more prominent)
- Overreliance on certain sections (move that content to SKILL.md)
- Ignored files (may be unnecessary or poorly signaled)
- Unexpected navigation paths (structure may not be intuitive)

## Checklist

### Core Quality

- [ ] Description states what the skill does and when to use it
- [ ] SKILL.md body is under 500 lines
- [ ] Detailed content split into reference files
- [ ] No time-sensitive information
- [ ] Consistent terminology throughout
- [ ] Concrete examples provided
- [ ] References are one level deep from SKILL.md
- [ ] No extraneous files (README, CHANGELOG, etc.)

### Code and Scripts

- [ ] Scripts handle errors explicitly
- [ ] All constants are documented
- [ ] Required packages listed
- [ ] Validation/feedback loops for critical operations
- [ ] Forward slashes in all file paths
