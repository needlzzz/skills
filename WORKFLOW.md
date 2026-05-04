# From Notes to Finished App — Skill Workflow Guide

How to use the skills in this repo to go from scattered thoughts to a running application. Each stage builds on the previous one, but you can enter at any point and skip what you don't need.

## The Pipeline at a Glance

```
 ┌──────────────┐    ┌──────────┐    ┌──────────────┐    ┌─────────────┐    ┌───────────┐
 │ idea-refiner │ ─▶ │ grill-me │ ─▶ │ to-tech-spec │ ─▶ │  build-app  │ ─▶ │    tdd    │
 │              │    │ design-  │    │  (or to-prd) │    │             │    │           │
 │ rough words  │    │ grill    │    │              │    │ pre-flight  │    │ red-green │
 │ → idea brief │    │ → battle-│    │ → buildable  │    │ → built app │    │ → tested  │
 └──────────────┘    │   tested │    │   spec       │    └─────────────┘    │   code    │
                     │   plan   │    └──────────────┘                       └───────────┘
                     └──────────┘
```

**Supporting skills** (use at any stage):

| Skill | Purpose | When to reach for it |
|-------|---------|----------------------|
| **to-dos** | Turn rough notes into a codebase-aware task list | Organizing work at any stage |
| **er-model** | Generate an ER diagram from the codebase | Visualizing data models during design or after build |
| **build-feature** | Plan and spec a single feature on an existing codebase | Adding to an app that already exists |
| **write-a-skill** | Create new skills for your team | When you want to codify a recurring workflow |
| **git-guardrails-claude-code** | Block dangerous git commands in Claude Code | Safety setup before any build phase |

---

## Stage 1: Idea Refiner — "I have a vague thought"

**Skill:** `idea-refiner`
**Trigger:** Say "refine my idea" and drop your raw input — keywords, fragments, half-sentences.

### What it does

Takes your scattered thoughts and turns them into a structured **idea brief**: one-liner, problem statement, target user, core features (3–5), form factor, existing alternatives, and what makes this different.

### How to use it

1. Dump everything you have — don't worry about structure or completeness.
2. Answer up to 5 targeted questions the skill asks to fill gaps.
3. Receive a focused idea brief you can iterate on.

### What you get out

```
## Idea Brief: [Working Title]
**One-liner:** ...
**Problem:** ...
**Target user:** ...
**Core features:** 1. ... 2. ... 3. ...
**Form factor:** ...
**What exists today:** ...
**What makes this different:** ...
```

### Skip this stage if...

You already have a clear idea of what you're building. Jump to Stage 2 or 3.

---

## Stage 2: Grill — "Is this idea solid?"

**Skills:** `grill-me` (general) or `design-grill` (architecture-focused)
**Trigger:** Say "grill me" or "design grill" followed by your plan.

### Which one to pick

| Skill | Best for | Focus areas |
|-------|----------|-------------|
| **grill-me** | General plans, scope, requirements, feasibility | Every branch of the decision tree — scope, behavior, edge cases, dependencies |
| **design-grill** | Architecture and technical design | Architecture, data modeling, API design, patterns, state management, security, scalability, failure modes, extensibility |

Use **grill-me** first to nail down *what* you're building. Then use **design-grill** to nail down *how* you're building it. Or use just one if the other isn't needed.

### How to use it

1. Paste your idea brief (from Stage 1) or describe your plan.
2. Choose your mode when prompted:
   - **Question by question** — you decide on each question individually.
   - **Accept all recommendations** — the AI walks every branch using its own recommendations and delivers a decision log.
   - **Cherry-pick** — see all questions upfront, accept some, discuss others.
3. Answer questions honestly. The skill will push back on vague answers and flag contradictions.
4. Receive a **decision log** summarizing every resolved branch.

### What you get out

A battle-tested plan with every ambiguity resolved and every trade-off acknowledged. This becomes the input for Stage 3.

### Skip this stage if...

You've already thought through the design thoroughly and just need it written down as a spec.

---

## Stage 3: Spec — "Make it buildable"

**Skills:** `to-tech-spec` (for AI agents) or `to-prd` (for human stakeholders)
**Trigger:** Say "to tech spec" / "spec this out" or "to prd".

### Which one to pick

| Skill | Audience | Output |
|-------|----------|--------|
| **to-tech-spec** | AI coding agents | Tech stack, data model, API routes, features with acceptance criteria, UI specs, implementation order |
| **to-prd** | Human stakeholders, product teams | Problem statement, solution, implementation decisions, testing decisions, scope boundaries |

For the idea-to-code pipeline, **to-tech-spec** is the default choice. Use **to-prd** when you need a document for humans to review and approve before building.

### How to use it

1. Make sure the conversation already contains the decisions from Stage 2 (or your own planning).
2. Say "to tech spec" — the skill mines the entire conversation without re-interviewing you.
3. If there's an existing codebase, the skill reads it to match patterns and conventions.
4. Receive a `TECH-SPEC.md` (or `PRD.md`) written to the project root.

### What you get out

A structured specification with:
- Tech stack and project structure
- Data model with field-level detail
- API routes / server actions with request/response shapes
- Features broken into tasks with acceptance criteria
- UI specifications
- Step-by-step implementation order

