# Org2Agentforce Codex Operating Contract

This repository is a Salesforce DX project for Agentforce development. Codex is the execution manager. Role files under `.agents/roles/` are the employee agents. File-backed context under `.context/` is the project memory. Work proceeds through `.task/current/` so requirements, decisions, tests, and review evidence remain inspectable and Git-backed.

## Core Rules

1. Use `gpt-5.5` with `xhigh` reasoning for this repo.
2. Read `.context/MEMORY.md` before planning meaningful work.
3. Keep Salesforce metadata changes scoped to `force-app/main/default` unless the task explicitly asks for project configuration.
4. Treat `sfdx-project.json`, `force-app/main/default/aiAuthoringBundles`, Apex classes, flows, prompt templates, permission sets, and package manifests as deployment-sensitive assets.
5. Do not modify auth state, org aliases, deployment targets, or scratch org config without stating the intended command and expected org impact first.
6. Do not deploy, assign permissions, publish agents, or run destructive metadata operations unless the user explicitly asks.
7. For behavior-changing work, satisfy the test-first gate in `.context/governance/test-first-policy.md` before implementation. Apex changes must use test-first or test-updated-first work when an authenticated org and relevant tests are available.
8. For Agentforce authoring changes, keep Agent Script, tools, prompt templates, flows, Apex invocables, and permission metadata consistent.
9. Preserve existing Salesforce naming conventions and metadata folder structure.
10. Every completed file-change task must be committed to Git after validation and review. Do not leave completed changes unstaged or uncommitted.
11. Use a feature or requirement branch for every meaningful requirement before changing files. Do not implement directly on `master` except for explicit repository setup or emergency repair approved by the user.
12. Capture task feedback before final closeout and update memory only with reusable, verified lessons.

## File-Backed Context

This project uses Markdown files, not a vector database, for persistent context.

Before planning:

1. Read `.context/MEMORY.md`.
2. Inspect relevant files under `.context/knowledge-base/` for Salesforce and Agentforce guidance that applies to the request.
3. Inspect `.context/governance/governance.md`, `.context/governance/guardrails.md`, and `.context/governance/milestone-review.md` for governance and approval rules.
4. Inspect `.context/governance/compliance-checklist.md` and `.context/governance/process-exceptions.md` for the required closeout checks and exception rules.
5. Inspect `.context/feedback/improvement-log.md` when prior feedback may affect the current request.
6. Inspect relevant files under `.context/decisions/`, `.context/patterns/`, `.context/salesforce-org-notes/`, and `.context/completed-tasks/` only when they relate to the current request.
7. If prior context is unclear or stale, state the uncertainty and verify from source files or Salesforce CLI output.

After meaningful work:

1. Update `.task/current/` with task evidence.
2. Add durable lessons to `.context/MEMORY.md` only when they should guide future work.
3. Add or update `.context/knowledge-base/` entries when a reusable Salesforce or Agentforce practice is discovered.
4. Capture task outcome and user feedback in `.task/current/feedback.md`.
5. Add durable feedback trends to `.context/feedback/improvement-log.md`.
6. Add detailed notes under the relevant `.context/` subfolder when the detail is useful but too long for `MEMORY.md`.

Do not store secrets, access tokens, session IDs, private keys, or credentials in `.context/`.

## File-Based Knowledge Base

The knowledge base is not a vector DB or automated RAG system. It is curated Markdown that Codex reads when relevant.

Use these files first:

1. `.context/knowledge-base/salesforce-agentforce.md`
2. `.context/knowledge-base/project-map.md`
3. `.context/knowledge-base/development-workflow.md`
4. `.context/knowledge-base/validation-and-release.md`
5. `.context/knowledge-base/knowledge-update-policy.md`
6. `.context/governance/git-commit-policy.md`
7. `.context/governance/branching-policy.md`
8. `.context/governance/test-first-policy.md`
9. `.context/feedback/feedback-process.md`
10. `.context/governance/compliance-checklist.md`
11. `.context/governance/process-exceptions.md`
12. `.context/knowledge-base/future-scope.md`

Update the knowledge base only with reusable guidance, stable project facts, or verified lessons. Keep task-specific evidence in `.task/current/` and completed task summaries in `.context/completed-tasks/`.

## Codex-Only Employee Workflow

Use the role files in this order unless the task is clearly narrower:

1. `.agents/roles/product-analyst.md`
2. `.agents/roles/salesforce-architect.md`
3. `.agents/roles/implementation-engineer.md`
4. `.agents/roles/test-engineer.md`
5. `.agents/roles/code-reviewer.md`
6. `.agents/roles/governance-reviewer.md`
7. `.agents/roles/feedback-reviewer.md`
8. `.agents/roles/release-engineer.md`

For each meaningful task, create or update:

```text
.task/current/intent.md
.task/current/requirements.md
.task/current/architecture.md
.task/current/implementation-plan.md
.task/current/test-plan.md
.task/current/review.md
.task/current/milestone-review.md
.task/current/feedback.md
.task/current/compliance-checklist.md
.task/current/release-checklist.md
```

Small, low-risk edits may use a compressed version of the workflow, but Codex must still know the acceptance criteria and validation command before editing.

## SDLC Enforcement

1. Plan before coding and state confidence as `HIGH`, `MEDIUM`, or `LOW`.
2. If confidence is low, inspect more project evidence or ask the user.
3. Complete milestone review checkpoints before crossing from requirements to architecture, architecture to implementation, implementation to validation, validation to release, or release to deploy.
4. Create or confirm the task branch before changing files for a meaningful requirement.
5. Write or update tests or scenario evidence before implementation when behavior changes.
6. Run the new or updated test/scenario before implementation when technically possible, and record the failing result or documented gap in `.task/current/test-plan.md`.
7. Run the narrowest relevant verification after implementation, then broader validation when the change risk requires it.
8. Self-review the exact diff before final response.
9. Capture feedback status and memory-update decision before final closeout.
10. Complete `.task/current/compliance-checklist.md` before committing.
11. Commit every completed file-change task with a clear message after validation and review.
12. Do not push, deploy, publish, or merge to `master` unless the user explicitly asks.

## Salesforce Validation Defaults

Use the available commands based on the changed surface:

```powershell
npm run prettier:verify
sf project deploy validate --source-dir force-app --target-org <alias> --test-level RunLocalTests
sf apex run test --target-org <alias> --test-level RunLocalTests --wait 30 --result-format human
sf project deploy start --source-dir force-app --target-org <alias> --test-level RunLocalTests --wait 60
```

If no org alias is known, report that validation is limited to local metadata and formatting checks. Live Salesforce sign-in remains user-owned; Codex owns command shape, scope, and verification after sign-in.

## Definition Of Done

A task is done only when:

1. Requirements and acceptance criteria are clear.
2. Implementation is scoped to the approved Salesforce metadata.
3. Test-first evidence exists for behavior changes, or a documented exception explains why it does not apply.
4. Tests or validation commands have been run, or the limitation is explicitly reported.
5. A review pass has checked metadata consistency, permissions, and deployment risk.
6. A governance review has checked guardrails, approval requirements, milestone status, and residual risk.
7. Work was completed on an appropriate feature or requirement branch, unless the branch exception is documented.
8. Feedback status and memory-update decision are recorded.
9. The compliance checklist is complete, or every unchecked item has a documented exception.
10. The completed file-change set is committed to Git.
11. Release notes include deploy command, target org assumptions, rollback path, and residual risk.
