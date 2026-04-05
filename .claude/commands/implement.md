You are implementing micro-SaaS MVPs for Jobelo. This command builds products from the idea leaderboard, one iteration at a time, designed to work with `/loop`.

## Arguments
- `$ARGUMENTS` — expects `--ideas N` where N is how many top ideas to build (default: 3). Can also pass `--idea <name>` to target a specific idea.

## CONSTRAINTS
- NO Web3 security products (day job conflict at Webacy)
- Global market, English-first
- Async-only, no calls
- Each MVP must ship in 1-4 weeks
- Landing page ships WITH the MVP (not after)

## TECH STACK (mandatory — do not deviate)

### Frontend
- **Next.js** (App Router) — all web UIs and landing pages
- **React** with **TypeScript**
- **Tailwind CSS** for styling
- **shadcn/ui** for component library (install via `npx shadcn@latest init`)
- Deploy to **Vercel**

### Backend
- **NestJS** with **TypeScript** — all API services
- **Prisma** as ORM
- **PostgreSQL** as database (use Neon, Supabase, or AWS RDS)
- Deploy to **Railway**, **Fly.io**, or **AWS** (via CDK)

### Payments
- **Stripe** — Checkout for subscriptions, webhooks for lifecycle events, Customer Portal for self-serve management
- Use `stripe` npm package in NestJS backend
- Pricing tiers defined in Stripe Dashboard, referenced by price IDs in code

### Infrastructure (when needed)
- **AWS CDK** (TypeScript) for any infrastructure beyond Vercel/Railway (queues, cron jobs, custom workers, etc.)
- Keep infra minimal for MVP — prefer managed services over self-hosted

### Project Structure (per idea — inside projects/)
```
projects/<project>/
├── apps/
│   ├── web/          # Next.js frontend (landing + app)
│   └── api/          # NestJS backend
├── packages/         # Shared types, utils (only if needed)
├── infra/            # AWS CDK stacks (only if needed)
├── docs/
│   ├── plan.md
│   └── audit-log.md
├── CLAUDE.md
├── README.md
├── package.json      # Workspace root (pnpm workspaces)
└── .env.example
```

### Stack Rules
- **Monorepo per idea** using pnpm workspaces (consistent with Plata pattern)
- **No Python backends** — use NestJS even for developer tools (keep stack uniform)
- Python is OK for one-off scripts, data processing, or CLI tools that don't need a web API
- **No Supabase Auth or Firebase Auth** — use NextAuth.js (Auth.js) in the Next.js app or a custom JWT flow in NestJS
- **No ORMs other than Prisma** — no TypeORM, Drizzle, Knex, etc.
- **No CSS frameworks other than Tailwind** — no MUI, Chakra, Ant Design, etc.
- **No component libraries other than shadcn/ui** — no Radix directly, no Headless UI (shadcn wraps Radix already)

---

## TRACKING FILES (read + update EVERY iteration — this is non-negotiable)

### Master tracker:
- `research/implementation/TRACKER.md` — implementation progress across all ideas (create if missing)
- `research/reports/2026-04-04-idea-leaderboard.md` — source of truth for which ideas to build

### Per-idea tracking (inside each project folder):
- `projects/<project>/CLAUDE.md` — project context, architecture decisions, what NOT to do
- `projects/<project>/docs/plan.md` — implementation plan with phases and checkable deliverables
- `projects/<project>/docs/audit-log.md` — iteration-by-iteration audit trail (THE critical file for loop continuity)
- `projects/<project>/README.md` — project overview, setup, status

---

## LOOP EXECUTION MODEL

This command is designed for `/loop 30m /implement --ideas 3`. Each invocation is ONE iteration. The loop runs every 30 minutes. **You have NO memory of previous iterations** — the tracking files ARE your memory.

### Iteration lifecycle (every single run):
```
READ STATE → DETECT ITERATION # → PICK ONE IDEA → BUILD OR PLAN → AUDIT → UPDATE ALL TRACKING → DONE
```

