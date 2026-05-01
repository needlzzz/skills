# AI Prompts & Skills

A collection of reusable AI prompts that work across different tools and models. The prompts live in `prompts/` as plain markdown (LLM-agnostic). Tool-specific wrappers are provided where needed.

## Prompts

| Prompt | Description |
|--------|-------------|
| [grill-me](prompts/grill-me.md) | Interview you relentlessly about a plan until reaching shared understanding |
| [design-grill](prompts/design-grill.md) | Grill you on design choices — architecture, patterns, data modeling, trade-offs |
| tdd | Test-driven development with red-green-refactor loop (Kiro skill only for now) |

## Architecture

```
prompts/                  ← LLM-agnostic markdown (works everywhere)
  design-grill.md
  grill-me.md

.kiro/skills/             ← Kiro-specific wrappers (SKILL.md with frontmatter)
  design-grill/SKILL.md
  grill-me/SKILL.md
  tdd/SKILL.md
```

The `prompts/` folder is the source of truth. Each file is a standalone prompt you can paste into any AI chat, IDE agent, or CLI tool. The `.kiro/skills/` folder contains Kiro-specific wrappers that reference the same logic but add frontmatter so Kiro can detect and activate them automatically.

## Setup

### Making prompts available globally (any tool)

The prompts in `prompts/` are plain markdown. Copy-paste them into any AI chat or reference them from any tool. No setup required.

### Kiro — global skills via symlink

Kiro looks for skills in `~/.kiro/skills/` (user-level, available in every workspace). Instead of copying files every time you add a skill, symlink the folder:

```bash
# Clone this repo somewhere permanent
git clone https://github.com/needlzzz/skills.git ~/path/to/skills

# Symlink so Kiro picks up all skills globally
ln -s ~/path/to/skills/.kiro/skills ~/.kiro/skills
```

On Windows (WSL):
```bash
ln -s /mnt/c/Users/<you>/path/to/skills/.kiro/skills ~/.kiro/skills
```

On Windows (PowerShell, native — run as admin):
```powershell
New-Item -ItemType SymbolicLink -Path "$env:USERPROFILE\.kiro\skills" -Target "C:\Users\<you>\path\to\skills\.kiro\skills"
```

Now every skill you add to this repo is immediately available in all Kiro workspaces. Just `git pull` to get updates.

### Claude Code

Create a `CLAUDE.md` at your home directory or project root that references the prompts:

```markdown
See ~/path/to/skills/prompts/ for reusable prompt instructions.
```

Or symlink individual prompts into your project.

### Cursor / Windsurf

Add prompt files as rules or context. In Cursor, reference them with `@prompts/design-grill.md` in chat. In Windsurf, add them to your rules configuration.

### Aider

```bash
aider --read ~/path/to/skills/prompts/design-grill.md
```

## Project-Scoped Context

Global skills define *how* the AI behaves (workflows, question formats, rules). But each project also needs its own context — what the project is, how it's built, what conventions it follows.

This is what **steering files** and **project-level context** are for. They are scoped to a single project and never leak into other workspaces.

### Kiro — steering files (project-scoped)

Create `.kiro/steering/` in your project root. Markdown files here are automatically included in every Kiro conversation for that project.

```
my-project/
  .kiro/
    steering/
      project-context.md    ← always included
      api-conventions.md    ← always included
      testing-guide.md      ← always included
```

Example `project-context.md`:
```markdown
# Project Context

This is a React + TypeScript SPA with a Go backend. 
The API follows REST conventions defined in docs/api-spec.yaml.
We use PostgreSQL with sqlc for type-safe queries.
Tests use Vitest for frontend and Go's testing package for backend.

## Build & Run
- Frontend: `npm run dev` (Vite)
- Backend: `go run ./cmd/server`
- Tests: `npm test` / `go test ./...`

## Conventions
- All API responses use the envelope format: `{ data, error, meta }`
- Feature flags live in `config/flags.yaml`
- Database migrations are in `db/migrations/` using golang-migrate
```

### Conditional steering (only when relevant files are open)

Add frontmatter to scope a steering file to specific file patterns:

```markdown
---
inclusion: fileMatch
fileMatchPattern: '**/*.test.ts'
---

# Testing Conventions

Use `describe` blocks grouped by feature, not by function.
Prefer integration tests over unit tests.
Mock only external services, never internal modules.
```

This file only activates when a test file is open — it won't clutter context otherwise.

### Manual steering (opt-in via # mention)

```markdown
---
inclusion: manual
---

# Deployment Checklist

1. Run full test suite
2. Check migration compatibility
3. ...
```

This file is only included when you explicitly reference it with `#` in Kiro chat.

### Claude Code — project context via CLAUDE.md

Place a `CLAUDE.md` in your project root with project-specific context. Claude Code reads it automatically.

### Cursor — .cursorrules

Place a `.cursorrules` file in your project root with project conventions and context.

### Windsurf — .windsurfrules

Place a `.windsurfrules` file in your project root.

## Summary: Global vs Project-Scoped

| What | Scope | Where it lives |
|------|-------|----------------|
| Skills / prompts (this repo) | Global — same behavior everywhere | `~/.kiro/skills/` (symlinked) or `prompts/` (copy-paste) |
| Steering / context files | Per-project — describes *this* codebase | `.kiro/steering/` in the project root |
| `.cursorrules` / `CLAUDE.md` | Per-project (tool-specific) | Project root |

The idea: skills define reusable *workflows* (how to grill, how to do TDD). Steering/context files describe the *project* (what to build, what conventions to follow). Keep them separate so skills stay portable across projects.

## Adding New Prompts

1. Create a new `.md` file in `prompts/` with the prompt content. This is the LLM-agnostic version.
2. If you want it as a Kiro skill, create `.kiro/skills/<name>/SKILL.md` with Kiro frontmatter (`name`, `description`).
3. Update this README table.
4. Commit and push. Anyone with the symlink gets the new skill automatically.
