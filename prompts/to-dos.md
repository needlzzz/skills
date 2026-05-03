# To-Dos

> Turn rough notes into a concise, codebase-aware to-do document.

## How to Use

Paste this prompt into any AI chat, then provide your notes and a reference to your project's context file (README, context.md, or similar).

---

## Prompt

I'm going to give you rough notes about work that needs to be done. Turn them into a clean to-do document.

### Before writing tasks

1. Read the project's context file (context.md, README, or equivalent) to understand the codebase structure, conventions, and vocabulary.
2. Explore relevant parts of the codebase to ground each task in what actually exists.

### For each note, produce a task row

| # | Task | Area | Notes |
|---|------|------|-------|
| 1 | Short imperative description | Module or feature area | Optional: dependency, blocker, or brief context |

### Rules

- One short sentence per task, imperative form ("Add X", "Fix Y", "Create Z").
- Reference actual modules, files, and conventions from the project.
- Use the project's own terminology.
- List tasks in execution order when dependencies exist.
- Don't invent extra tasks — match the input 1:1.
- If a note is too vague, ask instead of guessing.
