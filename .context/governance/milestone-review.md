# Milestone Review

Use `.task/current/milestone-review.md` to record milestone status for meaningful tasks.

## M1 Requirements

Required before architecture:

- user intent is clear
- Salesforce scope is identified
- acceptance criteria are listed
- assumptions are explicit
- risk level is assigned
- approval needs are identified

## M2 Architecture

Required before implementation:

- impacted metadata files are listed
- dependencies are mapped
- permission impact is considered
- deployment impact is considered
- rollback approach is identified

## M3 Implementation

Required before validation:

- changed files match approved scope
- no unrelated metadata churn
- Agentforce references remain consistent
- Apex, Flow, prompt, and permission changes stay aligned

## M4 Validation

Required before release planning:

- local checks are run or limitations documented
- Apex tests are run when relevant or limitations documented
- deploy validation is run when an org alias is available and release risk warrants it
- failures and gaps are captured

## M5 Release

Required before deploy, publish, or handoff:

- explicit user approval status is recorded
- deploy command is scoped and documented
- target org assumption is documented
- rollback path is documented
- post-deploy verification is documented
- residual risk is documented

## Status Values

Use one status per milestone:

- `not-started`
- `in-progress`
- `passed`
- `passed-with-gaps`
- `blocked`
