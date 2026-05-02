---
name: build-feature
description: Plan a single new feature on top of an existing codebase. Grills the user on every aspect of the feature, then produces an AI-ready tech spec. Use when user wants to add a feature, plan a feature, says "build feature", "new feature", "add feature", or "plan feature".
---

# Build Feature

Plan and specify a single new feature for an existing codebase. Two phases: grill, then spec.

## Quick Start

When triggered, run Phase 1 then Phase 2 in order. Do not skip phases.

## Phase 1 — Grill (invoke grill-me)

Activate the **grill-me** skill and run its full workflow scoped to the new feature:

1. Explore the existing codebase first — read project structure, key modules, data models, and patterns already in use. Use what you learn to inform your questions.
2. Present the grill-me opening message (question-by-question / accept all / cherry-pick).
3. Interview the user on every branch of the feature: scope, behavior, edge cases, data changes, API surface, UI impact, dependencies, migration needs, and rollback strategy.
4. For any question answerable from the codebase, answer it yourself instead of asking.
5. End Phase 1 with a concise **decision log** summarizing every resolved branch.

## Phase 2 — Tech Spec (invoke to-tech-spec)

Once the decision log is complete, activate the **to-tech-spec** skill:

1. Mine the conversation and decision log — do NOT re-interview the user.
2. Explore the repo to capture the existing stack, patterns, and what already exists.
3. Produce the tech spec using the to-tech-spec TEMPLATE, scoped to only the new feature and its touchpoints with the existing code.
4. Write the spec to `FEATURE-SPEC.md` in the project root (or a path the user specifies).

## Rules

- Stay scoped to one feature. If the user's idea is multiple features, pick the core one and note the rest as future work.
- Never invent requirements the user didn't confirm during the grill.
- The tech spec must reference existing files and patterns by name — an agent building from it should not have to rediscover the codebase.
- If the codebase has tests, include a testing section in the spec that follows the existing test patterns.
