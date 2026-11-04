---
name: review-api
description: Review an existing HTTP API or proposed contract change against Speakeasy guidance, with evidenced findings and compatibility implications.
disable-model-invocation: true
---

# Review API

Assess the requested API surface and return actionable findings. Keep the review read-only unless the user also requested fixes; writing a requested review artifact is allowed.

## Load the shared discipline

Invoke the model-invoked `api-design` skill using the host's skill mechanism (the Skill tool where available). If there is no invocation tool, read its `SKILL.md` using the path in the host's available-skills listing. Load its interpretation notes and applicable source pages. This skill depends on `api-design`; if it is unavailable, report the missing dependency rather than presenting a generic review as Speakeasy-based. Do not invoke the user-only `refactor-api` skill.

## Establish coverage

Honor the user's paths, service, specification, diff, or concerns. For a change review, inspect both the changed surface and affected consumers. For a whole-API review, inventory resources and common contract machinery before choosing representative operations. Inspect shared middleware as well as endpoint handlers; a missing local check may be supplied centrally.

Look for OpenAPI or another contract definition, routes, schemas/serializers, validators, error handlers, authentication/authorization, tests, docs, and known clients. If OpenAPI is absent, review from those artifacts and mark schema completeness as unassessed. Do not create a specification as a prerequisite.

Use the shared topic map to identify applicable areas. Prioritize behavior, security, client breakage, and inconsistency that increases consumer effort. Load launch, monetization, or compliance chapters only when the scope makes them relevant. Record what was assessed, sampled, unavailable, or outside scope; do not imply complete coverage from a small sample.

## Investigate findings

Trace a suspected issue to the actual contract or implementation and an observable consequence. Check project decisions and nearby patterns before calling a convention a defect. Separate protocol violations, implementation/contract mismatches, and guide recommendations. A deliberate, documented alternative can be a tradeoff rather than a finding.

For each retained finding, identify the operation or schema location, concrete evidence, affected consumer behavior, relevant Speakeasy section (and standard when needed), and smallest useful correction. Explain whether that correction changes the published contract. Mark a plausible but unverified risk as such; avoid invented consumers, arbitrary compliance scores, and unsupported severity labels.

Run existing read-only validation or isolated tests when useful and authorized. Do not send state-changing requests to a live service just to substantiate a review. If runtime access is unavailable, state what static evidence establishes and what remains unverified.

## Deliver

Use [report-format.md](references/report-format.md) for a review proportional to the scope. Findings come first, ordered by impact. Include material strengths or cleared concerns only when they help the decision. If no actionable findings survive investigation, say so and report the coverage limits. Suggest a sequence of corrections; do not begin a migration solely because the review found one.
