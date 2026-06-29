# Issue Tracker: GitHub

The default issue tracker for this repo is GitHub. Use `gh` CLI for all issue tracker operations.

## Conventions

- Create an issue: `gh issue create --title "<title>" --body "<body>"`. Use a heredoc for multi-line bodies.
- Read an issue: `gh issue view <number> --json number,title,labels,body,comments --jq '{number, title, labels: [.labels[].name], body, comments: [.comments[].body]}'`
- List issues (without body or comments): `gh issue list --state open --json number,title,labels --jq 'map({number, title, labels: [.labels[].name]})'`
- List issues (with body and comments): `gh issue list --state open --json number,title,labels,body,comments --jq 'map({number, title, labels: [.labels[].name], body, comments: [.comments[].body]})'`
- Comment on an issue: `gh issue comment <number> --body "<body>"`
- Apply a label to an issue: `gh issue edit <number> --add-label "<label>"`
- Remove a label from an issue: `gh issue edit <number> --remove-label "<label>"`
- Close an issue: `gh issue close <number> --comment "<reason>"`

## Link between parent and child issues

The `gh` CLI does not support native parent/child relationships between issues. Use explicit link in the child issue body, near the top of the file:

```md
# <title>

Parent issue: #<parent-issue-number>

<body>
```

## Closing Issues

Agents must not close issues unless explicitly instructed or allowed by user.

## Security And Privacy

NEVER include secrets, tokens, credentials, raw personal data, sensitive customer data, or confidential material in issues or comments.
