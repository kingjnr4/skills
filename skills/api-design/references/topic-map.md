# Select the relevant Speakeasy pages

Read the articles linked for the current task, not every article. These routing notes are editorial; the articles retain Speakeasy's wording. Paths below are relative to this file. Consult [interpretation-notes.md](interpretation-notes.md) alongside the articles.

## Common task routes

| Task | Start with | Expand when relevant |
| --- | --- | --- |
| New resource or endpoint | URLs, HTTP methods, parameters, request body, responses, status codes, errors | Security; collections/pagination for lists; architecture when REST itself is undecided |
| Collection/list endpoint | Collections, pagination, filtering responses, parameters, responses | Caching, security, rate limiting, versioning for existing lists |
| Create/update/delete/action | HTTP methods, request body, status codes, errors | Security, caching/concurrency, file uploads, versioning for changed behavior |
| Existing contract change | Versioning plus the chapters for the changed surface | Consistency, documentation, testing, SDK/client expectations |
| Review a service | Applicable basics, errors, security, consistency, versioning, documentation, testing | Collection topics, caching, rate limiting and uploads as applicable; launch/billing/compliance only within scope |
| Public launch | Exposing APIs publicly, security, developer experience, documentation, testing | Rate limiting, caching, versioning, compliance and monetization if needed |

## API design basics

- [Picking an architecture](speakeasy/api-design/01-api-design-basics/picking-architectures.md): choosing among REST, RPC, GraphQL, and event/streaming approaches. Do not reopen an established architecture for a routine endpoint change.
- [URLs](speakeasy/api-design/01-api-design-basics/urls.md): resource names, relationships, nesting, and query strings.
- [HTTP methods](speakeasy/api-design/01-api-design-basics/http-methods.md): retrieval, creation/actions, replacement, partial updates, deletion, and concurrency.
- [Parameters](speakeasy/api-design/01-api-design-basics/parameters.md): path, query, header, and cookie parameter choices.
- [Data formats](speakeasy/api-design/01-api-design-basics/data-formats.md): JSON, XML, form and multipart tradeoffs.
- [Request body](speakeasy/api-design/01-api-design-basics/request-body.md): payload design, content types, and request/response consistency.
- [Status codes](speakeasy/api-design/01-api-design-basics/status-codes.md): success, redirection, client and server failures.
- [Responses](speakeasy/api-design/01-api-design-basics/responses.md): body structure, headers, data types, and error representations.

## Advanced considerations

- [File uploads](speakeasy/api-design/02-advanced-considerations/file-uploads.md): binary transfer, multipart and alternative upload designs.
- [Pagination](speakeasy/api-design/02-advanced-considerations/pagination.md): page, offset and cursor tradeoffs; navigation links and changing datasets.
- [Filtering responses](speakeasy/api-design/02-advanced-considerations/filtering-responses.md): collection filtering and response selection conventions.
- [Caching](speakeasy/api-design/02-advanced-considerations/caching.md): cache behavior, headers, validators, and conditional requests.
- [Errors](speakeasy/api-design/02-advanced-considerations/errors.md): useful machine and human information, Problem Details, and failure consistency.
- [Rate limiting](speakeasy/api-design/02-advanced-considerations/rate-limiting.md): limits, client communication, and strategy tradeoffs.
- [Versioning](speakeasy/api-design/02-advanced-considerations/versioning.md): compatibility, API evolution, versions, and consumer coordination.

## Productizing APIs

- [Collections](speakeasy/api-design/03-productizing-apis/collections.md): collection representations and operations. Read with pagination and filtering despite its upstream placement in this section.
- [Consistency](speakeasy/api-design/03-productizing-apis/consistency.md): shared conventions, style guides, automated checks, and governance.
- [Security](speakeasy/api-design/03-productizing-apis/security.md): authentication, authorization, and protecting API consumers and data.
- [Documentation](speakeasy/api-design/03-productizing-apis/documentation.md): OpenAPI, examples, reference documentation, and guides.
- [Testing](speakeasy/api-design/03-productizing-apis/testing.md): consumer-facing integration and contract checks, with additional testing concerns.
- [Developer experience](speakeasy/api-design/03-productizing-apis/developer-experience.md): usability across onboarding, tooling, and integration.
- [Exposing APIs publicly](speakeasy/api-design/03-productizing-apis/expose-api-publicly.md): launch readiness and operation of a public API.
- [Monetization](speakeasy/api-design/03-productizing-apis/monetization.md): entitlement, usage metering, and pricing flexibility. Read for billing scope, not every endpoint.
- [API compliance](speakeasy/api-design/03-productizing-apis/api-compliance.md): technical compliance concerns and responsibilities. Do not present a design review as legal certification; verify applicable current requirements when needed.

The [guide index](speakeasy/api-design/index.md) supplies the original reading order. This map also includes Collections, which is omitted from that index's listing.
