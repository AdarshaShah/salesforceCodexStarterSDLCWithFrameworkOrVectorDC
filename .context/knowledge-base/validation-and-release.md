# Validation And Release

## Local Validation

Use local formatting checks after touching Markdown, JSON, XML, Apex, or Salesforce metadata:

```powershell
npm run prettier:verify
```

If the full formatting check fails because of unrelated pre-existing files, run a focused check on changed files and report the broader pre-existing failure.

## Apex Validation

For Apex behavior changes, prefer targeted tests first:

```powershell
sf apex run test --target-org <alias> --tests <TestClassName> --wait 30 --result-format human
```

Use broader local tests when risk or dependency surface increases:

```powershell
sf apex run test --target-org <alias> --test-level RunLocalTests --wait 30 --result-format human
```

## Metadata Validation

Before live deploy, prefer validation-only deploy:

```powershell
sf project deploy validate --source-dir force-app --target-org <alias> --test-level RunLocalTests
```

For narrow changes, scope the source directory when possible:

```powershell
sf project deploy validate --source-dir force-app/main/default/classes --target-org <alias> --test-level RunLocalTests
```

## Deployment

Deploy only when the user explicitly asks:

```powershell
sf project deploy start --source-dir force-app --target-org <alias> --test-level RunLocalTests --wait 60
```

## Release Checklist

Before release, record:

- target org alias
- deploy command
- test level
- pre-deploy checks
- post-deploy verification
- Agentforce preview or publish steps
- rollback or restore path
- residual risks

## Auth Boundary

Salesforce sign-in, MFA, license assignment, and tenant/admin consent remain user-owned. Codex owns command shape, scope, and verification after the user completes the auth step.
