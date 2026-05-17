# Test-First Policy

## Purpose

Behavior-changing work must start with test or scenario evidence before implementation. This keeps Codex execution requirement-driven and prevents code changes from defining their own success criteria.

## Required Gate

Before changing runtime behavior, Codex must record one of these in `.task/current/test-plan.md`:

- a new or updated Apex test
- a new or updated LWC/Jest test when the project has a relevant test harness
- a Flow, prompt, or Agentforce scenario with inputs, expected output, and safety constraints
- a documented exception explaining why test-first is not possible

Implementation must not begin until this gate is satisfied.

## Red-Green-Prove Loop

Use this loop for behavior-changing work:

1. Write or update the narrowest useful test or scenario.
2. Run it before implementation when technically possible.
3. Record the failing or gap result in `.task/current/test-plan.md`.
4. Implement the minimum scoped change.
5. Re-run the narrow test or scenario until it passes.
6. Run broader validation when the risk or dependency surface requires it.
7. Record final proof and remaining gaps before review.

## Salesforce Application

Use the strongest available proof for the changed surface:

- Apex: Apex test method or updated test class.
- Invocable Apex: Apex test covering the invocable contract and bulk behavior.
- LWC: Jest test when available, otherwise documented manual scenario plus local static checks.
- Flow: Flow test metadata when available, otherwise Apex coverage or scenario evidence.
- Prompt template: scenario with required inputs, expected response shape, grounding, and safety checks.
- Agentforce Agent Script: scenario with user utterance, expected tool use, expected response, disallowed behavior, and permission assumptions.
- Permission metadata: review and deploy validation; classic red-green testing may not apply.

## Allowed Exceptions

Test-first may be skipped only when the exception is documented with:

```text
Exception:
Reason:
Risk:
Alternative proof:
Follow-up:
```

Common valid exceptions:

- docs-only or process-only change
- no behavior changed
- no local or org test harness exists for the changed surface
- first baseline scaffold where no executable target exists yet
- live org validation is blocked by missing user-owned auth or license setup

## Not Allowed

- implementing behavior first and writing acceptance criteria afterward
- claiming prompt or Agentforce behavior is validated without scenario evidence
- skipping Apex tests for Apex behavior changes when an authenticated org and relevant tests are available
- treating formatting as behavior validation
