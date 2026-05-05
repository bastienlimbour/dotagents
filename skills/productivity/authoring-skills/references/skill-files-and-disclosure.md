# Skill files and disclosure

Read this file ONLY when deciding what stays in `SKILL.md` and what moves into bundled files.

## Keep the main file focused

`SKILL.md` is the entry point. Put the core workflow there, then move rare detail out.

## When to split content

Split content when:

- `SKILL.md` is getting long or noisy
- the skill covers distinct subdomains
- domain-specific material can be separated by feature or dataset
- advanced material is rarely needed
- a checklist or schema is too large to keep inline

## Where to put extra detail

- `references/`: long workflows, domain rules, schemas, checklists
- `scripts/`: deterministic operations, validation, repeatable transforms
- `assets/`: templates, sample files, static resources

Add scripts only when executable code is more reliable than natural-language instructions.

## Progressive disclosure rules

- Reference bundled files directly from `SKILL.md`.
- Keep references one level deep from `SKILL.md`.
- Say when to load each file.
- For workflow-based skills that rely on multiple reference files, reference the file at the point of use.
- Avoid a separate catch-all reference navigation section unless the skill is primarily a reference index (reference-based).
- Use relative paths from the skill root.

Good:

```markdown
- For API errors, read [api-errors.md](references/api-errors.md).
- Run `python scripts/validate.py output.json` before finalizing.
```

Bad:

```text
SKILL.md -> references/advanced.md -> references/api.md
```

## Naming and structure

- Use descriptive file names.
- Avoid placeholder names like `doc-2.md` or `misc.md`.
- Add a table of contents when a reference file grows past ~100 lines.

## Iterate on file layout

- If the agent keeps missing a file, make the link from `SKILL.md` more explicit.
- If the agent keeps reading the same reference file, move the most-used part into `SKILL.md`.

## Example split

```text
my-skill/
├── SKILL.md
├── references/
│   ├── api-errors.md
│   └── output-format.md
├── scripts/
│   └── validate-output.py
└── assets/
    └── template.md
```
