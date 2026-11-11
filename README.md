# Agent skills

## API design

Self-contained HTTP API design guidance with optional deeper reading in Speakeasy's guide, plus explicit review/refactor workflows. Install `api-design` alone, or include it alongside either workflow.

| Skill                                        | Invocation    | Purpose                                                                    |
| -------------------------------------------- | ------------- | -------------------------------------------------------------------------- |
| [api-design](skills/api-design/SKILL.md)     | Model or user | Design and change HTTP contracts using compact, self-contained guidance    |
| [review-api](skills/review-api/SKILL.md)     | User only     | Review existing APIs or contract changes with evidence and coverage limits |
| [refactor-api](skills/refactor-api/SKILL.md) | User only     | Implement scoped improvements with compatibility and migration checks      |

Examples in Codex:

```text
Use $api-design to design a paginated GET /orders endpoint.
Use $review-api to assess the billing API from its routes and tests.
Use $refactor-api to improve error consistency while preserving current clients.
```

The core skill is a single `SKILL.md`, with [Speakeasy's REST API Design Guide](https://www.speakeasy.com/api-design) linked for further reference; no bundled articles or images are required.

### OpenCode

Install the skill folders under `~/.config/opencode/skills/` or the target project's `.opencode/skills/`. Invoke them with `@` mentions; no command wrappers are needed. The review and refactor skills retain `disable-model-invocation: true` for user-only invocation.

```text
@review-api assess the billing API from its routes and tests
@refactor-api improve error consistency while preserving current clients
```

## Other skills

- [delegate-deliberately](skills/delegate-deliberately/SKILL.md): use subagents only when their benefit outweighs coordination overhead.
