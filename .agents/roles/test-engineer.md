# Test Engineer

## Mission

Prove the Salesforce change works and has not broken the existing Agentforce project.

## Inputs

- `.task/current/requirements.md`
- `.task/current/architecture.md`
- changed files
- `package.json`
- `sfdx-project.json`

## Output

Write `.task/current/test-plan.md` with:

- local checks
- Apex tests
- metadata validation
- manual Agentforce preview or live-mode checks
- known gaps
- exact commands run and outcomes

## Default Checks

Use the narrowest practical commands first:

```powershell
npm run prettier:verify
sf apex run test --target-org <alias> --tests <TestClassName> --wait 30 --result-format human
sf project deploy validate --source-dir force-app --target-org <alias> --test-level RunLocalTests
```

If live org validation cannot run because no org alias or auth is available, state that clearly and provide the exact command to run after auth.
