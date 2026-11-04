# API review report

Scale the report to the request. A single-operation review can be a few paragraphs; a service review benefits from a coverage table.

## Findings

Order by consumer impact. For each actionable finding include:

- **Finding and impact:** what happens to a consumer, and when.
- **Evidence:** operation/schema pointer or repository `file:line`, with observed versus inferred behavior distinguished.
- **Basis:** protocol requirement, contract mismatch, or Speakeasy recommendation; link the relevant guide page and name the section. Cite the standard if it resolves an upstream ambiguity.
- **Correction:** smallest useful change and whether it is behavior-preserving, additive, or potentially breaking.
- **Verification:** check performed and result, or the remaining check needed.

Severity, if useful: high for supported security/data-loss or widespread client-breakage consequences; medium for a reproducible functional or integration problem; low for bounded consistency or usability friction. Keep optional preferences separate from defects. Do not inflate severity because a guide recommendation was not followed.

## Coverage and next actions

State the scope and artifacts inspected. For broader reviews, use:

| Area | Assessed surface | Result or limitation |
| --- | --- | --- |
| Applicable topic | Operations/files, including any sampling | Findings, checked with no finding, unavailable, or not applicable |

Mention applicable areas that were not assessed. End with the most useful correction order and unresolved questions that materially affect it. Do not turn the report into a complete rewrite proposal unless requested.
