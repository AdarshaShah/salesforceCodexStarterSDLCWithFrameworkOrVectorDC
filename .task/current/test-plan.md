# Test Plan

## Checks

- Run focused Prettier check on README, AGENTS, role, context, and task Markdown files.
- Confirm Git status is clean after commit.

## Results

- `npx prettier --check README.md AGENTS.md .agents/roles/*.md .context/**/*.md .task/current/*.md`: passed

## Salesforce Validation

Not required. This task does not change Salesforce runtime metadata.
