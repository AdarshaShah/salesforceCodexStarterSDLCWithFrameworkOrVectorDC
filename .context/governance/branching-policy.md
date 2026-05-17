# Branching Policy

## Rule

Use a feature or requirement branch for every meaningful requirement before changing files.

## Branch Names

Use lowercase, hyphen-separated names:

```text
feature/<short-requirement>
requirement/<short-requirement>
fix/<short-bug>
docs/<short-doc-task>
chore/<short-maintenance-task>
```

Examples:

```text
feature/add-weather-tool-context
requirement/local-info-agent-hours
fix/weather-service-null-location
docs/update-agentforce-runbook
chore/add-governance-policy
```

## When To Create The Branch

Create or confirm the branch after requirements are clear and before implementation begins.

Use:

```powershell
git checkout -b feature/<short-requirement>
```

If the branch already exists:

```powershell
git checkout feature/<short-requirement>
```

## Protected Base

Treat `master` as the protected base branch.

Direct commits to `master` are allowed only for:

- explicit repository setup requested by the user
- governance/process updates requested by the user
- emergency repair approved by the user

## Merge Policy

Do not merge to `master` unless the user explicitly asks.

Before merge, the task should have:

- validation evidence
- code review
- governance review
- local commit on the task branch
- release checklist when release is in scope

## Evidence

Record the active branch in `.task/current/milestone-review.md` for meaningful work.
