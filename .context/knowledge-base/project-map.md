# Project Map

## Repository Type

Salesforce DX project.

## Key Files

- `sfdx-project.json`: Salesforce project configuration.
- `package.json`: local formatting scripts and Node dev dependencies.
- `README.md`: Salesforce Agentforce sample project guidance.
- `manifest/package.xml`: package manifest.
- `config/project-scratch-def.json`: scratch org shape for Agentforce-ready orgs.
- `AGENTS.md`: Codex operating contract.
- `.agents/roles/`: Codex employee-role instructions.
- `.agents/skills/sdlc/SKILL.md`: Codex SDLC workflow skill.
- `.context/`: file-backed memory and knowledge base.
- `.task/current/`: active task state.

## Main Salesforce Source

Source root:

```text
force-app/main/default
```

Current notable metadata areas:

- `aiAuthoringBundles/Local_Info_Agent/`
- `classes/`
- `flows/`
- `genAiPromptTemplates/`
- `permissionsets/`
- `permissionsetgroups/`

## Current Sample Components

- `Local_Info_Agent.agent`: sample Agent Script.
- `CheckWeather`: Apex invocable weather action.
- `CurrentDate`: Apex invocable current date action.
- `WeatherService`: mock weather service.
- `Get_Event_Info`: prompt template for local events.
- `Get_Resort_Hours`: flow for facility hours.
- `Resort_Agent`: runtime agent-user permissions.
- `Resort_Admin`: admin/developer permissions.
- `AFDX_Agent_Perms`: agent permission set group.
- `AFDX_User_Perms`: admin/user permission set group.
