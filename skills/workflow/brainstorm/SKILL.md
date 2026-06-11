---
name: brainstorm
description: Runs divergent brainstorming for an early idea, project, feature, or opportunity while capturing the session in a local brainstorming artifact. Use when the user wants to explore options, angles, personas, use cases, differentiation, constraints, or wild ideas.
---

# Brainstorm

## Overview

Explore an open idea broadly while preserving useful context in a lightweight local brainstorming artifact. Optimize for more and better options, not premature convergence.

## When To Use

- The user wants to brainstorm, ideate, explore, riff, widen options, or think through an early product, feature, project, or technical opportunity.
- The problem, audience, solution shape, positioning, use cases, constraints, or differentiators are still open.

Do not use for validation, specs, implementation, or decision grilling.

## Core Principle

Divergence by default. Treat each user answer as material to expand, not as a decision to lock into product rules, scope, architecture, or implementation.

## Workflow

### 1. Resolve Target

Resolve the initiative and brainstorming artifact before live writing.

- Respect local artifact conventions already in context. If absent, use `.initiatives/<NNN-slug>/brainstorming.md` with simple Markdown and no frontmatter.
- Start from any user-provided initiative or path; otherwise inspect existing initiatives and artifacts for a likely match.
- If updating, inspect the existing artifact and preserve useful content.
- If no target matches, propose one initiative and artifact path.
- Report the matched or proposed target, create/update mode, and ambiguity. Ask for confirmation before creating an initiative or selecting a path.

Target confirmation approves only the artifact path. Do not draft substantive content during this step. If the user declines an artifact, continue in conversation only.

### 2. Frame Starting Context

Before generating many ideas, capture the minimum useful context for the conversation and `## Starting Context`:

- Initial idea.
- Problem or opportunity.
- Target users or personas.
- Desired outcome.
- Constraints and non-goals.
- Relevant existing context.

Use code, docs, issues, specs, briefs, ADRs, or project notes to answer factual context questions before asking the user. Ask only when sources are missing, conflicting, or insufficient.

### 3. Write Live When Confirmed

If an artifact is active, create or update it after target confirmation and starting-context framing using [brainstorming.md](assets/templates/brainstorming.md). For new artifacts, write `## Starting Context` once and do not rewrite it after the session starts.

After initial target confirmation, update the artifact throughout the session without asking again. This live-write exception applies only to the confirmed brainstorming artifact.

### 4. Diverge Actively

Act as a thinking partner, not a passive idea list generator.

- Ask one question at a time and wait for the answer.
- Before a question, provide concise context, a provocative angle, or divergent directions when useful.
- Provide a recommendation with each question, but avoid forcing implementation choices.
- After meaningful answers, broaden before asking the next question: variants, adjacent concepts, opposite approaches, wild versions, simpler versions, or persona-specific versions.
- Challenge weak assumptions, surface hidden constraints, and suggest unexpected alternatives.
- Do not force convergence unless the user explicitly asks.

Use ideation angles selectively, not as a checklist:

- Inversion.
- Simplification.
- Constraint removal.
- Persona shift.
- Analogy.
- 10x version.
- Decomposition.

### 5. Maintain The Artifact

Use [brainstorming.md](assets/templates/brainstorming.md) as the structure.

- Keep brainstormed material under `## Ideas`, grouped by useful themes.
- Keep each idea once; avoid separate sections for MVP, later, rejected, questions, assumptions, or synthesis.
- Use inline tags when helpful: `[Explore]`, `[Current scope]`, `[Later]`, `[Rejected]`.
- Use `[Current scope]`, `[Later]`, or `[Rejected]` only when explicit or unambiguous; otherwise use `[Explore]`.
- Attach short notes for source, nuance, explicit decision, risk, constraint, or unresolved question.
- Preserve useful existing content and reorganize only when it improves clarity.

Do not rewrite the artifact as a product brief, spec, task list, decision log, or implementation plan.

If the session drifts too technical, functional, decision-oriented, or narrow, stop that line, summarize the drift, suggest 3-5 broader paths, and ask which to explore next.

## Output

End with a concise summary of explored themes, key ideas captured, artifact path if any, and remaining `[Explore]` ideas.
