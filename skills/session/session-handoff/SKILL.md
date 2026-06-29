---
name: session-handoff
description: Compact the current conversation into a handoff document for another agent to pick up. Use when user asks to handoff the conversation to another agent.
---

# Session Handoff

Write a compact handoff document so a fresh agent can continue the work. Save it to the user's OS temporary directory, not the current workspace.

## Rules

- If the user provided arguments or next-session focus, tailor the handoff to that focus.
- Include all relevant context for continuation: what happened, what to read, current state, decisions, blockers, and what to do first.
- Reference existing artifacts by path or URL instead of duplicating docs, PRDs, specs, plans, tasks, briefs, ADRs, issues, commits, or diffs.
- Redact secrets, API keys, tokens, credentials, and personally identifiable information.
- Include `Suggested Skills` when a skill is likely useful next or was mentioned by the user.
- Write synthesis, not a transcript. Keep it compact and action-oriented.

## Output

- Write the handoff document to the OS temporary directory.
- Return the handoff path to the user.
