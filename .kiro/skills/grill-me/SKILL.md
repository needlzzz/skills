---
name: grill-me
description: Interview the user relentlessly about a plan or design until reaching shared understanding, resolving each branch of the decision tree. Use when user wants to stress-test a plan, get grilled on their design, or mentions "grill me".
---

# Grill Me

## Quick Start

Interview me relentlessly about every aspect of this plan until we reach a shared understanding. Walk down each branch of the design tree, resolving dependencies between decisions one-by-one. For each question, provide your recommended answer.

## Workflow

1. **Ask questions one at a time** — never batch multiple questions into a single message.
2. **Provide your recommended answer** with each question so the user can accept, reject, or refine it.
3. **If a question can be answered by exploring the codebase**, explore the codebase instead of asking the user.
4. **Resolve dependencies first** — if a later decision depends on an earlier one, walk the earlier branch to completion before moving on.
5. **Track progress** — mentally map the decision tree and mark branches as resolved.
6. **Offer "Accept All Recommendations"** — before starting the interview, give the user the option to accept all your recommendations at once. If chosen, walk through every branch, apply your recommended answer for each, and produce the final decision log without stopping for individual answers.
7. **Wrap up** — once all branches are resolved, summarize the shared understanding as a concise decision log.

## Opening Message

Before the first question, present the user with these options:

```
Before we begin, how would you like to proceed?

1. **Question by question** — I'll ask one at a time and you decide on each.
2. **Accept all recommendations** — I'll walk every branch using my recommended answers and deliver the full decision log at the end.
3. **Cherry-pick** — I'll list all my questions and recommendations upfront, you select which ones to accept and which to discuss further.
```

Wait for the user to choose before proceeding.

## Question Format

For each question use this structure:

```
**[Branch / Topic]**

Question: [Your specific question]

My recommendation: [Your suggested answer and why]
```

## Rules

- One question per message, no exceptions (unless the user chose "Accept all recommendations" or "Cherry-pick" mode).
- Don't accept vague answers — push for specifics.
- If the user's answer contradicts an earlier decision, flag the conflict and resolve it.
- Keep going until every branch is covered. Don't stop early.
- In **Accept all recommendations** mode, proceed through every branch using your recommendations without pausing, then present the complete decision log.
- In **Cherry-pick** mode, list all questions and recommendations first, let the user mark which to accept and which to discuss, then only interview on the unresolved ones.
