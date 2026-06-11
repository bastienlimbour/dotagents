---
name: reference-projects
description: Manages local reference project repositories for feature, architecture, stack, and implementation comparisons. Use when the user asks how reference repos, similar projects, inspirations, or competitors implement something, or asks to add, update, search, explore, or compare reference repos. Do not use for ordinary package documentation lookup or for editing files inside reference repos.
---

# Reference Projects

## Overview

Manage and analyze local read-only reference repositories inside the user's project. Use them to compare how similar projects implement features, architecture, stack patterns, or product behavior.

## When To Use

- The user asks how a named project or reference repo implements a feature, pattern, API, UI, workflow, or architecture.
- The user asks to add, update, search, explore, list, or compare reference projects.
- The user asks how project references handle auth, routing, billing, tests, config, data models, deployment, or similar concerns.

Do not use for ordinary web research, package docs lookup, dependency installation, implementation-only tasks, or comparisons limited to the main project.

## Core Rules

- Reference repos live under root `.references/`, optionally grouped by topic.
- `.references/` must be ignored by git and excluded from relevant tooling that would otherwise scan it: TypeScript, ESLint, Oxlint, Prettier, Oxfmt, tests, build tools, IDE indexers, or monorepo task runners.
- Name clones `<owner>_<repo-name>`, for example `.references/vercel_next.js` or `.references/backend/nestjs_nest`.
- Treat reference repos as read-only. Do not edit files inside them, commit them, or copy large chunks into the user's project.
- Do not install dependencies, run builds/tests, or activate language tooling inside references unless the user explicitly approves a specific repo and purpose.
- Use the `explore` subagent for broad reference repo exploration to preserve main context; ask it for cited files, findings, and relevant snippets.

## Workflow

### Add A Reference

1. Resolve GitHub `owner/repo` and target path: `.references/<owner>_<repo-name>` by default or `.references/<topic>/<owner>_<repo-name>` when grouping helps.
2. Ensure `.references/` exists, is in root `.gitignore`, and is excluded from relevant existing tooling. Do not add config for tools the project does not use.
3. Clone shallowly with `git clone --depth 1 https://github.com/<owner>/<repo>.git <target>`.

If the target exists, inspect it first and ask before replacing it.

### Update References

Update one reference with `git -C .references/<path-to-reference> pull`.

If pull fails because the clone is shallow or unrecoverable, delete/reclone only after:

- Confirming the target resolves inside root `.references/`.
- Reading the existing remote URL.

For multiple references, update each separately and report failures per repo.

### Explore And Compare

1. Identify relevant references. If unclear, list available repos under `.references/`, including topic folders, and ask one focused selection question only when it changes the answer.
2. Use `explore` for broad searches inside references; provide feature/pattern, paths, and thoroughness.
3. Inspect the user's project when comparison needs current behavior, architecture, or stack context.
4. Compare facts before recommendations: cited reference behavior, current project behavior, similarities, differences, tradeoffs, and applicable ideas.

## Output

For management tasks, report repos added, updated, skipped, or failed, plus git/tooling ignore changes.

For exploration/comparison tasks, return:

- References inspected.
- Cited paths.
- Observed patterns.
- Key differences and constraints.
- Practical recommendations without blindly copying reference code.

## Validation

Before finishing, verify:

- `.references/` is gitignored and excluded from relevant tooling when references were added or updated.
- Paths follow convention.
- No reference files were edited except controlled delete/reclone fallback.
- No dependency/build/test/tooling ran inside references without approval.
- Broad exploration used `explore`.
- Comparisons cite concrete files and separate observations from recommendations.
