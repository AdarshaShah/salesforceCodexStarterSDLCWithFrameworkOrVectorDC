# Compliance Checklist

## Required Checks

- Context read: passed
- Relevant knowledge base files read: passed
- Governance files read: passed
- Task branch created or branch exception documented: passed
- Intent and requirements captured: passed
- Acceptance criteria captured: passed
- Architecture or implementation plan captured: passed
- Test-first evidence captured for behavior changes, or exception documented: passed-with-exception
- Milestone review updated: passed
- Changed files match approved scope: passed
- Validation run, or limitation documented: passed
- Code review completed: passed
- Governance review completed: passed
- Feedback status captured: passed
- Memory update decision captured: passed
- Secrets and local auth artifacts excluded: passed
- Git commit created: pending

## Salesforce-Specific Checks

- Agent Script references valid tools and metadata: not applicable
- Apex invocable signatures remain compatible: not applicable
- Flow and prompt template assumptions are documented: not applicable
- Permission impact is reviewed: not applicable
- Target org and deployment impact are documented when release is in scope: not applicable
- Simulated preview is not treated as live validation: passed

## Compliance Result

Status: `passed-with-documented-exceptions`

Exception:

Reason: test-first behavior proof and Salesforce deploy validation are not required because this task changes process documentation only.

Risk: low

User approval: user requested TDD/process hardening.

Follow-up: apply `.context/governance/test-first-policy.md` to the next behavior-changing requirement.
