# Best practices for MCP tools

## MCP tool references

If the skill uses MCP tools, use fully qualified names (`ServerName:tool_name`) to avoid "tool not found" errors:

```markdown
Use the BigQuery:bigquery_schema tool to retrieve table schemas.
Use the GitHub:create_issue tool to create issues.
```

## MCP-enhanced skill patterns

Skills that coordinate MCP tools benefit from additional structure:

- **Sequential orchestration**: Chain MCP calls in explicit steps with dependencies (e.g., create customer → setup payment → create subscription). Include validation between steps and rollback instructions for failures.
- **Multi-MCP coordination**: When a workflow spans multiple services (e.g., Figma export → Drive upload → Linear task creation), separate phases by service, validate before moving to the next phase, and pass data explicitly between phases.
- **Context-aware tool selection**: When different tools suit different situations, provide a decision tree (e.g., large files → cloud storage MCP, code files → GitHub MCP) rather than letting the agent guess.