### Skip this stage if...

You already have a spec or PRD. Jump straight to Stage 4.

---

## Stage 4: Build — "Build this"

**Skill:** `build-app`
**Trigger:** Say "build this" / "build the app" / "implement this spec".

### How to use it

1. The skill locates your tech spec (or PRD) automatically.
2. It runs a **pre-flight scan** and reports:
   - **Commands it will run** — add these to your trusted list so the build doesn't stall.
   - **Commands you run yourself** — dev servers, Docker, anything long-running.
   - **Blockers** — missing env vars, API keys, unresolved ambiguities. Must be fixed before building.
   - **Handled** — decisions the agent makes on your behalf (e.g., choosing npm over yarn).
   - **Ambiguities** — judgment calls the agent made. Override if you disagree.
3. Resolve any blockers.
4. The build starts: scaffold → install → implement → compile → test → report.

### What you get out

A built project with a summary of what was created and any remaining manual steps (deployment, env setup, etc.).

---

## Stage 5: Test — "Make it robust"

**Skill:** `tdd`
**Trigger:** Say "tdd" / "red-green-refactor" / "test-first".

### When to use it

- **During the build** — if you want features built test-first, invoke TDD instead of (or alongside) build-app.
- **After the build** — to add test coverage to what was already built.
- **For bug fixes** — write a failing test that reproduces the bug, then fix it.

### How to use it

1. Confirm with the skill which behaviors to test and what the public interface looks like.
2. The skill works in vertical slices — one test at a time:
   ```
   RED:   Write test → fails
   GREEN: Write minimal code → passes
   REFACTOR: Clean up → tests still pass
   ```
3. It never writes all tests first. Each test responds to what was learned from the previous cycle.

### Key principles

- Tests verify **behavior through public interfaces**, not implementation details.
- A good test survives internal refactors.
- Focus testing effort on critical paths and complex logic, not every edge case.

---

## Supporting Skills

These aren't part of the linear pipeline but are useful at various stages.

### to-dos — Organize work at any stage

**Trigger:** Say "to-dos" and drop rough notes.

Turns scattered notes into a codebase-aware task table. Each task is grounded in actual modules and conventions from the project. Useful for:
- Breaking down a spec into work items before building.
- Tracking bugs and improvements alongside feature work.
- Organizing thoughts between stages.

### er-model — Visualize data relationships

**Trigger:** Say "er-model" or "entity diagram".

Scans SQL migrations, TypeScript types, and Zod schemas to generate a Mermaid ER diagram. Useful for:
- Reviewing the data model during Stage 2 (design grill).
- Documenting the schema after Stage 4 (build).
- Spotting missing relationships or orphaned tables.

### build-feature — Add to an existing app

**Trigger:** Say "build feature" / "new feature" / "add feature".

A two-phase skill that combines **grill-me** + **to-tech-spec** scoped to a single feature on an existing codebase. Use this instead of the full pipeline when the app already exists and you're adding something new. It:
1. Grills you on the feature (scope, behavior, edge cases, data changes, UI impact).
2. Produces a `FEATURE-SPEC.md` that references existing files and patterns by name.

### write-a-skill — Create new skills

**Trigger:** Say "write a skill".

Guides you through creating a new skill with proper structure, description, and bundled resources. Use when you want to codify a recurring workflow for your team.

### git-guardrails-claude-code — Safety for Claude Code

**Trigger:** Say "git guardrails".

Sets up hooks to block dangerous git commands (`push`, `reset --hard`, `clean -f`, `branch -D`) in Claude Code. Run this before any build phase if you're using Claude Code as your agent.

---

## Choosing Your Entry Point

| You have... | Start at | Skills to use |
|-------------|----------|---------------|
| Scattered keywords and fragments | Stage 1 | idea-refiner → grill-me → to-tech-spec → build-app |
| A clear idea, not yet validated | Stage 2 | grill-me / design-grill → to-tech-spec → build-app |
| A validated plan, needs a spec | Stage 3 | to-tech-spec → build-app |
| A written spec, ready to build | Stage 4 | build-app |
| A built app, needs tests | Stage 5 | tdd |
| An existing app, adding a feature | Any | build-feature (combines grill + spec for one feature) |
| Rough notes about work to do | Any | to-dos |

## Example: Full Pipeline Run

Here's what a complete run looks like for a new project:

```
You:   "refine my idea: swiss plumber app, scheduling, invoices, qr codes"
       ↓ idea-refiner asks 5 questions, produces idea brief

You:   "grill me" + paste the idea brief
       ↓ grill-me walks every branch, produces decision log

You:   "design grill" (optional, for architecture decisions)
       ↓ design-grill challenges data model, API design, security

You:   "to tech spec"
       ↓ to-tech-spec mines the conversation, writes TECH-SPEC.md

You:   "build this"
       ↓ build-app runs pre-flight, flags blockers, then builds

You:   "tdd" (optional, for critical paths)
       ↓ tdd adds test coverage with red-green-refactor
```

Each stage produces an artifact that feeds the next. You stay in control of every decision, and you can pause, iterate, or skip stages as needed.
