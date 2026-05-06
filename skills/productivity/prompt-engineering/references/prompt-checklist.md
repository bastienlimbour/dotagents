# Prompt Checklist

Use this checklist to create, revise, or audit prompt artifacts. Apply only the items relevant to the task.

## Core Shape

- Task: Does the prompt use a clear action verb and state what the model must do?
- Goal: Does it explain the desired outcome and why it matters when that context improves judgment?
- Audience: Does it name the intended reader, user, or downstream system when relevant?
- Scope: Does it say what is in scope and what is out of scope?
- Priority: Does it clarify whether accuracy, completeness, speed, creativity, brevity, cost, or safety matters most?

## Context

- Provide the minimum context needed to do the task well.
- Separate dynamic input from instructions with tags such as `<input>`, `<context>`, `<documents>`, `<example>`, or `<output>`.
- For long documents, put source material before the final task and ask for evidence extraction or quotes before analysis when grounding matters.
- For current or domain-specific facts, use provided source material or retrieval rather than relying on model memory.
- Remove irrelevant context that increases contradictions, ambiguity, or token cost.

## Workflow

- Use numbered steps only when order or completeness matters.
- Include decision criteria for branches, escalation, refusal, or asking clarifying questions.
- For agent prompts, define tool-use expectations, autonomy boundaries, state tracking, progress updates, and safety confirmations.
- For complex work, split into stages if intermediate outputs need inspection, validation, or reuse.

## Output Format

- Specify the response shape: prose, bullets, table, JSON, schema, function call, label, patch, email, report, or other artifact.
- Specify required fields, optional fields, null handling, length limits, tone, and formatting conventions.
- Use structured outputs, schemas, tools/enums, or validators when downstream parsing matters.
- Provide examples when output style, schema, or transformation quality must be consistent.

## Rules and Constraints

- Prefer positive instructions: say what to do, not only what to avoid.
- Mark hard constraints clearly, but avoid excessive all-caps or alarm language.
- Include risk-based guardrails for prompt injection, secrets, private data, compliance, unsafe tool use, destructive actions, and unauthorized business commitments.
- Tell the model what to do when it lacks enough information: ask, state uncertainty, use `null`, cite missing evidence, or escalate.

## Examples

- Use 1-5 examples when format, tone, style, or edge-case behavior matters.
- Include both input and output for transformation tasks.
- Keep examples realistic, diverse, and aligned with the actual use case.
- Add a short note if the examples are meant to demonstrate a specific pattern.
- Remove examples that are inconsistent, redundant, or likely to teach the wrong pattern.

## Verification

- Add acceptance criteria for important prompts.
- Ask for concise self-checking against explicit criteria, not hidden chain-of-thought.
- For factual tasks, require evidence, citations, quotes, or source-grounded uncertainty when available.
- For coding prompts, require tests or validation and prohibit hard-coding to pass tests only.
- For review/eval prompts, separate issue discovery from severity ranking when recall matters.

## Final Audit

- Could a capable colleague follow the prompt without extra context?
- Are instructions separated from untrusted user or retrieved content?
- Is the prompt smaller than a bloated version but complete enough to work?
- Does it avoid vague terms like "good", "nice", "detailed", or "professional" unless defined?
- Are success criteria testable?
