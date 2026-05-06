# Agent Skill Validation Checklist

Use this checklist for a final skill audit before deployment. Every item must pass for validity.

## 1. General

* [ ] All files written in English.

## 2. Frontmatter, Metadata & Discovery

* [ ] `name` under 64 characters, lowercase, uses alphanumeric or single hyphens only.
* [ ] `name` matches skill purpose.
* [ ] Root directory name matches `name` exactly.
* [ ] `description` under 1024 characters.
* [ ] `description` is specific, includes key terms, covers use cases ("Use when..."), and exclusions if needed ("Do NOT use when...").
* [ ] `description` in third person; avoids "I", "me", "my", "you", "your".
* [ ]  No XML angle brackets (`<`, `>`) in YAML frontmatter.

## 3. File Structure & Paths

* [ ] Standard folder structure is used: `SKILL.md`, `scripts/`, `references/`, `assets/`.
* [ ] Directory does NOT contain human files like `README.md`, `CHANGELOG.md`, `INSTALLATION_GUIDE.md`.
* [ ] File paths in `SKILL.md` use forward slashes (`/`).
* [ ] Filenames are descriptive and clear at a glance.
* [ ] Long content is split across multiple reference files.

## 4. Bundled Files & References (skip if the skill doesn't have bundled files or references)

* [ ] Bundled files are referenced only one level deep from `SKILL.md` (no deep indirection; e.g., SKILL.md → reference.md → api.md → actual info).
* [ ] Bundled files are referenced from `SKILL.md` with clear "when to read" guidance.
* [ ] Bundled files are referenced using relative paths from `SKILL.md` (e.g. `[reference.md](references/reference.md)`).
* [ ] Reference files over ~100 lines include a table of contents.
* [ ] Table of contents in reference files is up to date and matches current file content.

## 5. Logic & Instructions

* [ ] `SKILL.md` under 500 lines.
* [ ] Instructions use imperative mood and direct commands (e.g., "Extract", "Run", "Validate").
* [ ] The default path is clear; alternatives appear only as escape hatches for real edge cases.
* [ ] Workflows use numbered, chronological steps with clear decision trees.
* [ ] Specific terminology consistent throughout.
* [ ] No time-sensitive content. Content does not depend on dates, versions, or changing external state.
* [ ] Examples are concrete, included only if they aid judgment or formatting.
* [ ] Command examples include required setup steps and preconditions.
* [ ] Quality-critical tasks include verification, feedback loops, or a copyable checklist when needed.

## 6. MCP Tools (skip if the skill doesn't use MCP tools)

* [ ] MCP tools referenced with fully qualified names (e.g., `ServerName:tool_name`) if used.

## 7. Scripts & Determinism (skip if the skill doesn't use scripts or executable code)

* [ ] Scripts in `scripts/` are tiny CLIs accepting arguments.
* [ ] Scripts implement feedback loops for agent self-correction (use descriptive `stdout` for success, `stderr` for failure, explicit error handling, fallbacks, and helpful messages).
* [ ] Each script single-purpose; complex logic handled by repo’s main CLI or external tools.
* [ ] No critical/irreversible actions without validation or confirmation.
* [ ] Scripts limited to relevant files and expected directories.
* [ ] All constants documented or extracted into named variables (no magic numbers).
* [ ] Required packages are listed with install commands.
* [ ] Scripts tested and verified working.

## 8. Error Handling

* [ ] `SKILL.md` includes "Error Handling", "Edge Cases", or "Troubleshooting" section for common failures or missing configs (optional but recommended).
* [ ] `SKILL.md` includes step to run validation scripts or a checklist if relevant.

## 9. Testing (optional, skip if not applicable)

* [ ] Skill triggers on obvious, expected queries.
* [ ] Skill does NOT trigger on unrelated queries.
* [ ] Ran the skill against 2-3 representative real or simulated tasks and verified output quality.
* [ ] Observed misses in activation, file navigation, or output quality and refined the skill accordingly.
* [ ] Tested and validated on intended models or runtimes when relevant.
