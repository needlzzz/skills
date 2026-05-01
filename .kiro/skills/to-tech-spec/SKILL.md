---
name: to-tech-spec
description: Turn the current conversation context into an AI-ready technical specification that a coding agent can execute. Use when user wants to generate a tech spec, technical specification, build spec, implementation spec, or says "spec this out", "make it buildable", or "to tech spec".
---

# To Tech Spec

Synthesize the current conversation into a technical specification precise enough for an AI coding agent to build from.

## When to use

After the user has discussed, refined, or grilled an idea in conversation and wants to turn it into a buildable document. Do NOT interview the user — extract everything from the conversation context and any referenced files.

## Process

### 1. Mine the conversation

Scan the full conversation for:

- **What it does** — features, behaviors, user flows
- **Decisions made** — tech choices, architecture, scope cuts
- **Constraints mentioned** — budget, timeline, platform, dependencies
- **Open questions resolved** — anything that was debated and settled

If an idea brief or PRD exists in the conversation, use it as the backbone.

### 2. Explore the repo (if applicable)

If there's an existing codebase, read the project structure, package files, and key modules to understand:

- Language, framework, and tooling already in use
- Patterns to follow (naming, file structure, state management)
- What already exists vs. what needs to be built

### 3. Produce the tech spec

Write the spec to the file the user specifies, or default to `TECH-SPEC.md` in the project root. Use the template in [TEMPLATE.md](mdc:TEMPLATE.md).

## Rules

- Write for a machine audience. Be explicit about every behavior — no "intuitive UX" or "handle edge cases appropriately."
- Every feature must have acceptance criteria. If you can't write a concrete check for it, it's too vague.
- Prefer concrete examples over abstract descriptions. Show sample payloads, file names, CLI output.
- If the conversation left gaps that matter for implementation, list them in an **Open Questions** section rather than guessing.
- Do not invent features that weren't discussed. Stick to what was actually decided.
- Keep the spec under 500 lines. If it's longer, the scope is too big — suggest splitting.
