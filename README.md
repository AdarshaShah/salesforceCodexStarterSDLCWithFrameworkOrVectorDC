# Agentforce Project

This Salesforce DX project contains a sample agent called Local Info Agent that you could, for example, embed in a resort's web site. The agent provides local weather updates, shares information about local events, and helps guests with facility hours.

The agent demonstrates:

- Three types of subagents (Invocable Apex, Prompt Template, and Flow).
- Mutable variables.
- Flow control with `available when`.
- Deterministic branching with `if/else` in reasoning instructions.

## Codex Development Process

This project is set up for Codex-only, file-backed Agentforce development. Codex acts as the execution manager, while role files under `.agents/roles/` act as employee agents. The process does not use Agents SDK, LangGraph, vector DB, or external orchestration.

Use this command pattern when starting work in the project:

```powershell
cd C:\Users\adarsha_shah\Projects\Org2Agentforce
codex -m gpt-5.5 -c 'model_reasoning_effort="xhigh"'
```

For implementation work, invoke the repo-local SDLC skill:

```text
Use $sdlc.

Requirement:
<describe the Salesforce Agentforce requirement>

Acceptance criteria:
1. ...
2. ...
3. ...

Constraints:
- Do not deploy unless explicitly requested.
- Use the employee-agent workflow from AGENTS.md.
```

### Process Files

Core process files:

- `AGENTS.md`: top-level Codex operating contract.
- `.agents/roles/`: employee-agent role instructions.
- `.agents/skills/sdlc/SKILL.md`: repo-local SDLC skill.
- `.context/MEMORY.md`: durable file-backed memory.
- `.context/knowledge-base/`: curated Salesforce and Agentforce knowledge base.
- `.context/governance/`: governance, guardrails, branching, commit, compliance, and milestone rules.
- `.context/governance/test-first-policy.md`: required test-first and scenario-first gate.
- `.context/feedback/`: feedback capture and improvement loop.
- `.task/current/`: active task evidence and phase state.

### Execution Loop

Every meaningful requirement should follow this loop:

```text
Read .context/MEMORY.md
Read relevant .context/knowledge-base/*.md
Read governance and guardrail files
Create or confirm a task branch
Capture intent and requirements
Run Product Analyst role
Run Salesforce Architect role
Run Test Engineer role for test-first/scenario-first evidence
Run Implementation Engineer role
Run Test Engineer role
Run Code Reviewer role
Run Governance Reviewer role
Run Feedback Reviewer role
Run Release Engineer role when release is in scope
Complete compliance checklist
Commit the completed file-change task locally
```

### Employee Agents

The employee agents are role files, not independent background workers:

- `Product Analyst`: turns intent into requirements and acceptance criteria.
- `Salesforce Architect`: maps impacted metadata, dependencies, permissions, rollout, and rollback.
- `Implementation Engineer`: performs scoped source changes.
- `Test Engineer`: defines and runs validation.
- `Code Reviewer`: reviews diffs for defects and Salesforce metadata risk.
- `Governance Reviewer`: checks guardrails, approvals, milestone gates, and compliance.
- `Feedback Reviewer`: captures task outcome and memory-update decisions.
- `Release Engineer`: prepares deploy, rollback, and post-deploy verification when release is in scope.

### Task Evidence

Meaningful work should update these files under `.task/current/`:

- `intent.md`
- `requirements.md`
- `architecture.md`
- `implementation-plan.md`
- `test-plan.md`
- `review.md`
- `milestone-review.md`
- `feedback.md`
- `compliance-checklist.md`
- `release-checklist.md`

### Branching Policy

Meaningful requirements must use a branch before implementation:

```text
feature/<short-requirement>
requirement/<short-requirement>
fix/<short-bug>
docs/<short-doc-task>
chore/<short-maintenance-task>
```

`master` is treated as the protected base branch. Do not merge to `master` unless explicitly requested.

### Commit Policy

Every completed file-change task must be committed locally after validation and review. Do not leave completed work uncommitted.

Codex may commit locally. Codex must not push, merge, deploy, publish, assign permissions, or change org state unless explicitly requested.

### Governance And Guardrails

Governance rules live under `.context/governance/`.

Key guardrails:

- unclear intent blocks implementation
- missing acceptance criteria blocks implementation
- deployment, publishing, permission assignment, destructive metadata, auth changes, and org default changes require explicit approval
- Salesforce sign-in, MFA, licenses, tenant consent, and admin portal decisions remain user-owned
- secrets, tokens, auth artifacts, and `node_modules` must not be committed
- simulated preview is not proof of live Agentforce behavior

### Milestone Review

Milestones are tracked in `.task/current/milestone-review.md`:

