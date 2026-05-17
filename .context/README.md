# File-Backed Context

This folder is the project memory system. It is intentionally Markdown-only and Git-backed. Codex reads it before planning and updates it after meaningful work.

## Folders

- `MEMORY.md`: short durable summary for future Codex sessions.
- `decisions/`: architecture and process decisions.
- `patterns/`: repeatable implementation and validation patterns.
- `completed-tasks/`: summaries of completed work.
- `salesforce-org-notes/`: org-specific notes that are safe to store.
- `knowledge-base/`: curated Salesforce and Agentforce guidance for Codex.
- `governance/`: governance, guardrails, approval, and milestone-review rules.
- `feedback/`: feedback capture, improvement log, and memory-update process.
- `retrieved-context.md`: optional scratch context assembled for the current task.
- `knowledge-base/future-scope.md`: known gaps and future hardening options.

## Rules

- Keep summaries short and source-oriented.
- Prefer links or file paths to long copied content.
- Never store secrets, access tokens, private keys, auth URLs, session IDs, or passwords.
- When a note may be stale, say so directly.
