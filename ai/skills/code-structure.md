# Skill: Code Structure

Separate domain orchestration from reusable operational mechanics using a service layer.

Actions own the "why/when": business rules, auth, ownership checks, state transitions, failure classification, retries, and user-facing errors.

Services own the "how": reusable operations, provider/SDK calls, command execution details, health checks, readiness checks, and structured operational results.

## When to use

- Multiple workflows duplicate the same operational logic.
- Multiple callers need the same low-level operation.
- A feature shares mechanics with existing flows.
- A bug fix in one workflow should also affect other workflows doing the same operation.
- Action files are copy-pasting sandbox, email, payment, build, runtime, integration, or provider logic.
- Refactoring repeated operational blocks across domain flows.

## When not to use

- The logic is truly domain-specific and used by only one caller.
- The extraction would create abstraction without demonstrated repetition or friction.
- The current task is an unrelated feature implementation.
- The proposed service would hide domain policy, state transitions, or authorization.

## Core rule

Keep product meaning in actions. Move repeatable mechanics to services.

- "What this product flow means" stays in actions.
- "How to do this operation reliably" moves to a service layer.

## Procedure

1. Read the story, impact analysis, project map, relevant action files, and existing service/module conventions.
2. Identify repeated operational chunks across two or more callers.
3. Classify each chunk as domain orchestration or reusable mechanics.
4. Extract only repeated, non-domain mechanics.
5. Design service functions as composable capability blocks, not one large operation.
6. Require explicit parameters and structured return values.
7. Keep database mutations, auth decisions, ownership checks, status transitions, and user-facing failure classification in actions unless an existing architecture explicitly says otherwise.
8. Replace one caller first.
9. Verify behavior and tests.
10. Replace remaining callers only after the first migration is stable.

## Service design rules

Good service functions:

```ts
createManagedSandbox(...)
prepareRepo(...)
detectPackageManager(...)
installDependencies(...)
runBuildCommand(...)
startSandboxRuntime(...)
```

Each service function must:

- accept required data as explicit parameters;
- return structured outputs;
- make failure explicit;
- avoid hidden global state;
- avoid reaching into domain database/state directly;
- avoid swallowing errors;
- allow callers to choose strict or relaxed behavior per product flow.

## Anti-patterns

- God service: one huge method hides all control flow.
- Leaky service: service mutates domain tables or product state directly.
- Inconsistent API: every function uses different argument and error semantics.
- Over-abstraction: extracting logic used by only one caller.
- Policy leakage: service decides auth, ownership, product status, or user-facing classification.

## Output format

```markdown
# Code Structure Recommendation

## Current duplication or friction

## Domain orchestration to keep in actions

## Operational mechanics to extract

## Proposed service functions

## Inputs and structured outputs

## First caller to migrate

## Verification plan

## Risks and stop conditions
```

## Stop conditions

Stop or escalate when:

- behavior preservation cannot be verified;
- the extraction changes product behavior;
- service boundaries would own auth, billing, permissions, destructive data changes, or secrets without approval;
- the proposed refactor exceeds one safe story;
- the service API would become a monolith.
