---
name: api-design
description: Design or change REST/HTTP API contracts. Use for resources and endpoints, request/response schemas, HTTP methods and status codes, pagination, errors, security, retries, or compatibility decisions. Excludes consuming an existing API, internal function interfaces, and backend changes that do not affect an HTTP contract.
---

# API Design

Design predictable HTTP contracts that consumers can use safely and that can evolve without surprises. Apply the guidance below within the requested surface; a small endpoint change is not a reason to redesign the application.

## Start with the consumer and existing contract

- Establish the use case, resource or action, and requested deliverable. Inspect relevant routes, schemas, middleware, tests, docs, and known consumers before recommending changes.
- Distinguish documented behavior, actual implementation, and intended changes. OpenAPI is useful, not a prerequisite; use the existing source of truth rather than introducing a second hand-maintained contract.
- Preserve established terminology and conventions unless changing them solves a concrete problem. These are design defaults, not universal requirements; explain material tradeoffs and follow HTTP standards when guidance conflicts.

## Core guidance

### Resources and URLs

- Prefer plural resource nouns (`/orders`, `/orders/{id}`), stable identifiers, and shallow nesting that reflects real ownership. Use query parameters for filtering, sorting, and pagination.
- Model actions that do not fit CRUD explicitly rather than disguising them as unrelated field updates. Do not reopen an established REST/RPC/GraphQL choice for a routine endpoint change.

### HTTP semantics

| Method | Intended use |
| --- | --- |
| GET | Read without requesting a state change; avoid request bodies. |
| POST | Create a resource or perform an action; retries are not inherently safe. |
| PUT | Replace the target's state; allow creation only if the contract supports it. |
| PATCH | Apply a documented partial-update format; define omission and null behavior. |
| DELETE | Remove the target; define repeated-delete and missing-resource responses. |

- Idempotency concerns the intended server effect, not identical responses. Repeated DELETE requests may return different statuses and still be idempotent. PATCH is not inherently idempotent, but a particular operation can be.
- Use meaningful statuses: `200` for success with a body, `201` for creation (include `Location` when appropriate), `202` for accepted but unfinished work with a way to track it, and `204` without a response body.
- Distinguish malformed requests (`400`), missing/invalid credentials (`401`, with an appropriate challenge), forbidden access (`403`), missing resources (`404`), conflicts (`409`), and semantic validation failures (`422`) using consistent project conventions. Do not turn every `403` into a token-refresh loop.

### Request and response schemas

- Define parameter locations, content types, types/formats, required fields, bounds, defaults, unknown-field handling, and omission versus null. Make input-writable and output-only fields explicit.
- Validate untrusted input at the API boundary. Use consistent field naming, timestamp/time-zone formats, enum conventions, and representations of identifiers and precise values such as money.
- Keep success shapes and empty-result behavior predictable. Choose an envelope only when it serves the contract; do not expose database models or internal implementation details by accident.

### Errors

- Return appropriate failure statuses and one consistent, machine-readable error structure with actionable human details. Do not hide failures inside `200` responses.
- Prefer RFC 9457 Problem Details for a new error contract (`application/problem+json`); preserve a supported existing format unless migration is in scope. Its `type` identifies the problem; an extra custom `code` is optional. If a body `status` is included, match the HTTP status.
- Include field-level validation details and a safe correlation identifier when useful. Never expose secrets, stack traces, or sensitive internals.

### Collections

- Bound potentially growing collections from the start: document default/maximum page size, stable ordering with a unique tie-breaker, filters, and invalid-parameter behavior.
- Choose page/offset pagination for straightforward navigation over suitable datasets; consider cursors for large or frequently changing datasets. Neither strategy automatically provides snapshot consistency; explain traversal behavior during writes.
- Return an empty collection for a successful query with no matches. Provide usable continuation links or tokens and explicit end-of-results behavior; do not require totals or first/last links when costly or unavailable.

### Security and operational behavior

- Require HTTPS. Keep credentials out of URLs, and redact sensitive data in logs, examples, and errors. Enforce operation-, resource-, and property-level authorization; possession of an ID is not permission.
- Allowlist writable fields and limit request/upload sizes and expensive queries. For URL imports or uploads, account for SSRF, content validation, and resource exhaustion when applicable.
- Define retry safety for mutations. If using idempotency keys, scope them to the caller and operation, bind them to the payload, claim atomically, handle in-flight duplicates and uncertain outcomes, and retain them through the supported retry window. A timeout does not prove the effect failed.
- Prevent lost updates where relevant, for example with ETag/If-Match preconditions. Choose cache directives and validators deliberately; prevent shared caches from leaking personalized data. Document rate limits and retry guidance (`429`, and `Retry-After` when appropriate).

### Compatibility and evolution

- Classify changes as behavior-preserving, additive, or potentially breaking. Check paths, types, required fields, nullability, validation, defaults, status/headers, errors, ordering, pagination, and SDK expectations.
- Additions are not automatically safe: strict deserializers and exhaustive enum handling can break. Determine whether consumers deploy together; treat unknown external consumers as a compatibility constraint.
- Prefer compatible extension over silently replacing a published contract. Use an established versioning strategy only when needed; do not impose a versioning mechanism on every API.
- For an authorized breaking change, define affected consumers, coexistence, migration, verification, rollback, and removal criteria. Do not invent deprecation dates or assume local caller updates prove external adoption.

## Small contract example

Illustrative only; adapt naming, pagination, and representation to the project.

```http
GET /orders?status=pending&limit=20

HTTP/1.1 200 OK
Content-Type: application/json

{"data":[{"id":"ord_123","status":"pending"}],"nextCursor":null}
```

Define allowed `status` values, `limit` bounds/default, ordering, and the next-page `cursor` parameter. Keep the same shape with `data: []` when empty; `nextCursor: null` means traversal is complete.

## Common pitfalls

- Cosmetic renames that break clients without improving behavior.
- Documenting retry safety without implementing deduplication or concurrency control.
- Assuming authentication alone provides resource authorization.
- Replacing a bare array with pagination metadata without assessing existing consumers.
- Treating a style preference or guide example as an HTTP requirement.

## Verify and deliver

- [ ] Inputs, success responses, errors, statuses, and headers form an explicit contract.
- [ ] Applicable authorization, collection bounds, retry, concurrency, and compatibility cases are covered.
- [ ] Implementation, contract source, examples, and docs agree; use existing tooling for focused tests and schema checks.
- [ ] Behavior was checked beyond schema lint, or unavailable checks are clearly disclosed.

Return the contract or changes, consequential tradeoffs, compatibility impact, and checks actually performed. Mark assumptions and unverified risks. For review-only requests, report evidenced findings and coverage limits without editing implementation.

## Further reference

[Speakeasy's REST API Design Guide](https://www.speakeasy.com/api-design) provides deeper explanations and alternatives. This skill is self-contained; consult relevant chapters only when useful, not as a prerequisite. For protocol questions, use primary standards such as [HTTP semantics (RFC 9110)](https://www.rfc-editor.org/rfc/rfc9110.html), [PATCH (RFC 5789)](https://www.rfc-editor.org/rfc/rfc5789.html), and [Problem Details (RFC 9457)](https://www.rfc-editor.org/rfc/rfc9457.html).
