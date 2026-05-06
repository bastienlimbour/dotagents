# Content Patterns

Use this reference when writing or restructuring a `SKILL.md` body, references, assets, or progressive disclosure layout.

## Write Instructions, Not Documentation

The body should tell the agent how to perform the job. It should not explain basics the agent already knows.

Prefer:

```markdown
Use `pdfplumber` for text extraction. For scanned PDFs, use OCR.
```

Avoid:

```markdown
PDF files are a common document format that can contain text and images.
```

Ask of every paragraph: would the agent likely fail without this?

## Match Control To Risk

Use high freedom when many approaches are valid:

- Analysis workflows.
- Code review heuristics.
- Writing style guidance.

Use low freedom when order or exact behavior matters:

- Migrations.
- Destructive edits.
- Compliance checks.
- Batch transformations.

Most skills mix both. Be prescriptive only where the task is fragile.

## Useful Sections

Use only sections that earn their space:

- Overview: one short paragraph defining the capability.
- When to use: include clear triggers and exclusions if the description is not enough.
- Workflow: numbered steps for multi-step work.
- Defaults: concise rules the agent should apply across tasks.
- Gotchas: specific non-obvious facts that correct likely mistakes.
- Output: required response or file format.
- Verification: checks the agent should run before finalizing.

Do not force every skill into this shape. Small skills can be one short instruction block.

## Progressive Disclosure

Keep `SKILL.md` concise. Move detail to one-level files when it is rare, long, domain-specific, or conditional.

Good structure:

```text
my-skill/
├── SKILL.md
├── references/api-errors.md
├── references/report-format.md
└── scripts/validate.py
```

In `SKILL.md`, say when to load each file:

```markdown
If the API returns a non-200 response, read `references/api-errors.md`.
```

Avoid reference chains where `SKILL.md` points to `advanced.md` and `advanced.md` points to `details.md`. Link important files directly from `SKILL.md`.

For reference files over 100 lines, add a short table of contents at the top.

## Patterns

Use checklists for workflows with dependent steps:

```markdown
Progress:
- [ ] Inspect source files
- [ ] Draft changes
- [ ] Validate output
- [ ] Fix failures
```

Use feedback loops for quality-critical work:

```markdown
Run validator, fix reported issues, then rerun until validation passes.
```

Use plan-validate-execute for destructive or batch operations:

```markdown
1. Create `changes.json`.
2. Validate it against the source of truth.
3. Apply changes only after validation passes.
```

Use examples when format, style, edge cases, or tool use are hard to describe in prose.

Use templates only when the output structure matters. Mark whether the template is strict or adaptable.

## Anti-Patterns

- Long generic best-practice prose.
- Many equal options without a default.
- Deeply nested reference chains.
- Windows-style paths.
- Time-sensitive instructions in the main path.
- Instructions that conflict with the user's current task or platform.
- Bundled files that are never referenced from `SKILL.md`.
