# Evaluation

Use this reference when creating eval plans, deciding whether to add `evals/`, improving trigger behavior, or iterating on skill quality.

## Eval Policy

Every new skill or material update needs one of these:

- A lightweight eval plan in the final response or skill notes.
- A short reason evals are unnecessary, such as a trivial one-command skill with obvious manual verification.
- Full eval files for non-trivial skills.

Add full eval files when the skill has complex activation boundaries, scripts, high-stakes behavior, repeated future use, or output quality that is hard to judge manually.

## Lightweight Eval Plan

Include:

- 2 to 5 should-trigger prompts.
- 2 to 5 should-not-trigger near-miss prompts.
- 1 to 3 representative task prompts with expected behavior.
- Manual checks or assertions for success.

This is enough for small instruction-only skills.

## Full Eval File Shape

Use `evals/evals.json` when a persistent eval suite is justified:

```json
{
  "skill_name": "skill-name",
  "trigger_queries": [
    {
      "query": "Create a report from this team-specific CSV format",
      "should_trigger": true,
      "reason": "Matches the skill's domain-specific workflow"
    }
  ],
  "evals": [
    {
      "id": "representative-task",
      "prompt": "Realistic user prompt",
      "expected_output": "Human-readable success criteria",
      "files": [],
      "assertions": [
        "Specific observable requirement"
      ]
    }
  ]
}
```

Adapt the schema if the target client already has an eval format.

## Trigger Quality

Test activation separately from output quality.

- Use realistic prompts with file paths, casual language, typos, and implicit intent.
- Include near-misses that share keywords but need a different skill or no skill.
- Run multiple times when possible and record trigger rate.
- Split train and validation queries when optimizing descriptions.

## Output Quality

Run each representative task in a clean context. Compare with and without the skill, or compare current skill against the previous version.

For each eval, capture:

- Produced files or response.
- Tool trace if available.
- Duration and token usage if available.
- Assertion results with concrete evidence.
- Human feedback for qualities not captured by assertions.

## Iteration Loop

1. Run trigger and output evals.
2. Identify failures and noisy instructions.
3. Improve the smallest part of the skill that addresses the failure.
4. Rerun the same evals.
5. Keep the version with the best validation behavior, not necessarily the latest draft.

If results do not improve after several iterations, reassess the skill scope, description, or eval labels rather than adding more instructions.
