# AI Prompts & Skills

A collection of reusable AI prompts that work across different tools and models.

## Prompts

| Prompt | Description |
|--------|-------------|
| [grill-me](prompts/grill-me.md) | Interview you relentlessly about a plan until reaching shared understanding |
| [design-grill](prompts/design-grill.md) | Grill you on design choices — architecture, patterns, data modeling, trade-offs |

## Usage

### Any AI Chat (ChatGPT, Claude, Gemini, etc.)

Copy the **Prompt** section from any file in `prompts/` and paste it into your chat, followed by your plan or design description.

### Kiro

The prompts are also available as Kiro skills in `.kiro/skills/`. They activate automatically when you use trigger phrases like "grill me" or "design grill".

### Cursor / Windsurf / Other IDE Agents

Add the prompt files as rules or context. For example in Cursor, reference them with `@prompts/design-grill.md` in your chat.

### Claude Code / Aider

Use the prompt files as system prompts or include them via CLI flags:

```bash
# Claude Code — add as a CLAUDE.md reference or paste directly
# Aider — use --read flag
aider --read prompts/design-grill.md
```

## Adding New Prompts

1. Create a new `.md` file in `prompts/`.
2. Follow the existing format: title, description, "How to Use" section, then the prompt itself.
3. If you also want it as a Kiro skill, create a matching `SKILL.md` in `.kiro/skills/<name>/` with the frontmatter format Kiro expects.
4. Update this README table.
