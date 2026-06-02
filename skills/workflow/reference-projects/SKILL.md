---
name: reference-projects
description: Manages local reference project repositories for feature, architecture, stack, and implementation comparisons. Use when the user asks how reference repos, similar projects, inspirations, or competitors implement something, or asks to add, update, search, explore, or compare reference repos. Do not use for ordinary package documentation lookup or for editing files inside reference repos.
---

# Reference Projects

## Overview

Manage and analyze local read-only reference repositories that live inside the user's project. Use them to compare how similar projects implement features, architecture, stack patterns, or product behavior.

## When To Use

- The user asks how a named project or reference repo implements a feature, pattern, API, UI, workflow, or architecture.
- The user asks to add, update, search, explore, list, or compare reference projects.
- The user asks how the project's references handle something, such as auth, routing, billing, tests, config, data models, or deployment.

Do not use this skill for ordinary web research, package documentation lookup, dependency installation, implementation-only tasks, or comparisons limited to files already in the main project.

## Core Rules

- Reference repos live in `.references/` at the root of the user's project, optionally grouped in topic subfolders.
- `.references/` must be ignored by git. Add `.references/` to the root `.gitignore` when missing.
- `.references/` must also be excluded from relevant project tooling. Inspect the project and update the appropriate ignore/exclude configuration for tools such as TypeScript, ESLint, Oxlint, Prettier, Oxfmt, test runners, build tools, formatters, linters, IDE indexers, or monorepo task runners when they would otherwise scan `.references/`.
- Name each clone directory as `<owner>_<repo-name>`, for example `.references/vercel_next.js` or `.references/backend/nestjs_nest`.
- Treat reference repos as read-only. Do not edit files inside them.
- Never commit reference repos or copy large chunks of reference code into the user's project.
- Do not install dependencies, run builds, run tests, or activate language tooling inside reference repos by default. Do that only with explicit user approval for a specific repo and purpose.
- Use the `explore` subagent when exploring reference repos to preserve the main context. Ask it to search specific `.references/...` paths and return cited files, findings, and relevant snippets.

## Workflow

### Add A Reference

1. Resolve the GitHub `owner/repo` and target path. Use `.references/<owner>_<repo-name>` by default, or `.references/<topic>/<owner>_<repo-name>` when grouping by backend, database, UI, auth, or another useful subject.
2. Ensure `.references/` exists, is listed in `.gitignore`, and is excluded from relevant project tooling. Adapt to the project's existing config style; do not add configs for tools the project does not use.
3. Clone shallowly:

```bash
git clone --depth 1 https://github.com/<owner>/<repo>.git .references/<owner>_<repo-name>
git clone --depth 1 https://github.com/<owner>/<repo>.git .references/<topic>/<owner>_<repo-name>
```

If the target already exists, inspect it first and ask before replacing it.

### Update References

Update one reference with:

```bash
git -C .references/<path-to-reference> pull
```

If pull fails because the clone is shallow or otherwise not recoverable, use this fallback only after confirming the target path resolves inside the root `.references/` directory and reading the existing remote URL:

```bash
rm -rf .references/<path-to-reference>
git clone --depth 1 <remote-url> .references/<path-to-reference>
```

For multiple references, update each clone separately and report failures per repo.

### Explore And Compare

1. Identify which reference repos are relevant. If unclear, list available repos under `.references/`, including nested topic folders, and ask one focused question only when selection materially changes the answer.
2. Use the `explore` subagent for broad searches inside reference repos. Give it the feature, pattern, paths to inspect, and desired thoroughness.
3. Inspect the user's project when comparison requires current behavior, architecture, or stack context.
4. Compare facts before recommendations: cited reference behavior, user's current behavior, similarities, differences, tradeoffs, and applicable ideas.

## Output

For management tasks, report repos added, updated, skipped, or failed, plus any git or tooling ignore changes.

For exploration or comparison tasks, return:

- Reference repos inspected.
- Cited paths from reference repos and the user's project when applicable.
- Observed implementation patterns.
- Key differences and constraints.
- Practical recommendations without blindly copying reference code.

## Validation

Before finishing, verify:

- [ ] `.references/` is ignored by git when reference repos were added or updated.
- [ ] `.references/` is excluded from relevant TypeScript, lint, format, test, build, IDE, or monorepo tooling that would otherwise scan it.
- [ ] Reference repo paths follow `.references/<owner>_<repo-name>` or `.references/<topic>/<owner>_<repo-name>`.
- [ ] No reference repo files were edited except controlled delete/reclone fallback during update.
- [ ] No dependencies, builds, tests, or language tooling were run inside reference repos without explicit user approval.
- [ ] Exploration used the `explore` subagent when broad reference repo search was needed.
- [ ] Comparisons cite concrete files and separate observations from recommendations.