- `M1 Requirements`: intent, scope, acceptance criteria, assumptions, risk, branch
- `M2 Architecture`: impacted metadata, dependencies, permissions, deployment impact, rollback, test-first strategy
- `M3 Implementation`: scoped changes, branch confirmation, metadata consistency, test-first gate satisfied
- `M4 Validation`: formatting, tests, deploy validation or documented gaps, final proof
- `M5 Release`: approval, target org, rollback, post-deploy verification, residual risk

### Compliance Checklist

Before final closeout, Codex should complete `.task/current/compliance-checklist.md`.

Required checks include:

- context and knowledge files read
- governance files read
- branch policy followed
- requirements and acceptance criteria captured
- test-first evidence captured before behavior changes, or exception documented
- milestone review updated
- validation run or limitation documented
- code review and governance review complete
- feedback and memory decision recorded
- secrets and local auth artifacts excluded
- local Git commit created

### Feedback And Memory

Feedback is captured in `.task/current/feedback.md`.

Durable feedback and lessons are stored in:

- `.context/feedback/user-feedback.md`
- `.context/feedback/improvement-log.md`
- `.context/MEMORY.md`

Only reusable, verified lessons should be promoted to durable memory. One-off feedback stays in task evidence unless the user says it should apply going forward.

### Validation Defaults

For behavior-changing work, follow the red-green-prove loop before implementation:

```text
Write or update the narrowest test or scenario
Run it first when technically possible
Record the failing result, gap, or exception
Implement the minimum scoped change
Re-run the same proof
Run broader validation when risk requires it
```

Use local formatting checks for documentation and metadata:

```powershell
npm run prettier:verify
```

For Apex changes, use targeted tests first:

```powershell
sf apex run test --target-org <alias> --tests <TestClassName> --wait 30 --result-format human
```

For deploy validation:

```powershell
sf project deploy validate --source-dir force-app --target-org <alias> --test-level RunLocalTests
```

If no org alias or auth is available, Codex must report that live validation is limited and provide the exact command to run after auth.

### Current Limitations And Future Scope

These are documented in `.context/knowledge-base/future-scope.md`.

Not implemented today:

- vector database
- embeddings-based RAG
- automatic semantic retrieval
- true parallel subagents
- external orchestration
- CI-enforced branch protection
- server-side required checks
- automatic Salesforce org capability detector
- automated Agentforce preview evidence capture
- automated secret scanning before commit
- automated pull request templates and approval workflow

The current setup is intentionally file-backed and Git-backed. It is strong for disciplined Codex execution, but future enterprise hardening should add CI checks, branch protection, semantic retrieval, and automated Salesforce validation gates when needed.

## Prerequisites

