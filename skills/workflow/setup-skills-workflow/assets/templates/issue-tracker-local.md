# Issue Tracker: Local Markdown

The default issue tracker for this repo is Local Markdown. Use markdown files under `.initiatives/` for all issue tracker operations.

Read `docs/agents/local-artifacts.md` for shared initiative naming, path, and local markdown file conventions.

## Conventions

- Create, read, or update an issue: Simply use the relevant markdown file in `.initiatives/<initiative>/`
- Comment on an issue: Comments and conversation history append to the bottom of the file under a `---` separator and a `## Comments` heading
- Apply a label to an issue: Labels are recorded as a `Labels:` line near the top of the issue file
- Remove a label from an issue: Remove the label from the `Labels:` line
- Close an issue: Close the issue file by adding a `Status: closed` line near the top of the file.

## Spec and Task issues

- Spec issue: `.initiatives/<initiative>/spec.md`
- Task issues: `.initiatives/<initiative>/tasks/*.md`

Spec is like a PRD. Task issues are the implementable vertical slices from the spec.

## Link between parent and child issues

Use explicit link in the child issue body, near the top of the file:

```md
# <title>

Status: closed
Labels: [label2, label3]
Parent issue: [.initiatives/<initiative>/spec.md](.initiatives/<initiative>/spec.md)

<body>

---

## Comments

<comments>
```

## Security And Privacy

NEVER include secrets, tokens, credentials, raw personal data, sensitive customer data, or confidential material in local issue files.
