---
name: capture
description: Captures long conversations, research sessions, grilling output, or code/docs exploration into a durable Markdown note. Use when useful conclusions, decisions, assumptions, findings, options, or open questions should be preserved outside chat. Do not use to create specs, ADRs, product briefs, task issues, QA checklists, or handoff prompts.
---

# Capture

## Overview

Condense useful context from a long conversation, research session, grilling session, or code/docs exploration into a durable Markdown note. Preserve actionable synthesis, source references, and unresolved questions, not raw transcripts.

## When To Use

- The user asks to capture, preserve, archive, extract, condense, write up, or save a long session.
- Research, grilling, code exploration, documentation exploration, or a long discussion produced findings worth revisiting.
- Decisions, conclusions, assumptions, options considered, risks, or open questions should survive beyond the current chat context.

Do not use this skill for ordinary chat summaries, product briefs, specs, ADRs, issue creation, task splitting, QA checklists, implementation summaries, or session handoff prompts.

## Workflow

### 1. Resolve Scope And Sources

Identify what should be captured and why it needs to be durable.

- Use the current conversation and any user-provided notes, files, issues, specs, briefs, ADRs, docs, diffs, commits, or research results.
- Inspect relevant repo and documentation sources when they can answer factual context questions. Ask the user only when sources are missing, contradictory, or a material scope decision remains.
- Treat canonical artifacts as sources to reference, not content to duplicate.

### 2. Confirm The Target Path

Use the user's explicit path when provided, after checking that it matches the intended scope and project conventions. If no path is provided, propose one target and ask for confirmation before writing.

Default target choices:

| Situation | Default target |
| --- | --- |
| Initiative-specific capture, local exploration, grilling extraction, or research that may stop being canonical after a spec | `.initiatives/<id>/research/<slug>.md` |
| Reusable project-level research, stack comparison, architecture analysis, vendor analysis, regulatory constraint, or cross-initiative context | `docs/research/<slug>.md` |

Rules:

- Use kebab-case filenames and a clear slug.
- If an initiative-specific target is needed but no initiative exists, propose a path such as `.initiatives/<NNN-slug>/research/<slug>.md` and ask before creating directories.
- If the target file exists, ask for explicit confirmation before overwriting or updating it, or propose a new slug.
- Local capture files use simple Markdown with no frontmatter.

### 3. Write The Capture

After target confirmation, write directly to the confirmed path. Do not show a full draft first unless the user asks.

- Capture synthesis, not the transcript.
- Structure the note around the subject, not a rigid template.
- Use a clear title.
- Separate facts, assumptions, interpretation, decisions or conclusions, options considered, and open questions when those distinctions matter.
- Cite important sources with paths, URLs, issue numbers, commit hashes, or artifact names.
- Summarize and point to existing canonical artifacts instead of copying their content.
- Keep command logs, file lists, prompts, and model outputs out of the capture unless they are necessary source evidence.

Possible sections, only when useful:

- `Context`
- `Key Findings`
- `Facts`
- `Assumptions`
- `Interpretation`
- `Decisions Or Conclusions`
- `Options Considered`
- `Open Questions`
- `Sources And References`

### 4. Safety Pass

Before writing, remove anything that should not be stored in a repo-adjacent artifact:

- Secrets, tokens, credentials, or private keys.
- Raw personal data or sensitive customer exports.
- Raw prompts, full LLM transcripts, or tool dumps that do not add durable value.
- Anything the user would not want visible to someone with repo access.

Do not create or update briefs, specs, ADRs, issues, comments, tracker state, handoff prompts, or unrelated global documentation as part of capture. Write only the confirmed capture file unless the user explicitly asks for a separate artifact.

## Output

The primary output is one confirmed Markdown capture file.

Final response:

- File created or updated.
- What source material was captured.
- Important omissions, redactions, or unresolved questions.
- Confirmation that no unrelated workflow artifacts were created.

## Validation

Before finishing, verify:

- [ ] The target path was confirmed before writing.
- [ ] Existing files were not overwritten or substantially updated without explicit confirmation.
- [ ] The note is useful when read outside the conversation.
- [ ] The note is a synthesis, not a raw transcript or prompt dump.
- [ ] Facts, assumptions, interpretation, decisions, conclusions, options, and open questions are separated when that distinction matters.
- [ ] Important sources, paths, URLs, issues, commits, or artifacts are cited.
- [ ] Canonical artifacts are referenced instead of duplicated.
- [ ] No secrets, credentials, raw personal data, sensitive customer exports, or unnecessary full LLM/tool transcripts are included.
- [ ] No product brief, spec, ADR, issue, QA checklist, tracker publication, or handoff artifact was created implicitly.