- **Salesforce Developer Edition (DE)** org. Get a free one at [developer.salesforce.com/signup](https://developer.salesforce.com/signup).
- **Salesforce CLI** (`sf`). Download and install it from [developer.salesforce.com/tools/sfdxcli](https://developer.salesforce.com/tools/sfdxcli). See the [Salesforce CLI Setup Guide](https://developer.salesforce.com/docs/atlas.en-us.sfdx_setup.meta/sfdx_setup/sfdx_setup_install_cli.htm) for more detailed information.
- **VS Code** with the **Salesforce Extensions** pack and the **Agentforce DX** extension. See [Install Pro-Code Tools](https://developer.salesforce.com/docs/ai/agentforce/guide/agent-dx-set-up-env.html) for details.

After you get a DE org and set up your tools, authorize the org so you can start working with it. Open VS Code and use the **SFDX: Authorize an Org** VS Code command from the Command Palette, or run this CLI command in VS Code's integrated terminal:

```bash
sf org login web --alias my-de-org --set-default
```

Log in to the browser that opens using your DE credentials.

## Configure Your Salesforce DX Project

Your new Salesforce DX project is ready to use.

But you can further configure it by editing the `sfdx-project.json` file. See [Salesforce DX Project Configuration](https://developer.salesforce.com/docs/atlas.en-us.sfdx_dev.meta/sfdx_dev/sfdx_dev_ws_config.htm) in the _Salesforce DX Developer Guide_ for details about this file.

## Enable Skills in Agentforce Vibes to Vibe Code Agents

To vibe code agents using Agentforce Vibes, first open the Agentforce Vibes panel. Click the **Manage Agentforce Rules, Workflows, Hooks & Skills** icon, then the **Skills** tab, and ensure the `agentforce-development` skill is enabled. That's it!

### Use Other AI Tools

If you prefer to use other AI tools, such as Claude Code or Cursor, copy the [`agentforce-development` skills](https://github.com/forcedotcom/afv-library/tree/main/skills/agentforce-development) from the `afv-library` GitHub repository to the appropriate directory in this DX project. Check your AI tool's documentation for the specific location and how to enable the skills.

## Vibe Code the Sample Agent

Salesforce agents use an Agent Script file as their blueprint. To vibe code an agent, you vibe code its Agent Script file. Agent Script files are part of the `AiAuthoringBundle` metadata type.

Let's see how this works by vibe coding the Agent Script file associated with the sample Local Info Agent. Open up the `force-app/main/default/aiAuthoringBundle/Local_Info_Agent/Local_Info_Agent.agent` file in VS Code, then enter your prompts in the Agentforce Vibes chat box. For example, to learn more about how the agent is coded, ask questions like:

- _What does the Local Info Agent do?_
- _What Apex classes does this agent use?_
- _Does the agent use flows?_

As you get more familiar with vibe coding a Salesforce agent, you can start making actual changes to the Agent Script file.

## Preview the Agent in Simulated Mode

You can preview how the agent works right in VS Code using the Agentforce DX panel. For now you must preview in _simulated mode_, because you haven't yet deployed the Apex classes, flow, or prompt template to your org. After you deploy, you can use _live mode_ in which the agent uses the actual Apex classes, etc. In simulated mode, the Local Info Agent mocks the answers to your questions.

To preview in simulated mode, right-click the `Local_Info_Agent.agent` file and choose **AFDX: Preview This Agent**. In the Agentforce DX panel that opens, click **Start Simulation**. Then enter a question in the chat box at the bottom, such as `What's the weather like?`. The agent simulates an answer.

## Agentforce-Ready Scratch Orgs

This template includes a scratch org configuration file (`config/project-scratch-def.json`) that contains the required settings and features for creating an Agentforce-ready scratch org.

Here's an example of creating a scratch org using the file; it assumes you've already authorized the Dev Hub org with alias `DevHub`:

```bash
sf org create scratch --definition-file config/project-scratch-def.json --alias AgentScratchOrg --set-default --target-dev-hub DevHub
```

## What's Inside This DX Project?

These are the interesting metadata components associated with the Local Info Agent. All the component source files are in the `force-app/main/default` package directory under their associated metadata directory, such as `classes` for Apex classes.

| Component                | Type                 | Purpose                                                                 |
| ------------------------ | -------------------- | ----------------------------------------------------------------------- |
| `Local_Info_Agent.agent` | Agent Script         | The agent definition — tools, reasoning, variables, and flow control.   |
| `CheckWeather`           | Apex Class           | Invocable Apex. Checks current weather conditions for a given location. |
| `CurrentDate`            | Apex Class           | Invocable Apex. Returns the current date for use by the agent.          |
| `WeatherService`         | Apex Class           | Provides mock weather data for the resort.                              |
| `Get_Event_Info`         | Prompt Template      | Retrieves local events.                                                 |
| `Get_Resort_Hours`       | Flow                 | Returns facility hours and reservation requirements.                    |
| `Resort_Agent`           | Permission Set       | Agent user permissions (Einstein Agent license).                        |
| `Resort_Admin`           | Permission Set       | Admin/developer Apex class access.                                      |
| `AFDX_Agent_Perms`       | Permission Set Group | Bundles agent user permissions for assignment.                          |
| `AFDX_User_Perms`        | Permission Set Group | Bundles admin user permissions for assignment.                          |

## Next Steps

This README provides just a taste of working with Salesforce agents. Check out the [_Agentforce DX Developer Guide_](https://developer.salesforce.com/docs/einstein/genai/guide/agent-dx.html) which shows you how to:

- Author an agent, which involves generating an authoring bundle, coding the Agent Script file, and publishing the agent to your org.
- Preview and debug an agent.
- Test an agent.

## Read All About It

- [_Agentforce DX Developer Guide_](https://developer.salesforce.com/docs/einstein/genai/guide/agent-dx.html)
- [_Agent Script_](https://developer.salesforce.com/docs/ai/agentforce/guide/agent-script.html)
- [_Agentforce Vibes Extension_](https://developer.salesforce.com/docs/platform/einstein-for-devs/guide/einstein-overview.html)

- [_Salesforce Extensions for VS Code_](https://developer.salesforce.com/docs/platform/sfvscode-extensions/guide)
- [_Salesforce CLI Setup Guide_](https://developer.salesforce.com/docs/atlas.en-us.sfdx_setup.meta/sfdx_setup/sfdx_setup_intro.htm)
- [_Salesforce DX Developer Guide_](https://developer.salesforce.com/docs/atlas.en-us.sfdx_dev.meta/sfdx_dev/sfdx_dev_intro.htm)
- [_Salesforce CLI Command Reference_](https://developer.salesforce.com/docs/atlas.en-us.sfdx_cli_reference.meta/sfdx_cli_reference/cli_reference.htm)
