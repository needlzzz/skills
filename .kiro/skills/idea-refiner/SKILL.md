---
name: idea-refiner
description: Turn rough keywords and fragments about a project idea into a specific, actionable idea brief. Use when user drops loose words, phrases, or half-formed thoughts about a project idea and wants help shaping them into something concrete, or mentions "refine my idea", "idea refiner", or "shape this idea".
---

# Idea Refiner

Turn scattered words into a sharp project idea.

## How it works

The user drops rough input — keywords, phrases, sentence fragments — about a project they're thinking about. Your job is to extract signal, ask the right questions, and produce a focused idea brief.

## Step 1: Absorb the raw input

Read everything the user provides without judgment. Identify:

- **Domain clues** — what space is this in? (health, finance, dev tools, etc.)
- **Action clues** — what does it do? (track, generate, connect, automate, etc.)
- **Audience clues** — who is it for? (developers, small businesses, students, etc.)
- **Problem clues** — what pain does it solve?

## Step 2: Fill the gaps

After absorbing, identify which of these are missing or vague. Ask **up to 5 targeted questions** to fill gaps. Questions should be multiple-choice or short-answer to keep momentum. Group them in a single message.

Key dimensions to probe:

- [ ] **Who** — Who specifically would use this? What's their day look like?
- [ ] **Pain** — What's the current frustration or workaround?
- [ ] **Core action** — What's the one thing this tool does that matters most?
- [ ] **Scope** — Is this a CLI tool, web app, mobile app, API, browser extension?
- [ ] **Differentiation** — What exists today and why isn't it enough?

Skip questions where the user's input already gives a clear answer.

## Step 3: Produce the idea brief

Once you have enough signal (from input + answers), produce this:

```
## Idea Brief: [Working Title]

**One-liner:** [One sentence that explains what this is]

**Problem:** [2-3 sentences on the pain point]

**Target user:** [Specific persona, not "everyone"]

**Core features:**
1. [Most important thing it does]
2. [Second most important]
3. [Third — keep it to 3-5]

**Form factor:** [Web app / CLI / API / mobile / extension / etc.]

**What exists today:** [Current alternatives and their gaps]

**What makes this different:** [The key insight or angle]
```

## Rules

- Never pad the brief with generic filler. Every line should be specific to this idea.
- If the user's input is too vague even after questions (e.g., just "app"), say so honestly and ask for more raw material.
- Keep the tone direct. This is a thinking tool, not a pitch deck.
- If the user provides more words after the brief, treat it as iteration — update the brief, don't start over.
- The brief should be concise enough to fit in a single screen.
