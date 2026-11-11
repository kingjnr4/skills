# Evolving an existing API

Use the shared `api-design` skill's compatibility and evolution guidance alongside this workflow. These notes expand that guidance into a migration checklist.

## Capture the baseline

Record representative old requests and their observable results: response bodies/status/headers, validation failures, authorization behavior, pagination, defaults, and retry/concurrency behavior where relevant. Use existing tests and contract artifacts; add focused characterization tests when behavior is otherwise unprotected.

Identify known clients, supported SDKs, deployment independence, and any published deprecation commitments. Treat unknown consumers as unknown, not absent. A frontend in the same repository may still be deployed independently or cached in browsers.

## Classify each proposed change

| Class | Examples | Evidence needed |
| --- | --- | --- |
| Behavior-preserving | Move validation without changing accepted inputs or errors; deduplicate serialization without changing output | Existing consumer-visible behavior remains the same |
| Additive, subject to client expectations | New endpoint, optional parameter with unchanged default, extra response property | Existing requests retain semantics; consumers tolerate the addition |
| Potentially breaking | Rename/remove path or field; narrow validation; change type/nullability/default/order/status; add required input; replace an array with a pagination envelope | Explicit consumer impact assessment and a migration strategy within the authorized scope |

Enum additions and newly emitted error variants can break exhaustive clients even though a schema diff looks additive. Validate the actual client assumptions rather than labeling every addition safe.

## Select the transition

- If every consumer can migrate together, update callers and server coherently and test the deployment assumptions. Do not create a permanent legacy layer without a need.
- If consumers cannot migrate together, consider retaining the old representation/endpoint, adding a compatible operation, or using the project's established versioning strategy. Choose the smallest transition that serves the requirement.
- Define what proves the transition is complete before deleting a supported contract. Repository caller migration alone does not prove external adoption.

For a needed migration, record old → new behavior, affected consumers, coexistence strategy, verification, rollback path, and any removal criteria. Timelines and deprecation announcements require actual project decisions; do not invent dates or publish notices.

## Prove and report

Check the preserved contract as well as the new behavior. Where versions coexist, test both and verify isolation of their semantics. Distinguish implemented local changes from proposed deployment, data migration, client adoption, and eventual removal. Keep unfinished external actions explicit.
