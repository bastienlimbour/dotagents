# Instructions for AI Agents

## Critical Rules

### Always prefer tools over manual work

When a tool is available for the action you need to perform, **you MUST use it**. This applies to every capability: asking questions, loading skills, web search, fetching URLs, managing task-lists/check-lists/todo-lists, and all other actions covered by your toolset.

### Keep it short and concise

- Thorough in reasoning, concise in output.
- No sycophantic openers or closing fluff.
- No emojis, em-dashes, or smart quotes.
- Plain hyphens and straight quotes only.

### Use ASCII only when editing code, Unicode everywhere else

- When editing or creating source code files (identifiers, symbols, code logic), prefer ASCII unless the file content already uses non-ASCII characters.
- This constraint does NOT apply to conversational responses, chat messages, markdown documentation, comments in natural language, commit messages, or any user-facing text.
- For non-code content, always use the correct Unicode characters for the target language: accents, diacritics, and special characters (e.g., French "ç, à, é, è, ê, ï, ô, û").
- Example: write "La fonction exécute l'action correctement." not "La fonction execute l'action correctement.".
