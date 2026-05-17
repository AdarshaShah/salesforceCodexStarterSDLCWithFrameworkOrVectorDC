# Org2Agentforce Codex Operating Contract

This repository is a Salesforce DX project for Agentforce development. Codex is the execution manager. Role files under `.agents/roles/` are the employee agents. Work proceeds through written task artifacts in `.task/current/` so requirements, decisions, tests, and review evidence remain inspectable.

## Core Rules

1. Use `gpt-5.5` with `xhigh` reasoning for this repo.
2. Keep Salesforce metadata changes scoped to `force-app/main/default` unless the task explicitly asks for project configuration.
3. Treat `sfdx-project.json`, `force-app/main/default/aiAuthoringBundles`, Apex classes, flows, prompt templates, permission sets, and package manifests as deployment-sensitive assets.
4. Do not modify auth state, org aliases, deployment targets, or scratch org config without stating the intended command and expected org impact first.
5. Do not deploy, assign permissions, publish agents, or run destructive metadata operations unless the user explicitly asks.
6. For Apex changes, prefer test-first or test-updated-first work. Run the narrowest relevant Apex test before broader validation.
7. For Agentforce authoring changes, keep Agent Script, tools, prompt templates, flows, Apex invocables, and permission metadata consistent.
8. Preserve existing Salesforce naming conventions and metadata folder structure.

## Codex-Only Employee Workflow

Use the role files in this order unless the task is clearly narrower:

1. `.agents/roles/product-analyst.md`
2. `.agents/roles/salesforce-architect.md`
3. `.agents/roles/implementation-engineer.md`
4. `.agents/roles/test-engineer.md`
5. `.agents/roles/code-reviewer.md`
6. `.agents/roles/release-engineer.md`

For each meaningful task, create or update:

```text
.task/current/intent.md
.task/current/requirements.md
.task/current/architecture.md
.task/current/implementation-plan.md
.task/current/test-plan.md
.task/current/review.md
.task/current/release-checklist.md
```

Small, low-risk edits may use a compressed version of the workflow, but Codex must still know the acceptance criteria and validation command before editing.

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
5. Release notes include deploy command, target org assumptions, rollback path, and residual risk.


# SDLC Enforcement

## Before Every Task
1. Plan before coding - outline steps, state confidence (HIGH/MEDIUM/LOW)
2. LOW confidence? Research more or ASK USER
3. Reasoning policy - use `gpt-5.5` with `xhigh` reasoning for this repo
4. Always keep this repo on `gpt-5.5` `xhigh`; do not switch wizard-repo work to `mixed`, mini-only, or lower-reasoning profiles
5. Keep this repo on `maximum` (`gpt-5.5` `xhigh` throughout) because codex-sdlc-wizard is unusually meta and high-blast-radius
6. If `GOALS.md` exists, treat it as the active-scope contract and keep `ROADMAP.md` as backlog/history
7. Write failing test FIRST (TDD RED), then implement (TDD GREEN)
8. ALL tests must pass before commit - no exceptions

## TDD Workflow (MANDATORY)
1. Write the test file FIRST - the test MUST FAIL initially
2. Run the test - confirm it fails (RED)
3. Write the minimum implementation to make the test pass
4. Run the test - confirm it passes (GREEN)
5. Only then: commit

## After Implementation
1. Self-review: read back your changes, check for bugs
2. Run full test suite - ALL tests must pass
3. Only then: commit and push

## Rules
- Delete legacy code - no backwards compatibility hacks
- Less is more - don't add what wasn't asked for
- Tests ARE code - treat test failures as bugs
- NEVER commit without running tests first
- During setup, environment repair, and auth-heavy workflows, prefer full access