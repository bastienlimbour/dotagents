# Agent Skill Validation Checklist

Use this checklist to perform a final audit of a skill before deployment. Every item must pass to ensure the skill is discoverable, lean, and deterministic.

## 1. General

* [ ] **Language:** All files are written in English.

## 2. Metadata & Discovery

* [ ] **Naming Format:** The `name` field is 1-64 characters, lowercase, and contains only numbers or single hyphens.
* [ ] **Naming Semantics:** The `name` is consistent with the skill's purpose.
* [ ] **Directory Match:** The `name` field exactly matches the parent directory name.
* [ ] **Description Length:** The description is under 1,024 characters.
* [ ] **Trigger Optimization:** The description is specific, includes key terms, and covers both use cases ("Use when...") and negative triggers ("Don't use for...").
* [ ] **Third-Person Tone:** The description avoids "I", "me", "my", "you", or "your".

## 3. File Structure & Paths

* [ ] **Flat Hierarchy:** All files in `scripts/`, `references/`, and `assets/` are exactly one level deep (no nested subfolders).
* [ ] **Standard Folders:** Only `scripts/`, `references/`, and `assets/` are used.
* [ ] **No Human Docs:** The directory contains NO `README.md`, `CHANGELOG.md`, or `INSTALLATION_GUIDE.md`.
* [ ] **Forward Slashes:** All file paths in `SKILL.md` use forward slashes (`/`) regardless of the operating system.
* [ ] **No Reference Chains:** `SKILL.md` links directly to actionable bundled files instead of routing the agent through reference-to-reference indirection to reach core instructions.
* [ ] **Descriptive Filenames:** Bundled file names clearly convey their content at a glance.
* [ ] **Content Splitting:** Long content is split across multiple reference files rather than crammed into one.
* [ ] **Table of Contents Exists:** Long reference files include a table of contents for navigability.
* [ ] **Table of Contents Accuracy:** Table of contents matches the actual file content.

## 4. Logic & Instructions (SKILL.md)

* [ ] **Lean Context:** The `SKILL.md` file is under 500 lines.
* [ ] **Imperative Mood:** Instructions use direct commands (e.g., "Extract," "Run," "Validate").
* [ ] **Deterministic Steps:** The workflow is a numbered, chronological sequence with clear decision trees.
* [ ] **Scope Boundaries:** `SKILL.md` clearly defines scope, "when to use", and "when not to use" boundaries.
* [ ] **Progressive Disclosure:** Large schemas, templates, or rule sets are stored in `references/` or `assets/` and each actionable bundled file is referenced from `SKILL.md` with clear "when to read" guidance.
* [ ] **Specific Terminology:** Uses domain-native terms consistently (e.g., "component" instead of "file").
* [ ] **No Time-Sensitive Information:** Content does not depend on dates, versions, or external state that will go stale.
* [ ] **Concrete Examples:** Examples are concrete (not abstract) and only included when they improve judgment or formatting.
* [ ] **MCP Tool References:** MCP tools are referenced using fully qualified names (`ServerName:tool_name`).
* [ ] **Feedback Loops:** Quality-critical tasks include a verification or feedback step.

## 5. Scripts & Determinism

* [ ] **CLI Design:** Scripts in `scripts/` are designed as tiny CLIs that take arguments.
* [ ] **Feedback Loop:** Scripts provide descriptive `stdout` for success and `stderr` for failure, with explicit error handling, fallbacks, and helpful messages to allow agent self-correction.
* [ ] **No Library Code:** Scripts are single-purpose; complex logic is offloaded to the repository's standard CLI or external tools.
* [ ] **Safety:** Scripts do not perform critical or irreversible actions without validation or confirmation.
* [ ] **Scope:** Script scope is limited to relevant files and expected directories.
* [ ] **No Magic Numbers:** All constants are documented or extracted into named variables.
* [ ] **Dependencies:** Required packages are listed with install commands.
* [ ] **Tested:** Scripts are tested and verified as working.

## 6. Error Handling

* [ ] **Edge Cases:** The `SKILL.md` includes an "Error Handling" section addressing common failure states or missing configurations.
* [ ] **Validation:** The `SKILL.md` includes a step to run validation scripts where applicable.

## 7. Testing (if the environment supports it)

* [ ] **Positive Trigger:** Skill triggers on obvious, expected queries.
* [ ] **Negative Trigger:** Skill does NOT trigger on unrelated queries.
* [ ] **End-to-End Run:** Ran the skill against a real or simulated use case and verified output quality.
