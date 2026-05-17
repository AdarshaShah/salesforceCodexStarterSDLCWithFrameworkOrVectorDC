# Guardrails

## Always Block Until Clarified

- unclear intent
- missing acceptance criteria
- unknown target Agentforce agent
- unknown target org for deployment
- ambiguous request to "make it live", "publish", "deploy", or "assign"

## Explicit Approval Required

- `sf project deploy start`
- Agentforce publish or activation
- permission set or permission set group assignment
- org default changes
- scratch org creation or deletion
- destructive metadata changes
- auth changes, connected app changes, named credential changes, or secret handling
- broad refactors across multiple metadata types
- direct implementation on `master` for a meaningful requirement

## Allowed Without Extra Approval

- reading source files
- writing task evidence under `.task/current/`
- updating `.context/` with non-secret project knowledge
- scoped local metadata edits after requirements and architecture are clear
- local formatting checks
- local static review
- Git commit after validation and review for completed file-change tasks
- creating a feature or requirement branch before scoped implementation

## Salesforce Safety Rules

- Do not put credentials, tokens, or session identifiers into prompts, files, commits, or memory.
- Do not assume org features, licenses, permission assignments, or live Agentforce status; verify when needed.
- Do not change runtime permissions without checking the relevant permission set or permission set group.
- Do not treat simulated preview as proof of live runtime behavior.
- Do not treat local metadata formatting as deploy validation.
- Do not commit generated secrets, local auth files, org session artifacts, or `node_modules`.
- Do not merge feature or requirement branches into `master` without explicit user approval.
