# Scripts And Security

Use this reference before adding scripts, executable commands, external downloads, network calls, third-party resources, or instructions that touch sensitive files.

## Conservative Script Policy

Prefer instruction-only skills. Add scripts only when they are clearly better than agent reasoning.

Good reasons to add a script:

- The operation is deterministic and repeated.
- The task is fragile or easy to implement incorrectly.
- Validation is machine-verifiable.
- Output is large and should be summarized or paginated.
- The agent repeatedly reinvents the same helper during evals.

Weak reasons:

- The script would only wrap one obvious command.
- The logic changes every run.
- The agent can safely use existing project tools.
- The script adds dependencies without improving reliability.

## Script Interface

Scripts must be non-interactive. Agents cannot answer TTY prompts reliably.

Require:

- Inputs via flags, environment variables, stdin, or files.
- `--help` with concise usage and examples.
- Helpful errors that say what failed, what was expected, and how to fix it.
- Structured stdout for data such as JSON, CSV, or TSV.
- Diagnostics, progress, and warnings on stderr.
- Meaningful exit codes.
- Idempotent behavior where possible.
- `--dry-run` or explicit confirmation flags for destructive actions.
- Bounded output with `--limit`, `--offset`, or `--output` for large results.

Pin dependencies when possible. State runtime prerequisites in the skill body or `compatibility` when they matter.

## Referencing Scripts

Reference scripts by relative path from the skill root:

```markdown
Run `python scripts/validate.py input.json`.
```

Make clear whether the agent should run the script or read it as reference. Running is preferred for utilities because it keeps script code out of context.

## Mandatory Risk Check

Before creating, modifying, or recommending a skill that includes scripts, network access, third-party content, or external downloads, perform a concise risk check.

Check:

- Does any script read secrets, home directories, SSH keys, tokens, browser data, or credential files?
- Does it write outside the requested workspace?
- Does it delete, overwrite, upload, or transmit data?
- Does it fetch remote code or depend on mutable URLs?
- Does it execute shell input built from user data without safe argument handling?
- Does it require broad permissions that are not necessary?
- Are dependencies pinned or otherwise constrained?
- Is the behavior aligned with the skill's stated purpose?

For untrusted skills, audit every bundled file before use. Treat skills like software packages: instructions and scripts can cause tool misuse, data exposure, or unauthorized changes.

If risk is high or unclear, stop and ask the user before proceeding.
