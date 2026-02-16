---
name: neldivad-blueprint-instantiator
description: Bootstraps a new SaaS project from blueprint templates. Runs phased Q&A to extract the idea, fills architecture docs, discovers stack-specific skills, and prepares the project for building. Use when user says "new project", "start a SaaS", "instantiate blueprint", or "bootstrap <name>".
disable-model-invocation: true
---

# Blueprint Instantiator

Create a new SaaS project from blueprint templates with phased architecture planning.

## Usage

```bash
/neldivad-blueprint-instantiator <project-name>
```

## What This Produces

```
<project-name>/
  blueprint/                  # The "what" — filled-in architecture docs
    00-variables.md           # Master variable registry (filled)
    00-state.md               # Session state / save file
    00-game-rules.md          # AI operating mode
    01-prd.md                 # Product requirements (filled)
    01-mvp-reduction-checklist.md
    02-stack.md               # Stack decisions (filled)
    02-schema.md              # Database schema (filled)
    02-auth-flow.md           # Auth architecture (filled)
    02-payment-flow.md        # Payment architecture (filled)
    02-api-routes.md          # API design (filled)
    02-file-tree.md           # Project structure (filled)
    02-pages-and-components.md
    02-risk-registry.md
    02-test-strategy.md
    03-milestones.md          # Build plan (filled)
    03-cursorrules.md         # Generated Cursor rules
    03-claude-md.md           # Generated CLAUDE.md for the project
    saves/                    # Phase gate snapshots
  .claude/
    skills/                   # Stack-specific skills (installed in Phase 2)
  src/                        # Empty until blueprint approved
```

## Workflow

### Phase 0: Setup

1. Create the project directory structure above
2. Copy all templates from [references/saas-blueprint/](references/saas-blueprint/) into `<project-name>/blueprint/`
3. Create empty `saves/` directory
4. Update `00-state.md` with the project path and current position
5. Verify required external skills are installed:
   - `find-skills` (from vercel-labs/skills)
   - If missing, prompt user to install: `npx skills add vercel-labs/skills@find-skills -g -y`

### Phase 1: Extract the Idea (Tutorial)

1. Read [references/saas-blueprint/01-qna-script.md](references/saas-blueprint/01-qna-script.md)
2. Run the Q&A script with the user — ask questions one at a time
3. After Q&A, populate `00-variables.md` with all extracted values
4. Generate `01-prd.md` from the answers
5. Run `01-mvp-reduction-checklist.md` — challenge every feature:
   - Does MVP need realtime? Background jobs? Caching? Admin panel? File uploads?
   - Default answer is NO unless user justifies it
6. **GATE 1**: Present summary to user. Wait for explicit approval before Phase 2
7. Save snapshot to `saves/gate-1-idea-approved.md`
8. Update `00-state.md`

### Phase 2: Architecture (World Map)

1. Fill `02-stack.md` — for every choice, document what, why, and what was rejected
2. Fill `02-schema.md` — database tables, relationships, indexes
3. Fill `02-auth-flow.md` — auth strategy, session handling, protected routes
4. Fill `02-payment-flow.md` — billing model, webhook handling, subscription states
5. Fill `02-api-routes.md` — every endpoint with method, auth, request/response
6. Fill `02-file-tree.md` — complete project structure
7. Fill `02-pages-and-components.md` — every page and component
8. Fill `02-risk-registry.md` — predict failure modes and mitigations
9. Fill `02-test-strategy.md` — what to test and how
10. **SYNC CHECK**: Read all 02-*.md files. Flag any inconsistencies.
11. **GATE 2**: Present architecture to user. Wait for explicit approval.
12. Save snapshot to `saves/gate-2-architecture-approved.md`
13. Update `00-state.md`

### Phase 2.5: Discover and Install Skills

Based on decisions in `02-stack.md`, use `find-skills` to search for relevant skills:

