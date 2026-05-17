# Implementation Plan

## Files To Change

- `AGENTS.md`
- `.agents/roles/governance-reviewer.md`
- `.context/MEMORY.md`
- `.context/README.md`
- `.context/governance/*`
- `.context/knowledge-base/development-workflow.md`
- `.context/knowledge-base/future-scope.md`
- `.task/current/*`
- `README.md`

## Files To Avoid

- `force-app/main/default/**`
- Salesforce org auth/config files
- deployment metadata unrelated to process documentation

## Validation

```powershell
npx prettier --check README.md AGENTS.md .agents/roles/*.md .context/**/*.md .task/current/*.md
```
