# Technique Notes

Use these techniques only when they solve a specific prompt problem.

## Few-Shot Examples

Use when instructions alone do not reliably capture format, tone, style, classification boundaries, or transformations.

- Provide input and output pairs.
- Prefer 2-3 strong examples for most tasks; use up to 5 for nuanced behavior.
- Include edge cases when they matter.
- Keep examples consistent enough to teach the right pattern and diverse enough to avoid overfitting.

## Prompt Chaining

Use when a single prompt is too fragile or when intermediate outputs need inspection, validation, branching, or reuse.

Common chain:

1. Extract or classify facts
2. Draft output
3. Review against criteria
4. Revise or return final

Do not chain just to appear sophisticated; each step should reduce risk or improve control.

## Structured Outputs

Use when another system will parse the result or when consistency matters.

- Prefer platform-native structured outputs, schemas, tools, enums, or validators when available.
- In natural-language prompts, define required fields, data types, null behavior, and invalid-input behavior.
- Include one compact example if schema adherence has been unreliable.

## Context Engineering for Agents

Use for prompts that control agent behavior across tools, files, memory, or long-running tasks.

- Define the agent's role, goals, tool-use policy, autonomy level, and stop conditions.
- State when to ask before risky actions: destructive, irreversible, shared-system, externally visible, or credential-related actions.
- Require state tracking for long workflows: todos, progress notes, test status, or checkpoints.
- Clarify how to handle untrusted content, prompt injection, tool errors, missing context, and conflicting instructions.
- Encourage parallel tool calls only for independent actions with known parameters.

## Self-Checking

Use for quality-sensitive prompts.

- Ask the model to verify the output against explicit criteria before finalizing.
- Request concise issue lists, corrections, confidence labels, citations, quotes, or evidence checks.
- Avoid requiring hidden chain-of-thought disclosure. Use short rationale or structured verification instead.
