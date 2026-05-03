---
name: to-dos
description: Turn rough notes into a concise, codebase-aware to-do document. Each task gets a brief description grounded in the project's context.md and actual code. Use when user wants to create a to-do list, task list, mentions "to-dos", "todos", "task list", or drops notes they want turned into actionable tasks.
---

# To-Dos

Turn rough notes into a short, actionable to-do document grounded in the codebase.

## Process

1. **Read the user's notes.** Accept any format — bullet points, sentence fragments, keywords, stream of consciousness.

2. **Gather project context.** Read the project's `.kiro/steering/project-context.md` (or equivalent context file) and explore relevant parts of the codebase to understand the current state — what exists, what's missing, what conventions are in place.

3. **Map notes to tasks.** For each note, determine:
   - What concrete work needs to happen
   - Where in the codebase it applies (module, feature area, layer)
   - Any dependencies or ordering constraints between tasks

4. **Write the to-do document.** Output a markdown document using the template below. Keep it short — one line per task, no essays.

## Output Template

```markdown
# To-Do

> Generated from notes on [date]. Context: [project name / area].

| # | Task | Area | Notes |
|---|------|------|-------|
| 1 | [Short imperative description] | [Module or feature area] | [Optional: dependency, blocker, or context — keep to a few words] |
| 2 | ... | ... | ... |
```

## Rules

- **Be concise.** Each task description should be one short sentence in imperative form ("Add validation to X", "Create migration for Y").
- **Ground in the codebase.** Reference actual modules, files, or conventions from the project. Don't invent structure that doesn't exist.
- **Use the project's vocabulary.** Match terminology from context.md and the codebase (e.g., use "MWST" not "VAT" if that's what the project uses).
- **Respect ordering.** If tasks have dependencies, list them in execution order and note the dependency.
- **Don't pad.** If the user gives 3 notes, produce 3 tasks. Don't invent extra work.
- **Skip obvious context.** Don't restate what the project is. The reader already knows.
- **Ask if ambiguous.** If a note is too vague to map to a concrete task, ask the user rather than guessing.
