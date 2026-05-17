# Future Scope

These items are intentionally not implemented yet. They are candidates for future hardening if the project needs stronger automation or enterprise controls.

## Context And Retrieval

- Vector database for semantic retrieval.
- Embeddings-based RAG over `.context/`, source files, Salesforce docs, and completed task archives.
- Automatic context ranking for large requirement histories.
- Staleness detection for org-specific notes.

## Automation And Enforcement

- CI checks for branch naming, formatting, tests, and required task artifacts.
- Server-side branch protection for `master`.
- Pull request templates that require milestone review, feedback, and release checklist links.
- Git hooks that block commits when `.task/current/compliance-checklist.md` is incomplete.
- Automated detection of secrets or Salesforce auth artifacts before commit.

## Salesforce Validation

- One-command org capability detector for Agentforce licenses, enabled features, permissions, and target org readiness.
- Automated metadata deploy validation by changed metadata type.
- Agentforce simulated-preview and live-mode evidence capture.
- Automated permission set assignment verification.

## Agent Workflow

- True parallel employee agents.
- External orchestration for durable background jobs.
- Trace dashboard for role handoffs and decisions.
- Automated feedback scoring and regression reports.

## Release Management

- Automated release notes from `.task/current/`.
- Rollback package generation.
- Environment promotion model across scratch, dev, UAT, and production orgs.
- Deployment approval records tied to Git commits.
