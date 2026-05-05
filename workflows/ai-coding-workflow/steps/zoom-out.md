# Zoom Out

**Skill name:** `zoom-out`

**Step type:** On-demand step.

**Role:** Map how a scoped code area fits into the system before editing it.

**When to use:** Unknown code area, stack trace crossing multiple modules, imminent refactor, domain onboarding, uncertainty about callers, data flow, seams, or risks.

**Possible inputs:** File, directory, symbol, stack trace, issue, PRD, task spec, modification intent, `CONTEXT.md`, `CONTEXT-MAP.md`, ADRs, relevant tests.

**Process:**

1. Define the area and modification intent before mapping.
2. Read durable vocabulary and decisions when they exist.
3. Map relevant modules, callers, callees, data flows, seams, adapters, and ownership.
4. Locate relevant tests or verification seams when useful.
5. Explain responsibilities in domain language, not just filenames.
6. Flag coupling, ambiguity, risk areas, and remaining unknowns.
7. Recommend the next step: `Build`, `Grill With Docs`, `Tech Design`, `Diagnose`, or `Improve Codebase Architecture`.

**Rules:**

- `Zoom Out` reduces modification risk; implementation belongs in `Build`.
- Limit exploration to the requested intent or affected area.
- Do not list unrelated files just because they were discovered.
- Use durable vocabulary when available.
- Route structural concerns to `Improve Codebase Architecture` instead of solving them inside the map.

**Output:** Concise area map with responsibilities, flows, seams, risks, unknowns, and recommended next step.

**Output location:** Check `.agents/workflow/output-locations.md` when it exists. Recommended default: session summary. If it supports an active initiative, publish a tracker comment or local `.initiatives/<initiative>/` note only when the map will be reused.

**Output template:**

```markdown
## Area Map

## Scope Studied
<!-- Required. Paragraph, 1-3 sentences: file, directory, symbol, flow, or modification intent. -->
<Scope studied.>

## Responsibilities
<!-- Required. Bullet list: domain responsibility and owning module/code area. -->
- **<Module or area>:** <Domain responsibility.>

## Relevant Flows
<!-- Required when flow matters. Bullet list: caller -> module -> callee, data flow, or lifecycle. -->
- <Caller or event> -> <module/area> -> <callee or outcome.>

## Seams & Interfaces
<!-- Conditional. Bullet list: interface, adapter, boundary, test seam, or invariant to preserve. -->
- <Seam, interface, boundary, or invariant.>

## Verification Seams
<!-- Conditional. Bullet list: tests, commands, fixtures, browser path, or missing signal. -->
- <Verification seam.>

## Risks & Unknowns
<!-- Conditional. Bullet list: coupling, ambiguity, ownership gap, or confidence note. -->
- <Risk, unknown, or confidence note.>

## Recommended Next Step
<!-- Required. One sentence: Build / Grill With Docs / Tech Design / Diagnose / Improve Codebase Architecture, with rationale. -->
<Recommended next step and rationale.>
```

**Possible sizes:** Micro-map for one symbol or stack trace; standard map for one feature area; full map for a sensitive refactor or unfamiliar subsystem.

**Verification:** The map explains how the area fits into the system, what seams to preserve, what feedback exists, and what remains unknown without listing unrelated files.

**Human gate:** Confirm that the map matches the intent before sensitive modification.
