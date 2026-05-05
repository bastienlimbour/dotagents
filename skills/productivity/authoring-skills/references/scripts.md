# Scripts

Read this file ONLY if the skill uses scripts or executable code.

## Use scripts when

- the operation is deterministic
- the same logic would otherwise be generated repeatedly
- validation or error handling needs to be explicit

Prefer execution over code generation when a small script can do the job reliably.

## Rules

- Say whether the agent should **run** the script or **read** it as reference
- Keep scripts small and single-purpose
- Solve problems in the script; do not punt obvious failures back to the agent
- Handle errors inside the script with specific messages
- Name constants instead of using magic numbers
- List required packages in `SKILL.md` with install commands
- Validate paths, scope, and dangerous actions
- Do not hardcode credentials

## Workflow pattern

For high-stakes or batch work, use:

1. plan
2. validate
3. execute
4. re-validate

Use this for destructive changes, complex validation rules, or large batch operations.

## Examples

````markdown
Run `python scripts/analyze_form.py input.pdf > fields.json` to extract fields.

Run `python scripts/validate_boxes.py fields.json` before filling the form.
````

Verbose validator output is better than generic failure messages:

```text
Field 'signature_date' not found. Available fields: customer_name, order_total, signature_date_signed
```

## Dependency example

````markdown
Install required package: `pip install pypdf`
````
