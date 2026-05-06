# Evaluation Mini-Suite

Use proportional evaluation. Do not build a large eval suite for a one-off lightweight prompt unless requested.

## Lightweight Prompts

Use a short self-check:

- Does the output satisfy the stated task?
- Does it follow the required format and length?
- Does it avoid unsupported claims?
- Does it handle missing information as instructed?

## Reusable or Production Prompts

Create 4-8 test cases:

- Representative case: normal expected input
- Edge case: unusual but valid input
- Missing-data case: incomplete input that should trigger uncertainty, nulls, or clarification
- Adversarial case: prompt injection, conflicting instructions, unsafe request, or misleading context
- Format case: output must validate against schema, JSON, enum, table, or parser expectations
- Domain-risk case: compliance, security, customer-facing promise, financial/legal/medical claim, or destructive tool use if relevant

For each case, specify:

- Input
- Expected behavior
- Must-have output properties
- Failure signs

## Metrics

Choose metrics that match the task:

- Schema validity or parse rate
- Accuracy or source-grounding rate
- Recall and precision for extraction, review, or bug-finding prompts
- Hallucination or unsupported-claim rate
- Safety violation rate
- User satisfaction or human preference
- Latency, token cost, and verbosity

## Regression Practice

- Version reusable prompts and record what changed.
- Pin production model snapshots where the platform supports it.
- Re-run evals when changing prompt text, model, tool descriptions, retrieval strategy, examples, or output schema.
- Compare before/after outputs and check for regressions, not only improvements.
