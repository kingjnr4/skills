---
name: refactor-api
description: Improve an existing HTTP API using Speakeasy guidance, with scoped implementation, compatibility checks, and migration planning when contracts change.
disable-model-invocation: true
---

# Refactor API

Improve the requested API surface through a concrete, verified change. An internal refactor preserves the external contract; a redesign may require a contract migration. Establish which work the user requested before treating a breaking change as authorized.

## Load the shared discipline

Invoke the model-invoked `api-design` skill using the host's skill mechanism (the Skill tool where available). If there is no invocation tool, read its `SKILL.md` using the path in the host's available-skills listing. Load its interpretation notes and applicable source pages. This skill depends on `api-design`; if it is unavailable, report the missing dependency. Do not invoke the user-only `review-api` skill; perform the scoped assessment here.

## Ground the change

Identify the target problem, current HTTP contract, desired consumer experience, and completion criteria from the request and repository. Read affected routes, schemas, shared middleware, tests, docs, and known consumers. Preserve existing work and unrelated conventions. If the request is broad, prioritize a coherent surface whose improvement has observable value rather than sweeping cosmetic renames.

Load the relevant Speakeasy pages using the shared topic map. Establish whether consumers deploy together, independently within the organization, or externally. Do not assume repository searches enumerate every consumer.

## Choose a compatible path

Read [migration.md](references/migration.md) before changing an existing contract. Compare current and proposed behavior, including paths, types, nullability, required fields, validation, defaults, status codes, errors, headers, ordering, and collection traversal.

For behavior-preserving restructuring, keep the contract and verify it through the same consumer-facing tests. For additive changes, verify assumptions about existing clients and SDKs. For potentially breaking changes, prefer compatible evolution unless the request authorizes a migration. If the user's objective requires an unresolved product decision about breaking clients, finish the impact assessment and concrete options before asking for that decision; continue independent work in the meantime.

Explain material tradeoffs concisely. Do not require a plan approval for ordinary, authorized edits, and do not interpret permission to refactor as permission to remove a published endpoint or migrate production data.

## Implement and verify

Update the contract's source of truth, implementation, tests, and affected examples/docs together. Use the existing framework and validation tools. Keep changes small enough that each unit has an observable completion condition. Avoid adding compatibility machinery for consumers that can demonstrably migrate together; retain compatibility for consumers that cannot.

Run focused checks of old and new behavior where they coexist, including affected failures and authorization. Exercise pagination or retry behavior if changed. Compare specifications when available, but verify behavior beyond schema syntax. Record unavailable runtime or client checks as limitations rather than passing them implicitly.

Deliver the implemented change, compatibility classification, relevant guide sections, checks performed, and any remaining migration or rollout work. A locally verified implementation is not evidence that external clients migrated. Do not deploy, announce deprecations, or delete old contracts as incidental cleanup.
