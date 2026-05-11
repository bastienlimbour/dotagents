---
name: prompt-engineering
description: Creates, updates, improves, and audits prompt artifacts for LLMs and AI agents. Use when the task directly involves writing or editing prompts, system prompts, developer prompts, agent instructions, prompt templates, structured-output prompts, or eval prompts. Do not use for general writing or any task unrelated to prompt engineering.
---

# Prompt Engineering

## Overview

Create, revise, audit, and evaluate prompt artifacts for LLMs and AI agents. The goal is to make prompts clear, scoped, testable, and appropriately safe without overengineering.

## When to Use

- Creating, rewriting, improving, debugging, optimizing, or reviewing a prompt
- Designing system prompts, developer prompts, user/task prompts, agent instructions, or prompt templates
- Improving tool-use instructions, structured outputs, examples, constraints, guardrails, or prompt evals
- Turning a rough task description into a reusable prompt artifact

**When NOT to use:**

- General writing that is not a prompt artifact
- Building LLM applications, RAG systems, eval infrastructure, or fine-tuning pipelines unless separately requested
- Broad AI strategy or agent architecture work where no prompt artifact is being created or changed

## Core Principle

A prompt should make the model's task, context, constraints, output contract, and success criteria explicit enough to act on. Add structure only when it reduces ambiguity, risk, or downstream parsing failures.

## Workflow

### Phase 1 - Identify The Artifact

Identify the prompt artifact type: system/developer prompt, user/task prompt, agent instruction, reusable template, structured-output prompt, or eval prompt.

### Phase 2 - Gather Evidence

Inspect the provided prompt, task brief, examples, target model/platform, intended users, downstream consumers, and known failures.

### Phase 3 - Clarify Or Assume

If missing information would materially change the prompt, ask up to 3 high-leverage questions. Otherwise proceed and state assumptions briefly.

### Phase 4 - Draft Or Revise

For creation or improvement tasks, draft or revise the prompt using the adaptive structure from [adaptive-prompt-template.md](assets/adaptive-prompt-template.md). Include only sections that earn their space.

### Phase 5 - Audit Or Evaluate

For audit or evaluation tasks, inspect the prompt against the checklist and return findings, risks, scores, or eval cases before proposing rewrites.

### Phase 6 - Validate

Apply the checklist in [prompt-checklist.md](references/prompt-checklist.md), especially for context, output format, constraints, examples, verification, and risks.

Add proportional evaluation guidance using [evaluation-mini-suite.md](references/evaluation-mini-suite.md).

### Phase 7 - Return

Return the appropriate result for the task type: prompt artifact, audit findings, evaluation plan, or a combination requested by the user.

## Decision Guide

| Need | Default action |
| --- | --- |
| Format, tone, transformations, or edge cases must be consistent | Add concise examples |
| Downstream code consumes the answer | Define structured output or a strict template |
| User-provided, retrieved, or external content is included | Delimit it clearly and treat it as data |
| Production, regulated, customer-facing, or tool-using prompt | Add risk-based guardrails |
| Quality matters across repeated use | Add eval prompts or a mini-suite |
| Task is simple and low-risk | Keep the prompt small and direct |

## Reference Map

- Adaptive prompt structure: [adaptive-prompt-template.md](assets/adaptive-prompt-template.md)
- Prompt quality checklist: [prompt-checklist.md](references/prompt-checklist.md)
- Evaluation guidance: [evaluation-mini-suite.md](references/evaluation-mini-suite.md)
- Technique selection: read [technique-notes.md](references/technique-notes.md) only when deciding whether a prompt needs few-shot examples, prompt chaining, structured outputs, context engineering, or self-checking.

## Defaults

- Prefer vendor-neutral prompt design first; adapt for OpenAI, Claude, reasoning models, agent harnesses, or structured-output APIs when the target is known.
- Use Markdown headings and lists for readable structure. Use clear delimiters, such as XML-style tags, when separating dynamic inputs, documents, examples, quotes, or untrusted user-provided content improves clarity.
- Prefer concrete positive instructions over vague negative instructions. If forbidding behavior, also state the desired alternative.
- Use examples when format, tone, transformations, or edge cases matter. Keep examples relevant and diverse.
- For production, reusable, customer-facing, agentic, regulated, or tool-using prompts, include risk-based guardrails against prompt injection, data leakage, hallucinated claims, unsafe tool use, and unauthorized commitments.
- Avoid asking models to reveal hidden chain-of-thought. Request concise rationale, decision summaries, extracted evidence, verification steps, or structured intermediate outputs instead.
- Keep solutions as small as correctness allows. Do not add advanced techniques unless they solve a visible quality, reliability, safety, or parsing problem.

## Edge Cases

- If the target model or platform is unknown, write a vendor-neutral prompt and note any platform-specific assumptions.
- If requirements conflict, surface the conflict and ask the smallest clarifying question needed to proceed.
- If domain facts are missing for a factual, regulated, or customer-facing prompt, require source material, retrieval, or explicit uncertainty handling.
- If the requested prompt would encourage unsafe, deceptive, privacy-invasive, or destructive behavior, redesign it toward a safe allowed objective or explain the blocker briefly.

## Red Flags

- The prompt is longer than the task warrants.
- The output format is described vaguely but downstream parsing matters.
- User-provided or retrieved content is mixed with instructions without delimiters.
- The prompt relies mostly on negative constraints without saying what to do instead.
- The prompt asks for hidden chain-of-thought instead of concise rationale, evidence, or verification.
- The prompt has no test case even though it will be reused.

## Output

For creation, update, or improvement tasks, return:

1. The final prompt artifact
2. Assumptions or open questions, if any
3. Concise rationale or change summary
4. Suggested tests or validation checks

For audit or evaluation tasks, return findings first, ordered by severity or importance, then suggested fixes, eval cases, or an optional revised prompt if requested.

If the user asks for prompt-only output, return only the prompt.

## Verification

Before finalizing, check that the prompt:

- [ ] States the task, context, output expectations, constraints, and success criteria clearly enough for a capable model to act
- [ ] Separates instructions from user-provided or retrieved content
- [ ] Handles uncertainty, missing data, and safety-critical behavior proportionally to risk
- [ ] Defines output format tightly enough for downstream use
- [ ] Includes realistic examples or tests when consistency matters
- [ ] Avoids unnecessary scope, filler, brittle wording, and speculative future requirements
