---
name: brainstorm
description: Runs divergent brainstorming for an early idea, project, feature, or opportunity while capturing the session in a local brainstorming artifact. Use when the user wants to explore options, angles, personas, use cases, differentiation, constraints, or wild ideas.
---

# Brainstorm

## Overview

Explore an open idea broadly while preserving useful context in a lightweight local brainstorming artifact. The goal is "more and better options", NOT premature convergence or implementation decisions.

## When To Use

- The user wants to brainstorm, ideate, explore, riff, widen options, or think through an early product, feature, project, or technical opportunity.
- The problem, audience, solution shape, positioning, use cases, or constraints are still open.
- More angles, personas, alternatives, or differentiators would reduce ambiguity before a brief, spec, prototype, or implementation.

Do not use this skill for market validation, deep technical research, writing a spec, splitting tasks, creating issues, code implementation, ordinary Q&A, or decision grilling.

## Core Principle

Divergence by default. Treat each user answer as material to expand into more possibilities, not as a decision to lock into a product rule, architecture choice, MVP scope, or implementation detail.

## Workflow

### 1. Establish The Artifact

Resolve the initiative and brainstorming artifact before writing. Use the project's local artifact conventions for paths, naming, and creation rules.

- Start from any user-provided initiative or artifact path; otherwise inspect existing initiatives and artifacts for a match to the current context.
- If nothing matches, propose a new initiative and a `brainstorming.md` artifact.
- Report findings: matched initiative, matched artifact, proposed create/update action, and any ambiguity.
- Ask for confirmation before creating an initiative, creating an artifact, or updating an existing artifact.
- After confirmation, create or update the artifact as needed using [brainstorming.md](assets/templates/brainstorming.md) template. For new artifacts, summarize the starting context in `## Starting Context`, and never rewrite it after the session starts.

Update the confirmed brainstorming artifact throughout the session without asking again for each write; the initial confirmation covers live brainstorming updates.

If the user explicitly declines an artifact, continue in conversation only and clearly state that no persistent brainstorming source will be maintained.

### 2. Frame Lightly Before Diverging

Before generating lots of ideas, capture the minimum useful starting context:

- The initial idea.
- The problem to solve or opportunity to capitalize on.
- Target users or personas known so far.
- Desired success or outcome.
- Known constraints and non-goals.

Use code, docs, issues, specs, briefs, ADRs, or project notes to answer factual context questions before asking the user. Ask the user only for context that cannot be inferred or where sources conflict.

### 3. Diverge Actively

Act as a thinking partner, not a passive idea list generator. Be curious, exploratory, and divergent.

- Ask one question at a time and wait for the answer.
- Before a question, provide concise context, a provocative angle, or several divergent directions when useful.
- Prefer multiple-choice questions only when they open exploration paths. Avoid choices that force a decision between implementation options.
- For each question, provide your recommendation.
- After each meaningful user answer, expand the idea space before asking the next question: suggest variants, adjacent concepts, opposing approaches, wild versions, simpler versions, or persona-specific versions.
- Challenge weak assumptions, surface hidden constraints, and suggest unexpected alternatives.
- Do not force convergence, the user is still exploring.

Use ideation angles selectively, not as a checklist:

- Inversion: explore the opposite of the initial idea.
- Simplification: remove features, steps, or complexity.
- Constraint removal: imagine no time, budget, or technical constraint, then return to reality.
- Persona shift: change the user segment or buyer.
- Analogy: borrow a model from another product, industry, or domain.
- 10x version: push beyond incremental improvements.
- Decomposition: split the problem into parts and recombine ideas.

### 4. Maintain The Artifact

Use the [brainstorming.md](assets/templates/brainstorming.md) template to guide the artifact.

- When the user gives a concrete idea or preference, keep the idea in `## Ideas`, update its inline tag or note if scope is explicit, then broaden around it. Do not immediately ask for the next decision in the chain.
- Keep `brainstorming.md` simple Markdown with no frontmatter or metadata block. Preserve useful existing content and reorganize only when it improves clarity.
- Keep all brainstormed material under `## Ideas`, organized by themes or exploration angles adapted to the conversation, such as `Problems`, `Personas`, `Use Cases`, `Feature Ideas`, `Differentiation Angles`, `Risks And Constraints`, `Wild Ideas`, `Pricing`, `Distribution`, or `Technical Bets`, or any other category that makes sense for the conversation.
- Each idea should appear once. Do not duplicate an idea in separate sections for MVP, later, rejected, questions, or assumptions.

Use inline tags at the start of each idea when helpful:

- `[Explore]` for ideas still being opened up or not scoped yet.
- `[Current scope]` for ideas explicitly kept for the current initiative scope (feature, MVP, V1, etc.).
- `[Later]` for ideas explicitly kept for a future improvement (not the scope of the current initiative but still useful).
- `[Rejected]` for ideas explicitly excluded or refused.

Do not infer `[Current scope]`, `[Later]`, or `[Rejected]` from weak preferences. Use these tags only when the user is explicit, or when the conversation makes the scope unambiguous. Otherwise use `[Explore]`.

Attach short notes under ideas for source, nuance, reason, explicit user decision, risk, constraint, or unresolved question. Avoid creating separate sections for open questions, assumptions, deferred ideas, rejected ideas, or final synthesis.

Do not rewrite the artifact as a product requirements document while brainstorming.

### 5. Close The Session

When the session naturally matures, optionally clean up `## Ideas` by merging duplicates, tightening notes, and making scope tags explicit where the user has clearly decided. Do not add a final synthesis section unless the user explicitly asks for one.

## Guardrails

- Do not produce a spec, task list, decision log, or implementation plan.
- Do not conduct deep market, competitor, technical, legal, or business validation by default; attach relevant risks or uncertainties as notes to the related ideas instead.
- Do not turn the session into a sequence of decisions unless the user explicitly asks to converge on a direction.
- Do not answer architecture, schema, storage, API, naming, or task-breakdown questions as the main thread. Attach them as notes to the relevant idea and return to idea exploration.
- If the user says the conversation is becoming too technical, too functional, too decision-oriented, or too narrow, immediately stop that line, summarize the drift, and suggest 3-5 broader exploration paths. Ask which path to explore next.

## Question examples

Bad example (avoid):

```text
Should we do X, Y, or Z?
```

Better example:

```text
The idea opens several product directions: X because ..., Y because ..., Z because .... Which approach feels most promising to explore?
```

Better example (do):

```text
There are several ways the product could help users: X can ..., Y can ..., Z can .... Which approach feels most promising to explore?
```

## Output

During the run, provide:

- The proposed initiative and brainstorming artifact, then one confirmation question before writing.
- One brainstorming question at a time, with options or recommendations when useful.
- Periodic concise summaries when a branch is resolved or the artifact has materially changed.
- A concise closing summary of the main explored themes and any explicit `[Current scope]`, `[Later]`, or `[Rejected]` ideas, with the artifact updated.
