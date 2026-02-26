# CLAUDE.md

This file provides guidance to Claude Code when working with this plugin.

## Project Overview

neldivad-skills is a Claude Code plugin for bootstrapping and building SaaS applications. It provides a blueprint-driven workflow where architecture decisions are documented before code is written.

## Architecture

Skills are organized in `skills/` with `neldivad-` prefix:

```
skills/
├── neldivad-blueprint-instantiator/   # Create new SaaS projects from templates
│   ├── SKILL.md
│   └── references/
│       └── saas-blueprint/            # Template .md files (Phase 0-3)
```

## Operating Mode

| Rule | Description |
|------|-------------|
| **Blueprint before code** | Never write code without approved blueprint docs |
| **CTO pushback** | Challenge bad ideas, force MVP minimalism |
| **Save files first** | Update .md docs before code, never the reverse |
| **Phase gates** | Human approves each phase before proceeding |
| **Sync rule** | When one 02-*.md changes, check all others for consistency |

## Required External Skills

These skills are not bundled — install them separately:

| Skill | Source | Purpose |
|-------|--------|---------|
| `find-skills` | `vercel-labs/skills@find-skills` | Discover domain-specific skills after stack is chosen |
| `skill-creator` | `anthropics/skills@skill-creator` | Create custom project-specific skills |

Install with:
```bash
npx skills add vercel-labs/skills@find-skills -g
npx skills add anthropics/skills@skill-creator -g
```

## Workflow

1. `/neldivad-blueprint-instantiator <project-name>` — creates project, runs Q&A, fills templates
2. Human reviews blueprint, approves at each phase gate
3. `find-skills` discovers stack-specific skills based on `02-stack.md` decisions
4. Install discovered skills into project `.claude/skills/`
5. Start building with both the "what" (blueprint) and the "how" (skills)

## Adding New Skills

- All skills MUST use `neldivad-` prefix
- Follow [Skill authoring best practices](https://platform.claude.com/docs/en/agents-and-tools/agent-skills/best-practices)
- SKILL.md under 500 lines, use references/ for detail
- Description in third person, include what + when triggers
