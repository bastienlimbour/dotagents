# Issue Tracker: GitLab

The default issue tracker for this repo is GitLab. Use `glab` CLI for all issue tracker operations.

## Conventions

- Create an issue: `glab issue create --title "<title>" --description "<description>"`. Use a heredoc for multi-line descriptions.
- Read an issue: `glab issue view <number> --comments -F json --jq '{number, title, labels: [.labels[].name], body, comments: [.comments[].body]}'`
- List issues (without body or comments): `glab issue list -F json --jq 'map({number, title, labels: [.labels[].name]})'`
- List issues (with body and comments): `glab issue list -F json --jq 'map({number, title, labels: [.labels[].name], body, comments: [.comments[].body]})'`
- Comment on an issue: `glab issue note <number> --message "<message>"`
- Apply a label to an issue: `glab issue update <number> --label "<label>"`
- Remove a label from an issue: `glab issue update <number> --remove-label "<label>"`
- Close an issue: `glab issue close <number>`

## Link between parent and child issues

The `glab` CLI does not support native parent/child relationships between issues. Use explicit link in the child issue body, near the top of the file:

```md
# <title>

Parent issue: #<parent-issue-number>

<body>
```

## Closing Issues

Agents must not close issues unless explicitly instructed or allowed by user.

## Security And Privacy

NEVER include secrets, tokens, credentials, raw personal data, sensitive customer data, or confidential material in issues or comments.
