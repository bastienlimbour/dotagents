# Prompt Patterns and Output Design

## Contents

- Prompt anatomy
- Full template
- Minimal template
- Common patterns (generation, editing, extraction, analysis, transformation, planning)
- Output design rules
- Context engineering

## Prompt anatomy

Every prompt is an execution contract built from these parts. Use the smallest combination that succeeds.

| Section | Purpose |
| --- | --- |
| **Objective** | What the model must do. Lead with a direct action verb. |
| **Context** | Minimum background needed — only what matters. |
| **Constraints** | Hard boundaries, non-goals, important preferences. Explain why when it improves judgment. |
| **Output contract** | Exact structure, format, length, tone, or schema. |
| **Examples** | Only when behavior is easier to show than describe. |
| **Uncertainty** | What to do when information is missing or ambiguous. |

## Full template

```markdown
# Role
You are [specific operational role].

# Objective
[precise objective]

# Context
- [useful info 1]
- [useful info 2]

# Success Criteria
- [criterion 1]
- [criterion 2]

# Constraints
- [constraint 1]
- [constraint 2]
- Do not invent missing information
- State assumptions clearly when necessary

# Tool Policy
- Use [tool] when [condition]
- If a tool fails, [fallback]

# Workflow
1. Understand the request
2. Check prerequisites
3. Gather missing context
4. Execute
5. Verify
6. Return the final result

# Output Contract
Return exactly:
1. [section 1]
2. [section 2]
3. [section 3]

# Before Finishing
- Verify all requirements are covered
- Verify the requested format is respected
- Verify the response is grounded in the available context
```

## Minimal template

Use when the full template is overkill:

```text
Task
<one clear sentence describing the job>

Context
<essential background only>

Constraints
- <hard requirement>
- <non-goal>

Output
<the exact shape of the answer you want>

If the provided information is insufficient, say so instead of guessing.
```

## Common patterns

### Generation

```text
Write <artifact> for <audience>.

Context
<background, purpose, important facts>

Constraints
- Preserve these ideas: <...>
- Avoid these mistakes: <...>
- Tone: <...>
- Length: <...>

Output
Return <sections, format, or schema>.
```

### Editing / Rewriting

```text
Rewrite the text below for <audience or purpose>.

Goals
- Preserve meaning
- Improve <clarity / precision / brevity>
- Keep these terms unchanged: <...>

Text
"""
<source text>
"""

Output
Return the revised text only.
```

### Extraction / Classification

```text
Extract the requested fields from the source text.

Fields
- <field 1>
- <field 2>

Rules
- Use only information present in the source
- If a field is missing, return null or "unknown"
- Do not infer unsupported values

Source
"""
<input text>
"""

Output
Return valid JSON matching this shape:
{ "field1": "", "field2": "" }
```

### Analysis / Review

```text
Review the material below against these criteria:
- <criterion 1>
- <criterion 2>

Output
Return:
1. Key findings ordered by severity
2. Gaps or uncertainties
3. A concise final recommendation
```

### Transformation

```text
Transform the input from <source form> into <target form>.

Preserve
- <facts that must survive>

Change
- <what should be reformatted or normalized>

Output
Return only the transformed result.
```

### Planning

```text
Create an execution plan for the task below.

Task
<goal>

Constraints
- <limitation>

Output
Return:
1. Assumptions
2. Ordered steps
3. Risks or blockers
4. Verification criteria
```

## Output design rules

1. Always specify the output shape explicitly.
2. For prose: define section names, order, length constraints.
3. For structured data: define exact schema, required fields, allowed values.
4. State whether preambles or markdown formatting are allowed.
5. Specify length or token budget if it matters.
6. Specify ordering rules.

**Format selection:**

| Consumer | Format |
| --- | --- |
| Human reads | Markdown with sections |
| Complex prompt boundaries | XML or structured tags |
| Machine parses | JSON or schema |
| Procedures | Checklist |

**Example structured schema:**

```json
{
  "summary": "string",
  "actions_taken": ["string"],
  "risks": ["string"],
  "next_step": "string"
}
```

## Context engineering

For complex tasks the job expands to deciding what information enters the model's context and in what order.

### Context layers

1. **Goal layer**: Objective and success criteria.
2. **Constraint layer**: Non-goals, limits, approval gates.
3. **Resource layer**: Files, tools, examples, schemas.
4. **State layer**: What has happened, what remains, blockers.
5. **Output layer**: Expected format, deliverable, next action.

### Context ordering

1. Permanent instructions (highest priority, near the top).
2. Supporting context.
3. Current task (at the end).

### Quality rules

- Include only material relevant to the current step.
- Summarize background that does not need verbatim detail.
- Put critical constraints near the beginning.
- Split unrelated objectives into separate prompts.
- Prefer just-in-time retrieval over preloading everything.
- Clearly separate instructions, context, examples, raw input, and expected output.
- Use system/developer messages when the platform supports them.
- If the model misses instructions in long context, reduce the prompt or isolate the task instead of repeating louder.
