# Feedback Process

## Purpose

Feedback closes the loop between completed work, user acceptance, and future memory updates.

## Task-Level Feedback

For meaningful tasks, write `.task/current/feedback.md` before final closeout.

Use this structure:

```text
# Feedback

Outcome status:
User feedback summary:
Memory update needed:
Memory target:
Follow-up actions:
```

## Outcome Status

Use one of:

- `accepted`
- `needs-revision`
- `rejected`
- `pending-user-feedback`

## Memory Update Rules

Update `.context/MEMORY.md` when the feedback creates a durable rule or project fact.

Update `.context/feedback/improvement-log.md` when the feedback creates a reusable process lesson.

Update `.context/knowledge-base/` when the feedback creates reusable Salesforce or Agentforce guidance.

Do not update durable memory for one-off feedback unless the user says it should apply going forward.

## Final Closeout Rule

Before final response, Codex should state:

- whether feedback was captured
- whether memory was updated
- where the feedback or memory update was written
