# Milestones
<!-- version: 0.1 | phase: 3 | last-updated: YYYY-MM-DD -->
<!-- changelog:
  v0.1 - Initial milestone plan from Phase 3
-->

<!--
  INSTRUCTIONS FOR AI:
  This is the game route. You propose milestones, human approves.
  Each milestone must:
  1. Have clear dependencies (what must be done first)
  2. Have a "done" definition (how do we know it's complete)
  3. Have a test checkpoint (what tests prove it works)
  4. Estimate which 02-*.md files it implements

  After completing a milestone, update its status and log learnings.
  At each Review Gate, present this document with progress.
-->

## Milestone Route Map

```
M0: Project Setup ─────► M1: Auth ─────► M2: Core CRUD ─────► M3: Payments ─────► M4: Polish ─────► LAUNCH
     (tutorial)           (unlock)         (main quest)          (boss fight)        (side quests)
```

## M0: Project Scaffold (Tutorial Zone)

**Dependencies:** All Phase 2 documents approved
**Implements:** 02-file-tree.md, 02-stack.md

| Task | Status | Notes |
|---|---|---|
| Initialize {{FRAMEWORK}} project | | |
| Install all packages from 02-stack.md | | |
| Set up {{DB_ORM}} with {{DB_PROVIDER}} | | |
| Create initial schema from 02-schema.md | | |
| Run first migration | | |
| Set up test framework from 02-test-strategy.md | | |
| Generate .cursorrules from 03-cursorrules.md | | |
| Generate CLAUDE.md from 03-claude-md.md | | |
| Create .env.example with all required variables | | |
| Verify: `npm run dev` works, `npm run test` works | | |

**Done when:** App runs locally, tests pass, DB connected, all env vars documented.

**Review Gate:** Present scaffold to human. Verify file tree matches 02-file-tree.md.

---

## M1: Authentication (Unlock Basic Access)

**Dependencies:** M0 complete
**Implements:** 02-auth-flow.md

| Task | Status | Notes |
|---|---|---|
| Set up {{AUTH_PROVIDER}} | | |
| Create sign-up page | | |
| Create sign-in page | | |
| Add auth middleware | | |
| Create local User table + sync with {{AUTH_PROVIDER}} | | |
| Protect /dashboard routes | | |
| Test: sign up → dashboard accessible | | |
| Test: unauthenticated → redirected to /sign-in | | |

**Done when:** User can sign up, sign in, sign out. Dashboard is protected.

**Review Gate:** Demo auth flow. Check 02-auth-flow.md for completeness.

---

## M2: Core CRUD (Main Quest)

**Dependencies:** M1 complete
**Implements:** 02-api-routes.md, 02-schema.md, 02-pages-and-components.md

| Task | Status | Notes |
|---|---|---|
| Create {{PRIMARY_ENTITY}} model in DB | | |
| Build server actions: create, read, update, delete | | |
| Build list page with data table | | |
| Build detail page | | |
| Build create/edit form | | |
| Add delete with confirmation | | |
| Test: full CRUD cycle works | | |
| Test: user can only see own {{PRIMARY_ENTITY}} | | |

**Done when:** User can create, view, edit, delete {{PRIMARY_ENTITY}}. Data is scoped to user.

**Review Gate:** Demo CRUD flow. This is the core product — get human feedback on UX.

---

## M3: Payments (Boss Fight)

**Dependencies:** M2 complete
**Implements:** 02-payment-flow.md

| Task | Status | Notes |
|---|---|---|
| Set up {{PAYMENT_PROVIDER}} account + products | | |
| Create checkout session endpoint | | |
| Build pricing page | | |
| Set up webhook endpoint | | |
| Handle checkout.session.completed | | |
| Handle subscription.updated / deleted | | |
| Build billing dashboard page | | |
| Add plan-based feature gating | | |
| Test: full purchase flow with test card | | |
| Test: webhook handles all events from 02-payment-flow.md | | |
| Test: downgrade restricts access correctly | | |

**Done when:** User can subscribe, upgrade, downgrade, cancel. Access is gated by plan.

**Review Gate:** Demo payment flow end-to-end. Review 02-risk-registry.md payment risks.

---

## M4: Polish & Launch Prep (Side Quests)

**Dependencies:** M3 complete

| Task | Status | Notes |
|---|---|---|
| Build landing page | | |
| Add error handling for all edge cases | | |
| Add loading states and empty states | | |
| Mobile responsiveness (if in MVP scope) | | |
| SEO basics (meta tags, OG images) | | |
| Set up production environment on {{HOSTING}} | | |
| Configure production env vars | | |
| Run full E2E test suite | | |
| Test Stripe webhooks in production mode | | |
| Set up error monitoring (optional) | | |

**Done when:** App deployed to production. All smoke tests pass on production URL.

**Review Gate:** Final review before "launch." Walk through 02-risk-registry.md one last time.

---

## Post-Launch Milestones (New Game+)

<!--
  AI INSTRUCTION: Pull from 01-prd.md "Explicitly Out of Scope" and
  01-mvp-reduction-checklist.md "Cut Features" to plan post-launch milestones.
-->

### M5: Post-MVP Features

| Feature | Priority | Dependencies |
|---|---|---|
| (from cut features list) | | |
| | | |
| | | |

---

## Milestone Status Tracker

| Milestone | Status | Started | Completed | Learnings |
|---|---|---|---|---|
| M0: Scaffold | not started | | | |
| M1: Auth | not started | | | |
| M2: Core CRUD | not started | | | |
| M3: Payments | not started | | | |
| M4: Polish | not started | | | |
