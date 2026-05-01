---
name: build-app
description: Pre-flight check before building an app from a tech spec. Analyzes the spec for anything that would require user intervention during the build — long-running commands, ambiguous requirements, missing configs, environment setup, or high-risk operations. Use when user says "build this", "build the app", "implement this spec", "start building", or "build-app".
---

# Build App — Pre-flight & Build

Analyze a tech spec (or PRD) before building to surface every point where the build would stall waiting for user input. Then execute the build autonomously.

## When to use

When the user wants to build an app from a spec and wants to go AFK while you work. Always run the pre-flight check first, even if the user doesn't explicitly ask for it.

## Process

### 1. Locate the spec

Find the tech spec or PRD. Check, in order:

- File the user referenced
- `TECH-SPEC.md` in the project root or nearest subfolder
- `PRD.md` as fallback
- Ask the user if nothing is found

### 2. Pre-flight scan

Read the full spec and flag every item that falls into these categories:

#### a. Environment & tooling

- Global CLI tools that need installing (e.g., `aws-cdk`, `firebase-tools`)
- Runtime versions required (Node 20, Python 3.12, etc.)
- Package managers assumed (pnpm vs npm vs yarn)
- Docker or containerized services needed locally
- Environment variables or `.env` files that must exist before build

#### b. External services & credentials

- API keys, secrets, or tokens the app needs at build or runtime
- Third-party services that need accounts (Stripe, Supabase, Auth0, etc.)
- Databases or message queues that must be running locally

#### c. Long-running processes

- Dev servers the user must start in their own terminal
- Watch-mode commands (webpack --watch, tsc --watch)
- Background services (Docker containers, local DBs)

#### d. Ambiguous or missing requirements

- Features described vaguely ("handle edge cases", "nice UX")
- Decisions the spec defers ("TBD", "to be decided")
- Conflicting requirements
- Missing acceptance criteria

#### e. High-risk operations

- Production config changes
- Data migrations or destructive DB operations
- Infrastructure provisioning (cloud resources, DNS)
- Operations that cost money

#### f. Platform-specific concerns

- OS-specific commands or paths
- Native dependencies that need compilation
- Permissions or admin access required

### 3. Collect all commands

Scan the spec and your planned implementation to build a complete list of every shell command you will need to run during the build. For each command, determine:

- **The exact command** (e.g., `npm install`, `npx prisma generate`, `npm run build`)
- **Why it's needed** (dependency install, code generation, compilation, etc.)
- **Whether it needs user approval** — commands that Kiro would normally pause on for confirmation (installs, builds, scaffolding CLIs, code generators, etc.)

Group commands into:

- **Trusted commands** — commands the user should add to their trusted/auto-approved list so the build runs without interruption
- **Manual commands** — commands the user must run themselves (dev servers, watch mode, anything long-running)

### 4. Report

Present findings as a checklist grouped by category. For each item:

- State what's needed
- State when during the build it will be needed (before start, mid-build, at the end for testing)
- Suggest a resolution if possible (e.g., "I'll use npm since no lockfile exists")

If there are items the user must resolve before you start, list those separately as **blockers**. Items you can handle or work around go under **handled**.

Example format:

```
## Pre-flight Report

### Commands I'll need to run
Add these to your trusted command list so I can run them without interruption:

| # | Command | Purpose |
|---|---------|---------|
| 1 | `npm install` | Install dependencies |
| 2 | `npx prisma generate` | Generate Prisma client |
| 3 | `npx prisma db push` | Sync database schema |
| 4 | `npm run build` | Compile TypeScript |
| 5 | `npm run test` | Verify implementation |

### Commands you'll need to run yourself
These are long-running or interactive — run them in your own terminal:

| Command | When |
|---------|------|
| `npm run dev` | After build, to test locally |
| `docker compose up -d` | Before build, if using containerized DB |

### Blockers (need your input before I start)
- [ ] `.env` file needed with DATABASE_URL — I can't generate this for you
- [ ] Stripe API key required for payment module

### Handled (I'll take care of these)
- [x] Will use npm (no lockfile detected)
- [x] Will scaffold SQLite for local dev instead of Postgres

### Heads-up (needed later, not blocking)
- [ ] Deployment section requires AWS credentials — skipping for now

### Ambiguities (I made a call, override if you disagree)
- Spec says "authentication" but doesn't specify provider — I'll use JWT with local strategy
```

### 5. Wait or proceed

- If there are **blockers**, stop and wait for the user to resolve them.
- If there are **no blockers**, tell the user "No blockers — starting the build. Add the commands above to your trusted list and I'll proceed." and wait briefly for them to do so, then proceed.

### 6. Build

Execute the implementation following the tech spec. Work through it systematically:

1. Scaffold project structure
2. Install dependencies
3. Implement features in dependency order
4. Run build/compile to verify
5. Run tests if they exist or are specified
6. Report completion with a summary of what was built and any remaining manual steps

## Rules

- Always run the pre-flight scan, even for simple projects. A 10-second check saves a 10-minute stall.
- Never guess at secrets or credentials. Always flag them.
- If the spec is missing, don't build from vibes. Ask for a spec or offer to generate one.
- Be honest about what you can't do (run dev servers, open browsers, provision cloud resources).
- If you hit an unexpected blocker mid-build, stop and report it clearly rather than working around it silently.
