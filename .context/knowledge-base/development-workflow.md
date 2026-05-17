# Development Workflow

## Codex Execution Loop

For meaningful requirements, Codex should follow this file-based loop:

```text
Read .context/MEMORY.md
Read relevant .context/knowledge-base/*.md
Capture intent in .task/current/intent.md
Product Analyst writes requirements
Salesforce Architect writes architecture
Implementation Engineer writes implementation plan and changes files
Test Engineer writes validation evidence
Code Reviewer writes review findings
Governance Reviewer writes milestone and guardrail review
Release Engineer writes release checklist
Update .context when durable lessons were learned
```

## Role Order

Use the role files in this order unless the task is narrow enough to compress the workflow:

1. `.agents/roles/product-analyst.md`
2. `.agents/roles/salesforce-architect.md`
3. `.agents/roles/implementation-engineer.md`
4. `.agents/roles/test-engineer.md`
5. `.agents/roles/code-reviewer.md`
6. `.agents/roles/governance-reviewer.md`
7. `.agents/roles/release-engineer.md`

## Intent Handling

If intent is unclear, Codex should stop before implementation and write open questions in `.task/current/requirements.md`.

Common unclear Salesforce dimensions:

- Which agent or metadata component is in scope.
- Whether the change is local-only, deployable metadata, or live org behavior.
- Whether simulated preview or live mode should be affected.
- Whether Apex, Flow, Prompt Template, Agent Script, or permission metadata should change.
- Whether deployment, publishing, or permission assignment is expected.

## Scope Discipline

- Keep changes small and scoped.
- Do not modify unrelated Salesforce metadata.
- Do not deploy, publish, or assign permissions unless explicitly asked.
- Prefer source-file evidence and CLI output over assumptions.

## Milestone Gates

Before moving between phases, update `.task/current/milestone-review.md`:

- `M1 Requirements`: intent, scope, assumptions, acceptance criteria, risk.
- `M2 Architecture`: impacted metadata, dependencies, permissions, rollout, rollback.
- `M3 Implementation`: changed files, scope adherence, no unrelated metadata churn.
- `M4 Validation`: tests/checks run, failures, gaps, org validation state.
- `M5 Release`: deployment readiness, explicit approval status, rollback path.
