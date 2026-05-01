---
name: design-grill
description: Grill the user specifically on design choices — architecture, patterns, data modeling, API contracts, UX flows, and trade-offs. Use when user wants to stress-test design decisions, validate architectural choices, or mentions "design grill" or "grill my design".
---

# Design Grill

## Quick Start

Grill me relentlessly on every design choice in this plan. Challenge my architecture, patterns, data models, API contracts, UX flows, and trade-offs. For each question, explain what could go wrong with my current choice and recommend an alternative if you see one.

## Workflow

1. **Ask one design question at a time** — never batch multiple questions into a single message.
2. **Provide your recommended answer** with each question so the user can accept, reject, or refine it.
3. **If a question can be answered by exploring the codebase**, explore the codebase instead of asking the user.
4. **Resolve dependencies first** — if a later design decision depends on an earlier one, walk the earlier branch to completion before moving on.
5. **Track progress** — mentally map the design decision tree and mark branches as resolved.
6. **Challenge trade-offs** — for every choice, probe what was traded away and whether the user has considered the cost.
7. **Wrap up** — once all branches are resolved, summarize the shared understanding as a concise design decision log with rationale for each choice.

## Design Branches to Cover

Work through these areas as they apply to the plan. Skip branches that are clearly irrelevant.

- **Architecture** — system boundaries, component responsibilities, layering, monolith vs services, deployment topology.
- **Data modeling** — entities, relationships, normalization, storage engine choice, schema evolution strategy.
- **API design** — contracts, versioning, error handling, pagination, authentication/authorization surface.
- **Patterns & abstractions** — design patterns chosen (and rejected), abstraction levels, coupling between modules.
- **State management** — where state lives, how it flows, caching strategy, consistency guarantees.
- **UX / interaction design** — user flows, edge cases in the UI, loading/error states, accessibility considerations.
- **Scalability & performance** — expected load, bottlenecks, indexing strategy, async vs sync boundaries.
- **Security** — threat surface, input validation, secrets management, least-privilege boundaries.
- **Failure modes** — what happens when dependencies fail, retry/fallback strategy, observability.
- **Extensibility** — how the design accommodates future requirements without major rewrites.

## Question Format

For each question use this structure:

```
**[Design Branch / Topic]**

Question: [Your specific design question]

Risk if ignored: [What could go wrong with the current choice or lack of a choice]

My recommendation: [Your suggested answer and why]
```

## Fast-Track Mode

At any point the user can say **"go with your recommendations"** (or similar). When this happens:

1. Stop asking questions.
2. For every remaining unresolved design branch, apply your recommended answer.
3. Present the full decision log — both the branches already resolved through discussion and the ones you auto-resolved — clearly marking which decisions were user-confirmed vs. auto-recommended.
4. Ask the user to review the log and flag anything they want to revisit before finalizing.

## Rules

- One question per message, no exceptions.
- Don't accept vague answers — push for specifics. "We'll figure it out later" is not an answer.
- If the user's answer contradicts an earlier design decision, flag the conflict and resolve it before moving on.
- If a choice introduces unnecessary complexity, call it out and ask the user to justify it.
- If a simpler alternative exists that meets the same requirements, present it as a challenge.
- Keep going until every relevant design branch is covered. Don't stop early.
- When wrapping up, note any open risks or decisions that were deferred with the user's explicit agreement.
