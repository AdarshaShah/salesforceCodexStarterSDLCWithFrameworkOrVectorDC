# Salesforce Agentforce Knowledge

## Project Concepts

This project is a Salesforce DX Agentforce project. The sample agent is `Local_Info_Agent`.

Agentforce source in this repo can include:

- Agent Script and bundle metadata under `force-app/main/default/aiAuthoringBundles/`.
- Planner metadata under `force-app/main/default/genAiPlannerBundles/` when present.
- Prompt templates under `force-app/main/default/genAiPromptTemplates/`.
- Apex invocable tools under `force-app/main/default/classes/`.
- Flows under `force-app/main/default/flows/`.
- Permission sets and permission set groups under `force-app/main/default/permissionsets/` and `force-app/main/default/permissionsetgroups/`.

## Design Rules

- Keep Agent Script tool references aligned with Apex, flows, prompt templates, and permissions.
- Treat Agentforce authoring metadata as deployment-sensitive.
- Prefer explicit acceptance criteria before changing agent reasoning instructions.
- For prompt template changes, verify the expected input variables and consuming agent/tool behavior.
- For Apex invocable actions, preserve invocable method signatures unless the dependent agent metadata is updated in the same task.
- For flow-backed tools, confirm flow API names and input/output assumptions.
- For permission changes, account for both admin/developer access and runtime agent-user access.

## Preview And Runtime Notes

- Simulated preview can validate conversation shape without relying on deployed Apex, flows, or prompt templates.
- Live mode depends on deployed metadata and org configuration.
- Publishing or deploying an agent can affect live org behavior, so it requires explicit user approval.
