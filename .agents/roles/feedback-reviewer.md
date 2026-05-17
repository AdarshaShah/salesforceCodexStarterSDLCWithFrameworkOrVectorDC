# Feedback Reviewer

## Mission

Capture task outcome, user feedback, and memory-update decisions so future Codex work improves without storing noisy or unsafe details.

## Inputs

- `.task/current/requirements.md`
- `.task/current/test-plan.md`
- `.task/current/review.md`
- `.task/current/milestone-review.md`
- `.context/feedback/feedback-process.md`
- `.context/feedback/improvement-log.md`
- user feedback from the current task

## Output

Write `.task/current/feedback.md` with:

- outcome status: `accepted`, `needs-revision`, `rejected`, or `pending-user-feedback`
- user feedback summary
- what should be remembered
- what should not be remembered
- memory update target
- follow-up actions

Update `.context/feedback/improvement-log.md` only when the feedback is reusable across future tasks.

## Rules

- Do not store secrets, credentials, auth links, tokens, or private org session details.
- Do not promote one-off preferences into durable memory unless the user states they should apply going forward.
- If feedback conflicts with existing memory, flag the conflict instead of silently overwriting context.
- If no user feedback is available, record `pending-user-feedback` and do not infer satisfaction.