### How to determine iteration number:
1. Read `research/implementation/TRACKER.md` — check "Last iteration" column
2. Read the active idea's `docs/audit-log.md` — count existing `## Iteration N` headers
3. Next iteration = max(existing) + 1
4. If no audit-log exists, this is iteration 1

### Scope per iteration:
- **Focus on ONE idea per loop cycle** (not all N). Pick the one that needs the most attention.
- **One meaningful deliverable per cycle.** Examples: "NestJS project scaffolded with Prisma + first migration", "changelog crawler service working for 3 APIs", "landing page hero + pricing section done". NOT "scaffolded 3 projects" or "planned all ideas."
- **If the last iteration left something broken, fix it FIRST** before new work. Read the audit-log's "Blockers" section from the previous iteration.

### Idea rotation strategy:
- Default: round-robin (idea 1, then 2, then 3, then 1 again...)
- Exception: if an idea has a blocker, skip it and note in TRACKER.md
- Exception: if an idea is close to MVP_COMPLETE (6+ of 10 checklist items done), focus on it until done
- **Never let any idea stall for 3+ consecutive skips** — address the blocker or kill the idea

---

## STEP 0: READ STATE (mandatory, every iteration)

**You MUST read these files before doing ANYTHING else:**

1. `research/implementation/TRACKER.md` — current status of all ideas, which iteration each is on, blockers
   - **If this file does not exist**, create it using the format in the TRACKER.md FORMAT section below, seeded from the leaderboard's top N ideas.
2. The active idea's `docs/audit-log.md` (if it exists) — what was done last time, what's next, what's broken
   - **If this file does not exist**, this idea needs planning (Step 1).
3. The active idea's `docs/plan.md` (if it exists) — what phase we're in, what's the next deliverable
   - **If this file does not exist**, this idea needs planning (Step 1).

**Based on the read, decide:**
- Which idea to work on this iteration (round-robin by "Last Iteration" column — pick the idea with the oldest/no date)
- The global iteration number (count ALL `## Iteration N` entries across ALL audit-logs, take max + 1)
- Whether there are blockers from last iteration to fix first
- What the SINGLE deliverable for this iteration should be

---

## AVAILABLE SKILLS (invoke via the Skill tool)

You have access to specialized skills that produce higher-quality output than doing it manually. **But skills are heavy — max ONE skill invocation per loop iteration.** Pick the one that adds the most value for the current deliverable.

### CRITICAL RULE: One skill per iteration
Each skill is a full analysis/generation pass. Invoking 2+ skills in a 30-min loop cycle will eat all the time and produce no actual code. **Pick the single most impactful skill for the deliverable you're building, invoke it, apply its output, then move on.**

### Skill → Deliverable mapping (use ONLY when building that specific thing):

| When you're building... | Invoke this skill | Why |
|------------------------|-------------------|-----|
| Landing page | **`landing-page-generator`** | Generates complete Next.js/TSX + Tailwind. ALWAYS use this — never hand-write landing pages from scratch. |
| Landing page copy (after generator) | **`copywriting`** | Sharpen hero, features, CTA copy. Use in a SEPARATE iteration from the generator. |
| App dashboard / core UI pages | **`frontend-design`** | Production-grade interfaces with shadcn components. |
| Stripe pricing tiers + pricing page | **`pricing-strategy`** | Tier structure, value metrics, pricing page layout. |
| Auth / signup flow | **`signup-flow-cro`** | Minimize registration friction. |
| Stripe upgrade / paywall flow | **`paywall-upgrade-cro`** | Optimize conversion from free to paid. |
| AI feature (e.g., changelog classification) | **`claude-api`** | Correct Anthropic SDK patterns, tool use, structured output. |
| Data entry forms (e.g., freight load entry) | **`form-cro`** | Optimize non-signup forms for completion rate. |
| Competitor positioning (planning phase) | **`competitive-teardown`** | Feature matrix + positioning insights for the 1-2 closest competitors. |

### Pre-launch quality gates (one per iteration, run sequentially across iterations):

When MVP checklist reaches 9/10 or 10/10, run these as **separate iterations** — one gate per cycle:

