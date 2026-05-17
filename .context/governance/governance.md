# Governance

## Ownership Model

Codex is the execution manager. The user remains the owner of business intent, org access, production approval, and final release decisions.

## Governance Principles

- Requirements must be explicit before implementation.
- Behavior-changing work must satisfy the test-first policy before implementation.
- Salesforce metadata changes must be scoped and reviewable.
- Meaningful requirement work must happen on a feature or requirement branch.
- Agentforce behavior changes must account for Agent Script, tools, Apex, flows, prompt templates, and permissions.
- Validation evidence must be captured before a task is marked done.
- Completed file-change tasks must be committed to Git after validation and review.
- Deployment, publishing, permission assignment, and destructive operations require explicit user approval.
- Live sign-in, MFA, license assignment, tenant consent, and admin portal decisions remain user-owned.

## Risk Levels

`low`:

- docs-only changes
- local task/context updates
- narrow formatting changes
- non-runtime metadata comments or descriptions

`medium`:

- Apex implementation changes
- Flow or prompt template changes
- Agent Script reasoning or tool changes
- permission metadata changes
- package manifest changes

`high`:

- live deploys
- agent publishing
- permission assignment
- auth/org alias/default-org changes
- destructive metadata operations
- changes that affect production runtime behavior

## Required Evidence

Each meaningful task should leave evidence in `.task/current/`:

- intent and requirements
- architecture
- implementation plan
- test plan and outcomes
- test-first evidence or documented exception
- code review
- milestone/governance review
- branch name
- git commit hash for completed file-change tasks
- release checklist when release is in scope
