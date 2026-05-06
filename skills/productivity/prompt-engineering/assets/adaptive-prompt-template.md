# Adaptive Prompt Template

Use this template as a menu, not a rigid form. Keep only the sections that improve the prompt.

```markdown
# Role

You are [specific role or capability].

# Goal

[State the outcome, success criteria, and what matters most.]

# Context

[Provide relevant background, domain facts, source material, assumptions, user profile, constraints, or available tools.]

<input>
{{INPUT}}
</input>

# Workflow

1. [Step or decision criterion]
2. [Step or decision criterion]
3. [Verification or escalation step]

# Output Format

[Specify exact format, required fields, length, tone, schema, null handling, and examples if needed.]

# Rules and Constraints

- [Positive instruction or hard rule]
- [Boundary, safety rule, or escalation trigger]
- [How to handle missing data or uncertainty]

# Examples

<examples>
  <example>
    <input>[Example input]</input>
    <output>[Desired output]</output>
  </example>
</examples>

# Verification

Before finalizing, check that:

- [Acceptance criterion]
- [Format criterion]
- [Safety or factuality criterion]
```

## Template Notes

- For system/developer prompts, put stable identity, goals, rules, and examples in the high-authority message. Keep user-specific task input separate.
- For reusable templates, use placeholders such as `{{INPUT}}`, `{{AUDIENCE}}`, or `{{CONSTRAINTS}}` and define expected values.
- For long-context prompts, put documents before the final query and use tags with source metadata.
- For agent prompts, add tool-use policy, autonomy boundaries, state tracking, and risky-action confirmation rules.
- For eval prompts, define the rubric, scoring scale, evidence requirements, and output schema.
