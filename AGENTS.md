# Org2Agentforce Codex Operating Contract

This repository is a Salesforce DX project for Agentforce development. Codex is the execution manager. Role files under `.agents/roles/` are the employee agents. File-backed context under `.context/` is the project memory. Work proceeds through `.task/current/` so requirements, decisions, tests, and review evidence remain inspectable and Git-backed.

## Core Rules

1. Use `gpt-5.5` with `xhigh` reasoning for this repo.
2. Read `.context/MEMORY.md` before planning meaningful work.
3. Keep Salesforce metadata changes scoped to `force-app/main/default` unless the task explicitly asks for project configuration.
4. Treat `sfdx-project.json`, `force-app/main/default/aiAuthoringBundles`, Apex classes, flows, prompt templates, permission sets, and package manifests as deployment-sensitive assets.
5. Do not modify auth state, org aliases, deployment targets, or scratch org config without stating the intended command and expected org impact first.
6. Do not deploy, assign permissions, publish agents, or run destructive metadata operations unless the user explicitly asks.
7. For Apex changes, prefer test-first or test-updated-first work. Run the narrowest relevant Apex test before broader validation.
8. For Agentforce authoring changes, keep Agent Script, tools, prompt templates, flows, Apex invocables, and permission metadata consistent.
9. Preserve existing Salesforce naming conventions and metadata folder structure.
10. Every completed file-change task must be committed to Git after validation and review. Do not leave completed changes unstaged or uncommitted.

## File-Backed Context

This project uses Markdown files, not a vector database, for persistent context.

Before planning:

1. Read `.context/MEMORY.md`.
2. Inspect relevant files under `.context/knowledge-base/` for Salesforce and Agentforce guidance that applies to the request.
3. Inspect `.context/governance/governance.md`, `.context/governance/guardrails.md`, and `.context/governance/milestone-review.md` for governance and approval rules.
4. Inspect relevant files under `.context/decisions/`, `.context/patterns/`, `.context/salesforce-org-notes/`, and `.context/completed-tasks/` only when they relate to the current request.
5. If prior context is unclear or stale, state the uncertainty and verify from source files or Salesforce CLI output.

After meaningful work:

1. Update `.task/current/` with task evidence.
2. Add durable lessons to `.context/MEMORY.md` only when they should guide future work.
3. Add or update `.context/knowledge-base/` entries when a reusable Salesforce or Agentforce practice is discovered.
4. Add detailed notes under the relevant `.context/` subfolder when the detail is useful but too long for `MEMORY.md`.

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

Update the knowledge base only with reusable guidance, stable project facts, or verified lessons. Keep task-specific evidence in `.task/current/` and completed task summaries in `.context/completed-tasks/`.

## Codex-Only Employee Workflow

Use the role files in this order unless the task is clearly narrower:

1. `.agents/roles/product-analyst.md`
2. `.agents/roles/salesforce-architect.md`
3. `.agents/roles/implementation-engineer.md`
4. `.agents/roles/test-engineer.md`
5. `.agents/roles/code-reviewer.md`
6. `.agents/roles/governance-reviewer.md`
7. `.agents/roles/release-engineer.md`

For each meaningful task, create or update:

```text
.task/current/intent.md
.task/current/requirements.md
.task/current/architecture.md
.task/current/implementation-plan.md
.task/current/test-plan.md
.task/current/review.md
.task/current/milestone-review.md
.task/current/release-checklist.md
```

Small, low-risk edits may use a compressed version of the workflow, but Codex must still know the acceptance criteria and validation command before editing.

## SDLC Enforcement

1. Plan before coding and state confidence as `HIGH`, `MEDIUM`, or `LOW`.
2. If confidence is low, inspect more project evidence or ask the user.
3. Complete milestone review checkpoints before crossing from requirements to architecture, architecture to implementation, implementation to validation, validation to release, or release to deploy.
4. Write or update tests before implementation when behavior changes.
5. Run the narrowest relevant verification first, then broader validation when the change risk requires it.
6. Self-review the exact diff before final response.
7. Commit every completed file-change task with a clear message after validation and review.
8. Do not push, deploy, or publish unless the user explicitly asks.

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
3. Tests or validation commands have been run, or the limitation is explicitly reported.
4. A review pass has checked metadata consistency, permissions, and deployment risk.
5. A governance review has checked guardrails, approval requirements, milestone status, and residual risk.
6. The completed file-change set is committed to Git.
7. Release notes include deploy command, target org assumptions, rollback path, and residual risk.
