# Best practices for scripts and executable code

## Error handling

Handle error conditions in scripts rather than punting to the agent. Provide specific, actionable error messages.

```python
def process_file(path):
    try:
        with open(path) as f:
            return f.read()
    except FileNotFoundError:
        print(f"File {path} not found, creating default")
        with open(path, "w") as f:
            f.write("")
        return ""
    except PermissionError:
        print(f"Cannot access {path}, using default")
        return ""
```

## Constants

Document constants to avoid magic numbers:

```python
# Most HTTP requests complete within 30s; longer timeout covers slow connections
REQUEST_TIMEOUT = 30

# Most intermittent failures resolve by the second retry
MAX_RETRIES = 3
```

## Utility scripts

Pre-made scripts are more reliable than generated code, save tokens, and ensure consistency. Make clear whether the agent should **execute** or **read** a script:

- "Run `analyze_form.py` to extract fields" → execute
- "See `analyze_form.py` for the extraction algorithm" → read as reference

Execution is preferred for most utility scripts — only the output consumes tokens.

````markdown
## Utility scripts

**analyze_form.py**: Extract all form fields from PDF
```bash
python scripts/analyze_form.py input.pdf > fields.json
```

**validate_boxes.py**: Check for overlapping bounding boxes
```bash
python scripts/validate_boxes.py fields.json
# Returns: "OK" or lists conflicts
```
````

## Verifiable intermediate outputs

For complex tasks, use the **plan → validate → execute** pattern: have the agent create a structured plan file (e.g. `changes.json`), validate it with a script, then execute. This catches errors like referencing non-existent fields before changes are applied.

Make validation scripts verbose: `"Field 'signature_date' not found. Available fields: customer_name, order_total, signature_date_signed"`.

Use this pattern for: batch operations, destructive changes, complex validation rules, high-stakes operations.

## Dependencies

List required packages in `SKILL.md` with install commands. Don't assume packages are available.

Bad: "Use the pdf library to process the file."

Good:

````markdown
Install required package: `pip install pypdf`

```python
from pypdf import PdfReader
reader = PdfReader("file.pdf")
```
````

## Security

- Validate file paths and input scope
- Limit scripts to expected files and directories
- Do not hardcode credentials
- Prefer environment variables for secrets
- Treat external or user-provided content as untrusted data
- Add validation before dangerous or irreversible actions