| Gate | Skill | What it checks |
|------|-------|---------------|
| 1 | **`page-cro`** | Landing page conversion optimization |
| 2 | **`seo-audit`** | Meta tags, structured data, performance |
| 3 | **`a11y-audit`** | WCAG Level A/AA violations |
| 4 | **`webapp-testing`** | Playwright smoke tests against running app |
| 5 | **`simplify`** | Code quality review — reuse, efficiency, dead code |

### Post-MVP (run once after MVP_COMPLETE):

| Skill | Purpose |
|-------|---------|
| **`launch-strategy`** | Product Hunt, communities, distribution plan |
| **`social-content`** | LinkedIn/Twitter launch posts |
| **`onboarding-cro`** | Optimize first-run experience (after core flow works) |

### Skills NOT to use for these projects:
`brand-guidelines`, `algorithmic-art`, `canvas-design`, `i18n-expert`, `app-store-optimization`, `skill-creator`, `doc-coauthoring`, `theme-factory`, `deep-research`, `product-analysis`, `product-discovery`, `prompt-optimizer`, `ux-researcher-designer`, `experiment-designer`, `ui-design-system`, `ui-designer`

### Tracking:
In the audit-log, note: `Skills used: [skill-name]` or `Skills used: none`. This prevents re-running skills that were already applied.

---

## STEP 1: PLAN (first iteration for a given idea only)

**Trigger:** The idea has no project folder, OR has a folder but no `docs/plan.md`.

1. **Create the project folder** inside `projects/` (e.g., `projects/driftwatch/`, `projects/freight-tms/`)
2. **Research the tech approach** — what APIs/data sources? What's the minimum viable feature?
   - **Invoke `competitive-teardown` skill** on the 1-2 closest competitors to inform positioning (this is the ONE skill for the planning iteration)
3. **Scaffold the monorepo** (structure only — NO `pnpm install` or dependency installation in this step):
   - Run `pnpm init` at the project root
   - Create directory structure: `apps/web/`, `apps/api/`, `packages/`, `docs/`
   - Write root `package.json` with pnpm workspaces config pointing to `apps/*` and `packages/*`
   - Write `apps/web/package.json` (Next.js deps listed but NOT installed)
   - Write `apps/api/package.json` (NestJS deps listed but NOT installed)
   - Write `pnpm-workspace.yaml`
   - Write `.env.example` with placeholder vars
   - **The actual `pnpm install` and app scaffolding (`npx create-next-app`, `nest new`) happen in the FIRST build iteration (Step 2), not during planning**
4. **Write `docs/plan.md`**:
   - Phase 1: Core feature (week 1-2) — the ONE thing that proves value
   - Phase 2: Landing page + auth + billing (week 2-3)
   - Phase 3: Polish + deploy + launch prep (week 3-4)
   - Each phase: specific checkable deliverables (files, endpoints, pages — not vague goals)
   - Include "kill criteria" — specific conditions that mean this idea should be abandoned
5. **Write `CLAUDE.md`** for the project:
   - What the product does (1 paragraph)
   - Tech stack decisions (reference the mandatory stack above)
   - Key constraints and what NOT to build
   - How to run locally (will be filled in as infra is set up)
6. **Write `README.md`** with project overview
7. **Write first entry in `docs/audit-log.md`**:
   ```markdown
   ## Iteration 1 — YYYY-MM-DD
   ### What was done
   - Project scaffolded, plan written, CLAUDE.md created
   ### What works now
   - Nothing yet — planning phase
   ### What's next
   - [First Phase 1 deliverable from plan.md]
   ### Blockers
   - None
   ```
8. **Update `research/implementation/TRACKER.md`**: status → `PLANNING`, last iteration → today + iter 1
9. **STOP.** Do NOT write application code in the planning iteration. Plan first, build next.

### Special handling: Acquisition Play
If one of the top N ideas is an acquisition play (not a build):
- Create a `docs/acquisition-targets.md` instead of scaffolding code
- Each iteration: research 1-2 potential targets (search MicroAcquire, Flippa, Chrome Web Store for underperforming extensions, Indie Hackers "for sale" posts)
- Track in TRACKER.md with status `SCOUTING`
- When a target is found: status → `DUE_DILIGENCE`, then `ACQUIRED` or `PASSED`

