---
name: prompt-engineering
description: Creates, updates, improves, and audits prompt artifacts for LLMs and AI agents. Use when the task directly involves writing or editing prompts, system prompts, developer prompts, agent instructions, prompt templates, structured-output prompts, or eval prompts. Do not use for general writing or any task unrelated to prompt engineering.
---

# Prompt Engineering

Create, revise, audit, and evaluate prompt artifacts for LLMs and AI agents. Make prompts clear, scoped, testable, and appropriately safe without overengineering.

## When To Use

- Creating, rewriting, debugging, optimizing, or reviewing a prompt artifact.
- Designing system prompts, developer prompts, user/task prompts, agent instructions, reusable templates, structured-output prompts, or eval prompts.
- Improving tool-use instructions, examples, constraints, guardrails, output contracts, or prompt evals.

Do not use for general writing, broad AI strategy, app/RAG/eval infrastructure, or fine-tuning work unless a prompt artifact is being created or changed.

## Core Principle

A prompt should make the model's task, context, constraints, output contract, and success criteria explicit enough to act on. Add structure only when it reduces ambiguity, risk, or downstream parsing failures.

## Workflow

### 1. Inspect And Scope

Identify the artifact type and inspect the provided prompt, task brief, examples, target model/platform, intended users, downstream consumers, and known failures.

Ask up to 3 high-leverage questions only when missing information would materially change the prompt. Otherwise proceed and state assumptions briefly.

### 2. Draft Or Revise

For creation or improvement tasks, draft or revise the prompt using the adaptive structure from [adaptive-prompt-template.md](assets/adaptive-prompt-template.md). Include only sections that earn their space.

### 3. Audit Or Evaluate

For audit or evaluation tasks, inspect the prompt against the checklist and return findings, risks, scores, or eval cases before proposing rewrites.

### 4. Validate

Apply [prompt-checklist.md](references/prompt-checklist.md), especially for context, output format, constraints, examples, verification, and risks. Add proportional evaluation guidance using [evaluation-mini-suite.md](references/evaluation-mini-suite.md).

### 5. Return

Return the appropriate result for the task type: prompt artifact, audit findings, evaluation plan, or a combination requested by the user.

## Rules

- Prefer vendor-neutral prompt design; adapt to OpenAI, Claude, reasoning models, agent harnesses, or structured-output APIs only when the target is known.
- Keep the prompt as small as correctness allows. Add structure, examples, guardrails, or techniques only when they reduce ambiguity, risk, or parsing failures.
- Prefer concrete positive instructions. If forbidding behavior, state the desired alternative.
- Use examples when format, tone, transformations, or edge cases must be consistent.
- Define structured output, schemas, validators, or strict templates when downstream parsing matters.
- Delimit user-provided, retrieved, external, or untrusted content and treat it as data.
- Add risk-based guardrails for production, reusable, customer-facing, agentic, regulated, or tool-using prompts.
- For factual, regulated, or customer-facing prompts, require source material, retrieval, citations, or explicit uncertainty handling when domain facts are missing.
- Avoid asking for hidden chain-of-thought. Request concise rationale, evidence, decision summaries, verification steps, or structured intermediate outputs instead.
- If requirements conflict or safety is at issue, surface the conflict and ask the smallest needed question, or redesign toward a safe allowed objective.

## Reference Map

- Adaptive prompt structure: [adaptive-prompt-template.md](assets/adaptive-prompt-template.md)
- Prompt quality checklist: [prompt-checklist.md](references/prompt-checklist.md)
- Evaluation guidance: [evaluation-mini-suite.md](references/evaluation-mini-suite.md)
- Technique selection: read [technique-notes.md](references/technique-notes.md) only when deciding whether a prompt needs few-shot examples, prompt chaining, structured outputs, context engineering, or self-checking.

## Output

For creation, update, or improvement tasks, return the final prompt artifact, assumptions or open questions, concise rationale or change summary, and suggested tests or validation checks.

For audit or evaluation tasks, return findings first, ordered by severity or importance, then suggested fixes, eval cases, or an optional revised prompt if requested.

If the user asks for prompt-only output, return only the prompt.

## Validation

Before finalizing, check that the prompt:

- [ ] States the task, context, output expectations, constraints, and success criteria clearly enough for a capable model to act
- [ ] Separates instructions from user-provided or retrieved content
- [ ] Handles uncertainty, missing data, and safety-critical behavior proportionally to risk
- [ ] Defines output format tightly enough for downstream use
- [ ] Includes realistic examples or tests when consistency matters
- [ ] Avoids unnecessary scope, filler, brittle wording, and speculative future requirements
