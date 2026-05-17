# Knowledge Update Policy

## Purpose

The knowledge base stores reusable Salesforce and Agentforce guidance for future Codex sessions.

## Add To Knowledge Base When

- A pattern is reusable across future tasks.
- A Salesforce org or project behavior is verified and safe to record.
- A deployment, validation, or rollback practice becomes standard.
- A recurring implementation decision needs to be remembered.
- User feedback reveals a reusable preference, recurring defect, or process improvement.

## Do Not Add

- Secrets, tokens, private keys, session IDs, auth URLs, passwords, or refresh tokens.
- One-off task details that belong only in `.task/current/`.
- Raw feedback that has not been interpreted or verified.
- Unverified guesses.
- Large copied files or generated logs.

## Where To Put Information

- Short durable summary: `.context/MEMORY.md`
- Reusable Agentforce guidance: `.context/knowledge-base/salesforce-agentforce.md`
- Repo structure facts: `.context/knowledge-base/project-map.md`
- Repeatable process guidance: `.context/knowledge-base/development-workflow.md`
- Validation and deploy guidance: `.context/knowledge-base/validation-and-release.md`
- Feedback trends and lessons: `.context/feedback/improvement-log.md`
- Long task summaries: `.context/completed-tasks/`
- Org-specific safe notes: `.context/salesforce-org-notes/`

## Staleness Rule

When a note depends on live org state, mark it with the date and org alias. Verify it again before using it for deployment or production-impacting decisions.
