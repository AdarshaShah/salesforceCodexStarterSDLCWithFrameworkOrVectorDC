# Compliance Checklist

Use this checklist before closing any meaningful file-changing task.

## Required Checks

- Context read: `.context/MEMORY.md`
- Relevant knowledge base files read
- Governance files read
- Task branch created or branch exception documented
- Intent and requirements captured
- Acceptance criteria captured
- Architecture or implementation plan captured
- Test-first evidence captured for behavior changes, or exception documented
- Milestone review updated
- Changed files match approved scope
- Validation run, or limitation documented
- Code review completed
- Governance review completed
- Feedback status captured
- Memory update decision captured
- Secrets and local auth artifacts excluded
- Git commit created

## Salesforce-Specific Checks

- Agent Script references valid tools and metadata.
- Apex invocable signatures remain compatible.
- Flow and prompt template assumptions are documented.
- Permission impact is reviewed.
- Target org and deployment impact are documented when release is in scope.
- Simulated preview is not treated as live validation.

## Compliance Result

Use one result:

- `passed`
- `passed-with-documented-exceptions`
- `blocked`
