# Content Patterns

Use this reference when writing or restructuring a `SKILL.md` body, references, assets, or progressive disclosure layout.

## Table of Contents

- Write Instructions, Not Documentation
- Scannable Markdown Structure
- Section Purpose
- Match Control To Risk
- Progressive Disclosure
- Useful Patterns
- Anti-Patterns

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

## Scannable Markdown Structure

Use structure as a behavioral tool, not as template compliance. Choose sections that help the agent decide, act, or verify.

Common useful sections:

- `Overview`: 1-2 sentences explaining what the skill does and why it matters.
- `When To Use`: list of task types, symptoms, artifacts, user intents that helps agents and humans decide if this skill applies to the current task; add "when not to use:" for near-miss exclusions that prevent likely false positives.
- `Core Principle`: one governing rule for skills where the main failure mode is easy to state.
- `Workflow`, `Process`, `Steps`, or phase headings: the main sequence the agent follows.
- `Examples` or `Templates`: concrete patterns when format, style, or edge cases matter.
- `Defaults` or `Rules`: short durable guidance the agent should apply throughout.
- `Common Rationalizations`: table of excuses agents use to skip important steps, paired with rebuttals; use only for process skills where agents are likely to skip important steps.
- `Red Flags`: observable signs that the skill is being violated; use only when observable failure patterns help (e.g. self-monitoring, code reviews, or audits).
- `Gotchas`: likely mistakes and non-obvious facts when they are relevant.
- `Output`: the expected output format and structure; useful for skills that produce structured output such as JSON, Markdown, tables, or code.
- `Verification`: the exit criteria; a checklist the agent uses to confirm the skill's process is complete; valuable for quality-critical, executable, or multi-step skills.

**Do not force every skill into this shape.** Small skills can be one short instruction block. A section earns its place only if it changes behavior.

Main workflows do not need branded names. Use a memorable name only when it clarifies behavior. Otherwise use `Workflow`, `Process`, `Steps`, or descriptive phase headings.

Prefer phase headings over deeply nested numbered lists when a workflow has many steps. Phase headings are easier to scan and easier to resume after interruption.

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

In `SKILL.md`, add clear when-to-load guidance for each file:

```markdown
When the API returns a non-200 response, read `references/api-errors.md`.
```

Avoid reference chains where `SKILL.md` points to `advanced.md` and `advanced.md` points to `details.md`. Link important files directly from `SKILL.md`.

For reference files over 100 lines, add a short table of contents at the top.

## Useful Patterns

Use checklists for workflows with sequential steps:

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

Use tables when information is comparison-heavy:

```markdown
| Situation | Default action |
|---|---|
| Rare detail | Move to `references/` |
| Repeated deterministic work | Consider `scripts/` |
```

Use examples when format, style, edge cases, or tool use are hard to describe in prose.

Use templates only when the output structure matters. Mark whether the template is strict or adaptable.

Use `Common Rationalizations` only when the skill protects against predictable shortcuts. Pair the excuse with a concrete correction:

```markdown
## Common Rationalizations
| Rationalization | Reality |
|---|---|
| Excuse agents use to skip steps | Why the excuse is wrong |
```

Use `Red Flags` only when the skill has observable misuse patterns that the agent can catch while working.

## Anti-Patterns

- Long generic best-practice prose.
- A fixed section template applied to every skill.
- Many equal options without a default.
- Deeply nested reference chains.
- Windows-style paths.
- Time-sensitive instructions in the main path.
- Instructions that conflict with the user's current task or platform.
- Bundled files that are never referenced from `SKILL.md`.
