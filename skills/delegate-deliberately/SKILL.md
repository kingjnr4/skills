---
name: delegate-deliberately
description: Controls subagent spawning and delegation in agentic workflows. Use whenever an agent can create subagents, child agents, parallel agents, agent teams, or delegated threads, especially before planning, researching, searching a codebase, debugging, implementing, testing, or reviewing. Prefer direct execution and permit delegation only when independent parallel work or context isolation clearly outweighs coordination and token overhead.
---

# Delegate Deliberately

Complete work in the main thread by default. Treat delegation as an optimization that must justify its coordination cost, not as a routine planning step.

## Apply the default

- Start every user request with a subagent budget of zero.
- Use direct tools, local search, and the current context first when they can solve the task cleanly.
- Do not spawn an agent merely to inspect a few files, run a command, confirm an obvious fact, restate the plan, or review the main agent's work.
- Obey higher-priority instructions and explicit user requests for delegation. When no agent count is specified, still use the minimum needed.

## Require all four delegation gates

Spawn a subagent only when every gate passes:

1. **Independent:** The workstream can proceed without frequent coordination or results from another workstream.
2. **Substantial:** It contains enough investigation or implementation to repay the handoff and synthesis overhead.
3. **Beneficial:** Parallel execution will materially shorten the critical path, isolated context will prevent large disposable inputs from polluting the main thread, or a genuinely distinct specialist perspective will materially improve coverage.
4. **Bounded:** The assignment has a precise scope, clear inputs, a concrete deliverable, and an unambiguous stopping point.

If any gate fails, work directly in the main thread.

## Keep a tight thread budget

- Spawn at most one subagent initially.
- Add a second only when it owns a separate qualifying workstream that can run concurrently.
- Do not exceed two subagents per user request unless the user or a higher-priority instruction explicitly requests more.
- Reuse or steer an existing subagent instead of creating another for follow-up work.
- Instruct subagents not to spawn descendants. Keep delegation depth at one unless deeper delegation is explicitly required.
- Avoid concurrent edits to the same files or other shared mutable state. Prefer read-only delegation; give write ownership to one agent at a time.

## Work directly for these cases

Do not delegate:

- simple questions, summaries, explanations, or status checks;
- single-file or tightly coupled edits;
- sequential tasks where each step depends on the previous result;
- small codebase searches that local search can answer quickly;
- one dominant slow command, build, test, download, or external operation;
- tasks requiring continuous use of the main conversation's nuanced context;
- duplicate reviews with no distinct lens or acceptance criteria;
- work that would require the parent to repeat most of the investigation during synthesis.

## Delegate only strong fits

Good candidates include:

- independent exploration of separate large subsystems;
- several plausible root causes that can be investigated independently;
- read-heavy processing of large logs, documents, or search results when only a concise finding is needed;
- independent implementation units with disjoint file ownership;
- explicitly requested parallel reviews with distinct lenses such as security, correctness, and test coverage.

Even for a strong fit, use only the smallest number of agents that maps cleanly to the independent workstreams.

## Write bounded handoffs

Every delegated prompt must state:

- the single objective;
- the exact scope and relevant inputs;
- whether edits are allowed and which files the agent owns;
- the required output, evidence, and verification;
- constraints, including no further delegation;
- what not to investigate when scope creep is likely.

While a subagent runs, continue useful independent work in the main thread. Do not spawn and immediately wait unless the main thread is genuinely blocked.

## Synthesize once

- Verify important claims against returned evidence or shared artifacts.
- Integrate results into one coherent answer or change set.
- Resolve contradictions in the main thread instead of spawning a tie-breaker by default.
- Report the outcome, not the orchestration mechanics, unless the user asks.

## Decision examples

| Situation | Decision |
| --- | --- |
| Find where one route is defined and patch it | Work directly |
| Diagnose one failure from a short log | Work directly |
| Explore auth, billing, and notifications in a large repository | Delegate at most two independent areas; handle the third in the main thread |
| Run one slow test suite | Run it directly; another agent does not shorten the command |
| Review a PR for security and test gaps in parallel | Use two agents only if both reviews are substantial and distinct |
| Implement changes across files that share the same interfaces | Keep one writer; delegate read-only analysis at most |
