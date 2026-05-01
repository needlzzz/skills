# Tech Spec Template

Use this template when producing the technical specification. Fill every section. If a section doesn't apply, write "N/A" with a one-line reason.

---

```markdown
# Tech Spec: [Project Name]

## Overview

[2-3 sentences. What is this, who is it for, what problem does it solve.]

## Tech Stack

| Layer        | Choice         | Reason                  |
|--------------|----------------|-------------------------|
| Language     | e.g. TypeScript | [why]                  |
| Framework    | e.g. Next.js    | [why]                  |
| Database     | e.g. PostgreSQL | [why]                  |
| Auth         | e.g. Clerk      | [why]                  |
| Hosting      | e.g. Vercel     | [why]                  |
| Styling      | e.g. Tailwind   | [why]                  |

[Add or remove rows as needed. If the project has an existing stack, document it and note what's new.]

## Project Structure

[Show the target file/folder layout. Be specific — an AI agent will create these.]

```
project-root/
├── src/
│   ├── components/
│   ├── pages/
│   ├── lib/
│   ├── types/
│   └── ...
├── package.json
└── ...
```

## Data Model

[Define every entity, its fields, types, and relationships. Use a table or schema notation.]

### [Entity Name]

| Field       | Type     | Required | Notes              |
|-------------|----------|----------|--------------------|
| id          | uuid     | yes      | Primary key        |
| ...         | ...      | ...      | ...                |

[Repeat for each entity. Include relationships: "User has many Posts".]

## API / Routes

[List every endpoint or page route the system needs.]

### `[METHOD] /path`

- **Purpose:** [what it does]
- **Request body:** `{ field: type }`
- **Response:** `{ field: type }`
- **Auth:** [required / public]
- **Errors:** [list error cases and codes]

[For frontend-only projects, list page routes and what they render.]

## Features & Acceptance Criteria

### Feature 1: [Name]

**Description:** [What it does in concrete terms]

**Acceptance criteria:**
- [ ] [Specific, testable condition]
- [ ] [Another condition]
- [ ] [Edge case handling]

### Feature 2: [Name]

[Repeat for each feature.]

## UI / UX Specifications

[Describe screens, layouts, and interactions. Reference wireframes if they exist. Be specific about:]

- Page layout and component hierarchy
- User flow (step 1 → step 2 → ...)
- Loading, empty, and error states
- Responsive behavior

[If no UI, write "N/A — headless / CLI / API only".]

## Environment & Configuration

[List every env variable, config file, or secret the project needs.]

| Variable          | Purpose                | Example Value     |
|-------------------|------------------------|-------------------|
| DATABASE_URL      | DB connection string   | postgres://...    |
| API_KEY           | Third-party service    | sk-...            |

## Implementation Order

[Ordered list of what to build first. Each step should be independently verifiable.]

1. **[Step name]** — [what to build and how to verify it works]
2. **[Step name]** — [what to build and how to verify it works]
3. ...

## Open Questions

[Anything from the conversation that wasn't resolved but matters for implementation.]

- [ ] [Question 1]
- [ ] [Question 2]

[If none, write "None — all decisions resolved."]
```
