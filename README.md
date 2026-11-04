# Agent skills

## API design

Speakeasy-based HTTP API design with shared guidance and explicit review/refactor workflows. Install the three skill folders together so both workflows can load `api-design`.

| Skill                                        | Invocation    | Purpose                                                                    |
| -------------------------------------------- | ------------- | -------------------------------------------------------------------------- |
| [api-design](skills/api-design/SKILL.md)     | Model or user | Design and change HTTP contracts using relevant Speakeasy chapters         |
| [review-api](skills/review-api/SKILL.md)     | User only     | Review existing APIs or contract changes with evidence and coverage limits |
| [refactor-api](skills/refactor-api/SKILL.md) | User only     | Implement scoped improvements with compatibility and migration checks      |

Examples in Codex:

```text
Use $api-design to design a paginated GET /orders endpoint.
Use $review-api to assess the billing API from its routes and tests.
Use $refactor-api to improve error consistency while preserving current clients.
```

The core skill bundles all 25 guide pages and 24 images from Speakeasy's rest apiguide.

## Other skills

- [delegate-deliberately](skills/delegate-deliberately/SKILL.md): use subagents only when their benefit outweighs coordination overhead.
