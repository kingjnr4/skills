# Applying the guide accurately

These editorial notes clarify ambiguities in the Speakeasy guide. Use them alongside the relevant articles; they are not quotations from Speakeasy.

## HTTP methods and retries

The [HTTP methods chapter](speakeasy/api-design/01-api-design-basics/http-methods.md) sometimes describes idempotency as identical outputs. Idempotency concerns the intended server effect of repeated identical requests, not byte-identical responses. A second DELETE returning 404 after a successful deletion does not alone violate idempotency. See [RFC 9110 §9.2.2](https://www.rfc-editor.org/rfc/rfc9110.html#section-9.2.2).

PATCH is not guaranteed idempotent by the method, but a particular patch operation can be designed to be idempotent. Inspect the patch format and actual effect before recommending retries; do not turn the chapter's wording into a blanket prohibition on idempotent PATCH operations. See [RFC 5789 §2](https://www.rfc-editor.org/rfc/rfc5789.html#section-2).

The guide recommends PUT upserts and supporting both PUT and PATCH. Preserve those as recommendations. PUT's protocol semantics do not require every endpoint to permit creation, and a scoped partial-update requirement does not automatically require adding a replacement endpoint. See [RFC 9110 §9.3.4](https://www.rfc-editor.org/rfc/rfc9110.html#section-9.3.4).

## Authentication and errors

The [errors chapter](speakeasy/api-design/02-advanced-considerations/errors.md) mentions token refresh on 403. Do not infer a generic refresh/retry loop from that example. Distinguish missing/invalid credentials (401) from refusal of an understood request (403), and follow the actual authentication protocol. See [RFC 9110 §15.5.2–15.5.4](https://www.rfc-editor.org/rfc/rfc9110.html#section-15.5.2).

Speakeasy recommends RFC 9457 Problem Details. Its `type` identifies the problem type; a separate custom `code` property is not mandatory solely because earlier examples use one. If `status` is present in the body, it must match the HTTP response status. Preserve a supported existing error contract or plan its migration before replacing it. See [RFC 9457 §3.1](https://www.rfc-editor.org/rfc/rfc9457.html#section-3.1).

## Pagination and compatibility

The [pagination chapter](speakeasy/api-design/02-advanced-considerations/pagination.md) labels Web Linking as RFC 8299, while its link correctly targets [RFC 8288](https://www.rfc-editor.org/rfc/rfc8288.html). Use RFC 8288 for Link header semantics. Choose useful navigation relations for the actual strategy; the example's first/last/previous links are not universally available or required.

The [versioning chapter](speakeasy/api-design/02-advanced-considerations/versioning.md) describes additive changes as typically non-breaking. Check the actual consumer expectations: exhaustive enum handling, strict deserializers, defaults, and pagination assumptions can make an apparent addition disruptive. Treat this as compatibility analysis, not a reason to prohibit all additions.

## Recommendations versus requirements

Guide examples illustrate options rather than a universal contract template. Existing project decisions, constraints, and consumer impact matter when choosing naming conventions, envelopes, pagination, authentication, versioning, or tools. Identify deviations from Speakeasy explicitly; do not label every stylistic difference a functional defect.

If another questionable claim affects the task, verify it against the relevant primary specification or implementation and explain the discrepancy. Do not assume every example is production-ready code.
