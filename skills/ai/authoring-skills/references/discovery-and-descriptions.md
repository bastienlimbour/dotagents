# Discovery And Descriptions

Use this reference when naming a skill, writing frontmatter, improving activation, or auditing false triggers and missed triggers.

## Trigger Surface Goal

The description is the primary discovery surface. Assume an agent may see many skill descriptions and only a shortened initial list. The first sentence must make the intended activation obvious.

Litmus test: if the agent sees 100 skill descriptions, this one should activate for the right tasks and stay silent for adjacent tasks.

## Naming

Good names are specific and action-oriented:

- `authoring-skills`
- `reviewing-security-changes`
- `processing-pdfs`
- `analyzing-sales-data`

Avoid vague names:

- `helper`
- `workflow`
- `tools`
- `docs`

Prefer one naming style across a collection. Use lowercase hyphenated names that match the directory.

## Description Formula

Use this shape as a default, then trim:

```yml
description: Does [specific capability]. Use when [user intent, artifacts, file types, or workflow context]. Do not use when [likely near-miss, only if needed].
```

Keep it concise. Front-load the high-value trigger words before secondary detail.

## What To Include

Include:

- The concrete job the skill performs.
- Common user phrasings and artifacts.
- Adjacent terms the user might use without naming the domain directly.
- Exclusions for likely false positives.

Avoid:

- Implementation details that users will not mention.
- Generic claims such as "helps with files".
- Long capability lists that make the skill look broader than it is.
- First-person wording.

## Boundary Design

Ask or infer these before finalizing the description:

- What tasks should definitely trigger the skill?
- What similar tasks should not trigger it?
- What words will users actually type?
- What other skills may compete for the same prompt?
- Would activation be harmful or noisy for simple one-step tasks?

## Trigger Evals

For non-trivial skills, create about 10 to 20 trigger queries:

- Should-trigger queries with varied phrasing, explicit and implicit intent, file paths, typos, and realistic context.
- Should-not-trigger queries that are near-misses with overlapping keywords.

Run each query multiple times when possible and track trigger rate. Improve the description using train queries, then confirm on held-out validation queries. Avoid adding exact failed query wording unless it represents a general category.

## Common Fixes

- Missed triggers: add the missing user intent category, artifact type, or synonym.
- False triggers: narrow the task boundary or add a concise exclusion.
- Overlong descriptions: remove implementation detail and keep only discovery signals.
- Competing skills: make each description name its specific artifact and scope.
