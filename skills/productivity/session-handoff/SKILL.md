---
name: session-handoff
description: Compact the current conversation into a handoff document for another agent to pick up. Use when user asks to handoff the conversation to another agent.
---

## Instructions

Write a handoff document summarising the current conversation so a fresh agent can continue the work. Save it to the temporary directory of the user's OS, not in the current workspace.

If the user provided information about the next session, treat it as a description of what the next session will focus on and tailor the handoff document accordingly.

## Rules

The next session will be with a different agent. The document must contain all relevant informations to continue the work. The next agent must understand what to read, and what to do first.

Do not duplicate content already captured in other artifacts (docs, PRDs, specs, plans, tasks, briefs, ADRs, issues, commits, diffs). Reference them by path or URL instead.

Redact any sensitive information, such as secrets, API keys, tokens, credentials, or personally identifiable information.

If a skill is likely to be useful for the next session or the user mentioned it, include a "suggested skills" section in the document, which suggests skills that the next agent should invoke.

Write synthesis, not a transcript. Keep it compact, action-oriented, and reference-heavy.

## Output

- Write the handoff document to the temporary directory of the user's OS.
- Provide the path to the handoff document to the user in the response.
