---
name: commit-message
description: >
  Generates commit messages from git diffs and user-provided change context.
  Use when user says "write commit message", "generate commit", or invokes "/commit-message".
  Auto-triggers when committing changes.
---

# Commit Message

Write a concise commit message. Follow the Conventional Commits format. No fluff. Why over what.

## Workflow

### 1. Choose the diff source

If the user provides a raw `git diff` output, use it as the diff to analyze.

Otherwise, run `git status` to see staged/unstaged files; detect no changes at all.

Then:

1. If **Staged non-empty**: Analyze **only** `git diff --staged`. Do not include unstaged changes, even if they exist.
2. If **Staged empty**: Analyze `git diff` (unstaged changes).
3. If **Both empty**: Rely on the user's description; if none was provided, say there is nothing to commit and do not invent a message.

### 2. Gather the Change Context

When the user provides a description, intent, scope, issue link, or other context in their message:

- The selected diff is the source of truth for **what** changed.
- User context clarifies **why**, scope, or nuances not visible in the diff.
- Do not contradict the diff; if context and diff diverge, follow the diff and briefly note the mismatch.

Infer from the selected diff and any plain descriptions of changes:

1. **What changed** — files, functions, logic affected by the changes
2. **Why it changed** — bug fix, new feature, refactor, performance, etc.
3. **Who/what triggered it** — issue number, user request, tech debt, etc.

### 3. Write the Commit Message

Follow this structure:

```
<type>(<optional scope>): <short imperative summary>

<body — the story: why this change was made, what problem it solves>

<footer — issue refs, breaking change notices>
```

Apply `Rules`, `Examples`, and `Auto-Clarity` below.

#### Rules

**Commit Types:**

| Type | Use When |
| ------ | ---------- |
| `feat` | A new feature or capability is added |
| `fix` | A bug or incorrect behavior is corrected |
| `refactor` | Code restructured without changing behavior |
| `perf` | A change that improves performance |
| `docs` | Documentation only changes |
| `test` | Adding or updating tests |
| `build` | Changes to build system or dependencies |
| `ci` | CI/CD pipeline changes |
| `style` | Formatting, whitespace, missing semicolons (no logic change) |
| `chore` | Other changes that don't modify source or test files |
| `revert` | Reverting a previous commit |

**Subject line (first line):**

- Use a correct commit type from the list above
- Add `!` for breaking changes
- Use imperative mood: "add", "fix", "remove" — not "added", "adds", "adding", or "fixes"
- Max 72 characters
- No period at the end of the subject line
- Lowercase after the colon

**Body (only if needed):**

- Skip entirely when subject is self-explanatory
- Add body only for: non-obvious **why**
- Explain the **why**, not the **what** (the diff already shows the what)
- Keep lines under 100 characters
- Bullets with `-` not `*`

**Footer:**

- Add footer only for: breaking changes, short migration notes, linked issues
- Reference issues: `Closes #123`, `Fixes #456`, `Refs #789`
- Mark breaking changes: `BREAKING CHANGE: <description>`

**What NEVER goes in:**

- "This commit does X", "I", "we", "now", "currently" — the diff says what
- "As requested by..." — use Co-authored-by trailer
- "Generated with Claude Code" or any AI attribution — unless the user's own rule requires an `Assisted-by`/AI-attribution trailer, then add it as a trailer
- Emoji (unless project convention requires)
- Restating the file name when scope already says it

#### Examples

- Diff: new endpoint for user profile with body explaining the why

  ```
  feat(api): add GET /users/:id/profile

  Mobile client needs profile data without the full user payload
  to reduce LTE bandwidth on cold-launch screens.

  Closes #128
  ```

- Diff: breaking API change

  ```
  feat(api)!: rename /v1/orders to /v1/checkout

  BREAKING CHANGE: clients on /v1/orders must migrate to /v1/checkout
  before 2026-06-01. Old route returns 410 after that date.
  ```

#### Auto-Clarity

Always include body/footer for: breaking changes, security fixes, data migrations, anything reverting a prior commit. Never compress these into subject-only — future debuggers need the context.

### 4. Generate Output

Return the message in a code block ready to paste (see `Boundaries`).

---

## Multiple Commits from One Diff

If the diff contains **logically separate changes**, split them into multiple commit messages and tell the user. Use this heuristic:

- Different files with unrelated purposes → likely separate commits
- Same file but distinct concerns (e.g., bug fix + refactor) → suggest splitting
- Everything tightly coupled → one commit is fine

## Boundaries

Only generates the commit message. Follow `Workflow`. Does not run `git commit`, does not stage files, does not amend. Output the message as a code block ready to paste.
