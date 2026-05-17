# Process Exceptions

## Purpose

Some tasks cannot satisfy every process requirement. Exceptions are allowed only when they are explicit, narrow, and documented.

## Allowed Exceptions

- Docs-only or governance setup work may happen on `master` only when the user explicitly requested the setup and the exception is recorded.
- Validation may be limited when no Salesforce org alias or auth is available.
- Apex tests may be skipped only when no Apex behavior changed or when org validation is unavailable and documented.
- Release checklist may be omitted only when release, deploy, publish, or merge is out of scope.
- Feedback may remain `pending-user-feedback` when the user has not yet accepted or rejected the result.

## Not Allowed As Exceptions

- storing secrets in repo files
- deploying without explicit user approval
- publishing or activating an Agentforce agent without explicit user approval
- committing ignored local auth/session artifacts
- silently skipping review or governance checks
- merging to `master` without explicit user approval

## Exception Format

Record exceptions in `.task/current/compliance-checklist.md`:

```text
Exception:
Reason:
Risk:
User approval:
Follow-up:
```
