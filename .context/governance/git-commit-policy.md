# Git Commit Policy

## Rule

Every completed file-change task must be committed to Git after validation and review.

## Commit Timing

Commit when:

- the requested file changes are complete
- validation has run, or limitations are documented
- code review and governance review are complete
- generated or local-only files are excluded

Do not commit in the middle of an incomplete task unless the user asks for an intermediate checkpoint.

## Commit Scope

Each commit should represent one coherent task or milestone. Avoid mixing unrelated Salesforce metadata changes, context updates, and environment repair unless they are part of the same requested setup task.

Commits for meaningful requirements should be made on a feature or requirement branch. Direct commits to `master` are allowed only for explicit repository setup, documentation-only governance updates, or emergency repair approved by the user.

## Commit Message

Use concise, imperative messages:

```text
Add Salesforce governance workflow
Update Agentforce validation runbook
Fix WeatherService date handling
```

## Push Policy

Commit locally by default. Do not push unless the user explicitly asks.

Do not merge back to `master` unless the user explicitly asks.

## Exclusions

Never commit:

- secrets or credentials
- local Salesforce auth/session files
- `node_modules`
- generated logs
- temporary scratch files
- files ignored by `.gitignore`