---

## STEP 2: BUILD (all iterations after planning)

1. Read `docs/plan.md` — identify the next unchecked deliverable in the current phase
2. Read `docs/audit-log.md` — check last iteration's "What's next" and "Blockers"
3. **If there are blockers from last iteration → fix them first**, then proceed to new work if time permits
4. **Write working code for ONE deliverable.** Check the skill→deliverable table above — if the deliverable has a matching skill, invoke it (max ONE per iteration):
   - "Set up NestJS app with Prisma, write schema for core models, run first migration" → no skill needed
   - "Build the changelog crawler service" → no skill needed (or `claude-api` if using Anthropic SDK)
   - "Create the dashboard page" → invoke `frontend-design`
   - "Build the landing page" → invoke `landing-page-generator` (copywriting is a separate iteration)
   - "Design Stripe pricing tiers" → invoke `pricing-strategy`
   - "Build auth/signup flow" → invoke `signup-flow-cro`
   - "Build Stripe upgrade flow" → invoke `paywall-upgrade-cro`
   - "Build data entry form" → invoke `form-cro`
5. **Verify it works:**
   - Run `pnpm build` in the affected app — fix any TypeScript/build errors
   - Run `pnpm dev` and manually verify the feature works
   - Run `npx prisma migrate dev` if schema changed — confirm it applies cleanly
6. **Mark the deliverable as done** in `docs/plan.md` (change `- [ ]` to `- [x]`)

---

## STEP 3: AUDIT (every iteration, after building)

After writing code, answer these questions in the audit-log:

1. **Does it build?** Run `pnpm build` in apps/web and apps/api. Record pass/fail.
2. **Does the feature work?** Not "is the code there" but "if I click the button / call the endpoint, does it DO the thing?"
3. **Security scan:**
   - Any hardcoded secrets? (search for API keys, passwords, tokens in code)
   - `.env.example` up to date with all required vars?
   - Input validation on API endpoints?
   - Auth checks on protected routes?
4. **If landing page exists:** Would a stranger understand what this does and want to sign up?
5. **Gap to MVP:** Count checklist items done vs remaining (X/10).

---

## STEP 4: UPDATE TRACKING (every iteration, non-negotiable)

Write ALL of the following before ending the iteration:

### A) `docs/audit-log.md` — append new entry:
```markdown
## Iteration N — YYYY-MM-DD
### What was done
- [specific changes: files created/modified, features built, bugs fixed]
### What works now
- [list of features that are functional end-to-end]
### Audit results
- Build: PASS/FAIL (apps/web: ✓/✗, apps/api: ✓/✗)
- Feature works: YES/NO — [details]
- Security: [any issues found]
- MVP checklist: X/10 complete
### What's next
- [THE single next deliverable — be specific]
### Blockers
- [anything preventing progress, or "None"]
```

### B) `docs/plan.md` — check off completed deliverables

### C) `research/implementation/TRACKER.md` — update the row for this idea:
- Status column: current status
- Phase column: current phase
- Last Iteration column: today's date + iteration number
- Blockers column: current blockers or "None"

### D) Check for MVP completion:
Count against this checklist:
- [ ] Core feature works end-to-end (not just UI, the actual workflow)
- [ ] Landing page exists (Next.js + shadcn/ui + Tailwind) with clear value prop, pricing, and CTA
- [ ] Auth works (NextAuth.js or custom JWT — sign up, log in, session management)
- [ ] Billing integration exists (Stripe Checkout + webhooks in NestJS — can be test mode)
- [ ] Frontend deployable to Vercel (vercel.json or auto-detect)
- [ ] Backend deployable to Railway/Fly.io (Dockerfile or deploy config)
- [ ] Prisma migrations run cleanly on a fresh database
- [ ] `.env.example` documents all required environment variables
- [ ] README has setup instructions (pnpm install, database setup, env vars, dev server)
- [ ] No hardcoded secrets or obvious security issues