1. Read `02-stack.md` for framework, styling, hosting, DB, auth, payments choices
2. For each major stack choice, run skill search:
   - Framework (e.g., "nextjs best practices", "react performance")
   - Hosting (e.g., "vercel deployment")
   - Database (e.g., "supabase", "prisma")
   - Auth (e.g., "clerk auth", "nextauth")
3. Present found skills to user with install counts and descriptions
4. Only recommend skills with 100+ installs or from verified sources (vercel-labs, anthropics)
5. User approves which to install
6. Install approved skills: `npx skills add <owner/repo@skill> -g -y`
7. Update `00-state.md` with installed skills list

### Phase 3: Build Plan (Gameplay)

1. Fill `03-milestones.md` — break into 1-2 week milestones
2. Generate `03-cursorrules.md` — Cursor IDE rules based on stack
3. Generate `03-claude-md.md` — project-level CLAUDE.md based on stack and architecture
4. **GATE 3**: Present build plan. Wait for approval.
5. Save snapshot to `saves/gate-3-plan-approved.md`
6. Update `00-state.md` — mark ready to build

### Post-Blueprint: Start Building

Only after Gate 3 approval:
1. Move `03-claude-md.md` content to `<project-name>/.claude/CLAUDE.md`
2. Create `src/` directory
3. Begin Milestone 1 from `03-milestones.md`

## Template Reference

All templates are in [references/saas-blueprint/](references/saas-blueprint/):

| File | Phase | Purpose |
|------|-------|---------|
| [00-variables.md](references/saas-blueprint/00-variables.md) | 0 | Master variable registry |
| [00-game-rules.md](references/saas-blueprint/00-game-rules.md) | 0 | AI operating mode |
| [00-state.md](references/saas-blueprint/00-state.md) | 0 | Session state save file |
| [00-readme.md](references/saas-blueprint/00-readme.md) | 0 | File map and navigation |
| [01-qna-script.md](references/saas-blueprint/01-qna-script.md) | 1 | Q&A extraction script |
| [01-prd.md](references/saas-blueprint/01-prd.md) | 1 | Product requirements doc |
| [01-mvp-reduction-checklist.md](references/saas-blueprint/01-mvp-reduction-checklist.md) | 1 | Feature cut checklist |
| [02-stack.md](references/saas-blueprint/02-stack.md) | 2 | Stack decisions |
| [02-schema.md](references/saas-blueprint/02-schema.md) | 2 | Database schema |
| [02-auth-flow.md](references/saas-blueprint/02-auth-flow.md) | 2 | Auth architecture |
| [02-payment-flow.md](references/saas-blueprint/02-payment-flow.md) | 2 | Payment flow |
| [02-api-routes.md](references/saas-blueprint/02-api-routes.md) | 2 | API routes |
| [02-file-tree.md](references/saas-blueprint/02-file-tree.md) | 2 | File structure |
| [02-pages-and-components.md](references/saas-blueprint/02-pages-and-components.md) | 2 | Pages and components |
| [02-risk-registry.md](references/saas-blueprint/02-risk-registry.md) | 2 | Risk predictions |
| [02-test-strategy.md](references/saas-blueprint/02-test-strategy.md) | 2 | Test plan |
| [03-milestones.md](references/saas-blueprint/03-milestones.md) | 3 | Build milestones |
| [03-cursorrules.md](references/saas-blueprint/03-cursorrules.md) | 3 | Generated Cursor rules |
| [03-claude-md.md](references/saas-blueprint/03-claude-md.md) | 3 | Generated CLAUDE.md |

## Important Rules

- **Never skip a gate.** Each phase requires human approval.
- **Never write code during blueprint phases.** Docs first.
- **CTO pushback mode.** Challenge scope creep, default to NO on nice-to-haves.
- **Sync check.** When any 02-*.md changes, verify all others are consistent.
- **Variables.** All `{{PLACEHOLDERS}}` in templates must resolve from `00-variables.md`.
