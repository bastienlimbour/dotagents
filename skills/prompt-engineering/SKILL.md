---
name: prompt-engineering
description: Designs, rewrites, reviews, and debugs prompts, system instructions, agent rules, and output contracts for LLM workflows. Use when working on prompt engineering, LLM prompts, prompt templates, system prompts, context engineering, agent instructions, rules files, prompt evaluation, prompt debugging, or output schema design. Not intended for general copywriting, non-LLM documentation, or model API integration unless prompt design is the core task.
---

# Prompt Engineering

## When to use

- Designing a new prompt, system prompt, or instruction set
- Rewriting or improving an existing prompt
- Reviewing or debugging a prompt that produces poor results
- Writing agent instructions, rules files (AGENTS.md, CLAUDE.md, .cursorrules)
- Designing output contracts or structured output schemas
- Context engineering for complex or multi-step LLM tasks
- Evaluating prompt quality or building prompt test cases

## When not to use

- General copywriting or content writing not targeting an LLM
- Writing documentation, READMEs, or changelogs
- Model API integration, fine-tuning, or infrastructure work
- Tasks where the prompt is incidental, not the deliverable

## Core principles

1. **Be precise.** Follow the exact task, not a guessed variation.
2. **Be explicit.** State the audience, format, inclusions, and exclusions. Do not make the model guess.
3. **Say what to do, not only what to avoid.** Positive instructions beat pure prohibitions. Replace `Do not be too long` with `Respond in at most 5 points, one sentence each`.
4. **Do not guess.** If required information is missing: ask one targeted question, state the limitation, or use a tool.
5. **Optimize for completion.** Execute, verify, then summarize. If blocked, attempt recovery before stopping.
6. **Verify before concluding.** Check requirements, format, and factual grounding before returning the final answer.
7. **Resolve conflicts by:** (1) priority, (2) specificity, (3) recency.
8. **Iterate with evidence.** Define success first. If a change does not improve measurable behavior, remove it.

## Quick start

Determine the task type, then follow the matching path:

| Task | Start here |
| --- | --- |
| **Create** a new prompt | Workflow step 1 below |
| **Rewrite** an existing prompt | Workflow step 1, with the existing prompt as input |
| **Review / Debug** a failing prompt | Read [prompt-debugging.md](references/prompt-debugging.md) for the failure taxonomy, then apply the rewriting heuristics |
| **Write agent instructions** | Read [agent-instructions.md](references/agent-instructions.md) for agent anatomy and persistent instruction patterns |

## Workflow

### 1. Clarify the objective

Identify:

- What must the prompt accomplish? (one clear job)
- Who is the audience or consumer of the output?
- What does success look like? (concrete criteria)
- What are the hard constraints and non-goals?

If the request is underspecified, ask one targeted clarification question before proceeding.

### 2. Choose the smallest effective structure

Use the **minimal template** for simple tasks. Use the **full template** only when the task requires role, tools, workflow, or verification sections.

See [prompt-patterns.md](references/prompt-patterns.md) for both templates and common prompt patterns (generation, editing, extraction, analysis, transformation, planning).

### 3. Write the prompt

Build in this order:

1. **Objective** — lead with a direct action verb.
2. **Context** — minimum background needed, nothing more.
3. **Constraints** — hard boundaries, non-goals, important preferences. Explain why when it improves judgment.
4. **Output contract** — exact structure, format, schema, or length.
5. **Uncertainty handling** — what to do when information is missing.
6. **Verification** — what to check before finishing.

Add examples only when behavior is easier to show than describe. One strong example beats many weak ones.

### 4. Apply formatting rules

- Use labeled sections (`# Objective`, `# Constraints`, `# Output`).
- Use numbered steps for ordered workflows; bullets for atomic rules.
- Separate instructions from data, examples, and raw input.
- Use triple quotes for source material, code fences for schemas, XML tags only when boundaries must be unmistakable.
- Use `IMPORTANT:` or `CRITICAL:` sparingly — only for a few truly critical rules.
- Use role framing only when it sharpens evaluation criteria or domain perspective.

### 5. Verify the prompt

Before finalizing, check:

- [ ] Objective is precise and in the first few lines.
- [ ] Context is sufficient but not excessive.
- [ ] Constraints are explicit.
- [ ] Output format is defined and testable.
- [ ] Uncertainty handling is specified.
- [ ] Completion criterion is clear.

For agent instructions, also check:

- [ ] Tool usage is clearly defined.
- [ ] Approval boundaries are set for risky actions.
- [ ] Stop conditions and escalation rules are explicit.

See [prompt-debugging.md](references/prompt-debugging.md) for the full review checklist, failure taxonomy, and evaluation set design.

## Key references

| File | Read when |
| --- | --- |
| [prompt-patterns.md](references/prompt-patterns.md) | Creating or restructuring any prompt — templates, patterns, output design, context engineering |
| [agent-instructions.md](references/agent-instructions.md) | Writing persistent agent instructions, rules files, tool policies, workflow design, or verification loops |
| [prompt-debugging.md](references/prompt-debugging.md) | Debugging a failing prompt, reviewing prompt quality, building evaluation sets, or rewriting weak prompts |
