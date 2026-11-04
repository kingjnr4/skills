---
name: api-design
description: Design or change REST/HTTP API contracts using Speakeasy's API Design Guide. Use for endpoint and resource design, request/response schemas, HTTP methods and status codes, pagination, errors, or API compatibility decisions, including when another skill needs these principles. Excludes consuming an existing API, internal function interfaces, and backend changes that do not affect an HTTP contract.
---

# API Design

Use the bundled Speakeasy guide to make concrete API decisions. Work within the requested surface; an endpoint change is not a reason to audit or redesign the whole application.

## Ground the contract

Identify the resource or action, consumer use case, and requested deliverable. In an existing project, inspect the relevant routes, schemas, serializers, authentication/authorization, tests, API documentation, and recorded design decisions. Use the artifacts that exist; OpenAPI is helpful but not a prerequisite.

Establish who consumes the API and whether their deployments can be coordinated. Treat unknown external consumers as a compatibility constraint. Distinguish the documented contract, observed implementation, and intended change; report discrepancies rather than assuming one proves the others.

## Read the relevant guidance

Read [interpretation-notes.md](references/interpretation-notes.md), then use [topic-map.md](references/topic-map.md) to select and read the relevant guide pages before making recommendations or edits. The map routes tasks; it does not replace the articles. Load only applicable topics, expanding when a decision crosses into another topic. A broad review should cover each applicable topic and disclose gaps.

The guide and its images are bundled under `references/speakeasy/`. Open an image when it contributes information needed for the decision that the surrounding prose does not convey. Do not open every illustration by default. Source provenance and snapshot limitations are in [source.md](references/source.md).

Follow Speakeasy's recommendations as the design baseline. Preserve their strength: an example is not a mandatory schema, and a preference is not an HTTP requirement. Honor explicit user choices and documented project constraints; explain material departures. When a guide claim conflicts with protocol semantics, use the cited standard and identify the discrepancy. Verify unresolved technical claims against primary sources when tools permit; otherwise mark the uncertainty.

## Shape and implement the requested surface

Start from how a consumer will use the API. Define the applicable parts of the contract together:

- Resource identity, relationships, paths, and operation semantics.
- Parameters and bodies: types, required fields, validation, defaults, omission versus null, and content types.
- Success status, headers, response shape, and empty results.
- Failure status and actionable, machine-readable error details.
- Collection bounds, pagination, filtering and ordering when collections are involved.
- Authentication, resource/property authorization, retries, caching, concurrency, and limits where relevant.

Use project terminology consistently. Choose among the guide's alternatives using the actual use case and data source; do not prescribe cursor pagination, an envelope, a versioning mechanism, or a new tool for every API. Check retry and concurrent-write behavior for mutations when relevant. Keep sensitive information out of examples and error responses.

For an existing contract, classify changes as behavior-preserving, additive, or potentially breaking. Include validation, defaults, nullability, ordering, status codes, headers, and SDK expectations in that assessment, not just path and field names. Do not silently replace a published contract to satisfy a style preference. Surface a conflicting requested change and offer a compatible evolution or scoped migration.

Update the requested implementation or specification and the affected examples/docs together. Use the project's existing contract source of truth; avoid introducing a second hand-maintained specification unless requested.

## Verify and hand back

Use available schema/style validation and focused behavior checks appropriate to the change. Check representative success and error cases, plus affected authorization, pagination, retries, or compatibility behavior. Prefer existing tooling; do not install a linter or generate an SDK merely to complete a small change. A clean schema lint does not prove the API behaves as documented.

Return the resulting contract or changes, consequential design choices with guide section references, and what was verified. Distinguish completed checks from proposed checks and note remaining assumptions. For review-only requests, return findings without modifying implementation. Repository-wide reviews and migrations belong to the explicitly requested workflow, not automatic scope expansion.
