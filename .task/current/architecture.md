# Architecture

## Scope

Process and documentation files only.

## Impacted Areas

- `README.md`
- `AGENTS.md`
- `.agents/roles/test-engineer.md`
- `.context/MEMORY.md`
- `.context/governance/`
- `.context/knowledge-base/`
- `.task/current/`

## Test-First Strategy

This task changes process documentation only, so classic red-green behavior testing does not apply. The policy itself adds the required red-green-prove loop for future behavior-changing work.

## Deployment Impact

None. No Salesforce runtime metadata changes.

## Rollback

Revert the documentation/process commit if the policy needs to be changed.
