# Org2Agentforce Memory

This is the durable, Git-backed memory for the Salesforce Agentforce project. Keep it short and decision-oriented. Store detailed notes in the subfolders and link them from here when needed.

## Operating Model

- Codex is the execution manager.
- Employee agents are role instruction files under `.agents/roles/`.
- The repo uses file-backed context under `.context/`, not a vector database.
- The project knowledge base is curated Markdown under `.context/knowledge-base/`, not automated RAG.
- Governance and milestone-review rules live under `.context/governance/`.
- Git commit policy lives under `.context/governance/git-commit-policy.md`.
- Branching policy lives under `.context/governance/branching-policy.md`.
- Current task state lives under `.task/current/`.
- Do not store secrets, tokens, private keys, or live session details in memory files.

## Salesforce Project Context

- This is a Salesforce DX project named `Org2Agentforce`.
- Main source path is `force-app`.
- Salesforce API version is `66.0`.
- The sample Agentforce implementation is the `Local_Info_Agent` authoring bundle.
- Current metadata includes Agent Script, Apex classes/tests, a flow, prompt template, permission sets, and permission set groups.

## Validation Defaults

- Use `npm run prettier:verify` for local formatting checks.
- Use targeted Apex tests for Apex behavior changes.
- Use Salesforce deploy validation before live deploy when an org alias is available.
- Do not deploy, publish, or assign permissions unless the user explicitly asks.

## Knowledge Base Entry Points

- `.context/knowledge-base/salesforce-agentforce.md`
- `.context/knowledge-base/project-map.md`
- `.context/knowledge-base/development-workflow.md`
- `.context/knowledge-base/validation-and-release.md`
- `.context/knowledge-base/knowledge-update-policy.md`

## Governance Entry Points

- `.context/governance/governance.md`
- `.context/governance/guardrails.md`
- `.context/governance/milestone-review.md`
- `.context/governance/git-commit-policy.md`
- `.context/governance/branching-policy.md`

## Known Setup Notes

- This folder was not a Git repository when the Codex SDLC and employee-agent workflow were installed.
- `npm install` has been run so local Prettier dependencies are available.
- Full `npm run prettier:verify` currently reports formatting issues in pre-existing Salesforce template files. New SDLC and employee-agent files were verified separately.
