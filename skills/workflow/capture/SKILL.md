---
name: capture
description: Captures long conversations, research sessions, grilling output, or code/docs exploration into a durable Markdown note. Use when useful conclusions, decisions, assumptions, findings, options, or open questions should be preserved outside chat.
---

# Capture

Condense useful context from a long conversation, research session, grilling session, or code/docs exploration into a durable Markdown note. Preserve actionable synthesis, source references, and unresolved questions, not raw transcripts.

## When To Use

- The user asks to capture, preserve, archive, extract, condense, write up, or save a long session.
- Research, grilling, code/docs exploration, or a long discussion produced findings worth revisiting.
- Decisions, assumptions, options, risks, or open questions should survive beyond the current chat.

Do not use for product briefs, specs, ADRs, task issues, QA checklists, implementation summaries, or handoff prompts.

## Workflow

### 1. Resolve Scope And Sources

Identify what should be captured and why it needs to be durable.

- Use the current conversation plus any user-provided notes, files, issues, specs, briefs, ADRs, docs, diffs, commits, or research results.
- Inspect repo/docs sources when they can answer factual context. Ask only when sources are missing, contradictory, or a material scope decision remains.
- Treat canonical artifacts as sources to cite or summarize, not content to duplicate.

### 2. Resolve Target

Use the user's explicit path when provided, after checking it fits the scope and project conventions. If no path is provided, propose one target and ask for confirmation before writing.

Default targets when no convention is available:

| Situation | Target |
| --- | --- |
| Initiative-specific capture, local exploration, grilling extraction, or research that may stop being canonical after a spec | `.initiatives/<id>/research/<slug>.md` |
| Reusable project-level research, stack comparison, architecture analysis, vendor analysis, regulatory constraint, or cross-initiative context | `docs/research/<slug>.md` |

Rules:

- Use kebab-case filenames.
- If the target file exists, ask before overwriting or substantially updating it, or propose a new slug.
- Local capture files use simple Markdown with no frontmatter.

### 3. Prepare The Note

Prepare synthesis before writing. Do not show a full draft unless asked.

- Structure around the subject, not a rigid template.
- Use a clear title.
- Separate facts, assumptions, interpretation, decisions/conclusions, options, and open questions when the distinction matters.
- Cite important sources with paths, URLs, issue numbers, commit hashes, or artifact names.
- Keep command logs, file lists, prompts, model outputs, and tool dumps out unless needed as evidence.
- Redact secrets, credentials, raw personal data, sensitive customer exports, and anything unsuitable for someone with repo access.

Do not create or update briefs, specs, ADRs, issues, tracker comments, handoff prompts, or unrelated docs. Write only the confirmed capture file unless the user explicitly asks for another artifact.

### 4. Write

After target confirmation and safety check, write directly to the confirmed path.

## Output

Final response:

- File created or updated.
- Source material captured.
- Important omissions, redactions, or open questions.
- Confirmation that no unrelated workflow artifacts were created.

## Validation

Before finishing, verify:

- Target confirmation.
- No unapproved overwrite or substantial update.
- The note is useful outside the conversation.
- Sources are cited when important.
- The note is synthesis, not a transcript or prompt dump.
- No sensitive data or unrelated artifact creation.