**When 9/10 or 10/10 — enter pre-launch quality gate mode.**
Run ONE gate skill per iteration (they are separate iterations, not one batch):
- Gate 1: **`page-cro`** on landing page → apply fixes
- Gate 2: **`seo-audit`** → fix critical issues
- Gate 3: **`a11y-audit`** → fix Level A/AA violations
- Gate 4: **`webapp-testing`** → Playwright smoke tests
- Gate 5: **`simplify`** → code quality pass

Track gate progress in audit-log: `Quality gates: 3/5 passed`

**When 10/10 checklist AND 5/5 gates passed:**
1. Update TRACKER.md: status → `MVP_COMPLETE`
2. Update `research/reports/2026-04-04-idea-leaderboard.md` with `[MVP SHIPPED]` tag
3. Next iteration for this idea: invoke `launch-strategy` skill
4. Following iteration: invoke `social-content` skill
5. If ALL N ideas are MVP_COMPLETE or KILLED → output `[LOOP_COMPLETE]` at the very end of your response

---

## TRACKER.md FORMAT

If TRACKER.md doesn't exist, create it with this structure:

```markdown
# Implementation Tracker

Last updated: YYYY-MM-DD

## Active Ideas

| # | Idea | Folder | Status | Phase | Last Iteration | Blockers |
|---|------|--------|--------|-------|---------------|----------|
| 1 | [idea name] | [folder]/ | NOT_STARTED | — | — | None |

## Status Key
- `NOT_STARTED` — idea selected, no work done yet
- `PLANNING` — plan written, monorepo scaffolded, no application code yet
- `BUILDING` — actively implementing features
- `AUDITING` — code review / bug fixing pass
- `MVP_COMPLETE` — all 10 checklist items done, ready to launch
- `LAUNCHED` — live and accepting users
- `KILLED` — abandoned (with reason)
- `SCOUTING` — (acquisition only) researching targets
- `DUE_DILIGENCE` — (acquisition only) evaluating a specific target

## MVP Completion Checklist (per idea — 10 items)
### [Idea Name]
- [ ] 1. Core feature works end-to-end
- [ ] 2. Landing page (Next.js + shadcn/ui + Tailwind) with value prop, pricing, CTA
- [ ] 3. Auth (NextAuth.js or custom JWT)
- [ ] 4. Billing (Stripe Checkout + webhooks in NestJS)
- [ ] 5. Frontend deployable to Vercel
- [ ] 6. Backend deployable to Railway/Fly.io
- [ ] 7. Prisma migrations run cleanly on fresh database
- [ ] 8. `.env.example` documents all required env vars
- [ ] 9. README has setup instructions
- [ ] 10. No hardcoded secrets or security issues
```

---

## IMPORTANT RULES

1. **ONE idea, ONE deliverable per loop cycle.** This is the most important rule. Don't scatter across ideas or try to do multiple things. Depth > breadth.
2. **Tracking files are your ONLY memory.** Read them thoroughly at the start. Write them thoroughly at the end. If it's not in the files, it didn't happen.
3. **Fix broken things before building new things.** If the audit-log shows a FAIL or blocker, address it first.
4. **Landing page is NOT optional.** It ships in Phase 2, before polish. No landing page = no customers = dead product.
5. **Working > perfect.** An ugly feature that works beats a beautiful one that doesn't.
6. **Never let any idea stall 3+ iterations.** If blocked, either solve the blocker or kill the idea with a reason in TRACKER.md.
7. **If an idea hits a fundamental blocker** (API doesn't exist, legal issue, technical impossibility), update TRACKER.md with status `KILLED` and the reason, then move to the next idea.
8. **Respect project boundaries** — each idea is its own folder. Don't mix code across projects.
9. **Check Plata (projects/costs-tracker/) for patterns** — it's the reference implementation for how Jobelo ships products. Match its doc structure.
10. **When all ideas reach MVP_COMPLETE or KILLED**, output `[LOOP_COMPLETE]` so the loop gets cancelled.
