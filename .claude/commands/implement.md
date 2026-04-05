You are implementing micro-SaaS MVPs for Jobelo. This command builds products from the idea leaderboard, one iteration at a time, designed to work with `/loop`.

## Arguments
- `$ARGUMENTS` — parse for `--ideas N` (default: 3) or `--idea <name>`. If $ARGUMENTS is empty or missing, default to `--ideas 3`.

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

## LOOP EXECUTION MODEL — PARALLEL AGENTS

This command is designed for `/loop 30m /implement --ideas 3`. Each invocation is ONE iteration. The `--ideas N` argument means **ALL N ideas are worked on in parallel** — one agent per idea.

**You have NO memory of previous iterations** — the tracking files ARE your memory.

### Iteration lifecycle (every single run):
```
ORCHESTRATOR: Read TRACKER.md
  → Spawn Agent 1 (Idea #1) ─┐
  → Spawn Agent 2 (Idea #2) ─┼─ ALL run in PARALLEL via Agent tool
  → Spawn Agent 3 (Idea #3) ─┘
  ← Collect results from all agents
  → Update TRACKER.md with consolidated status
  → Check if all ideas are MVP_COMPLETE or KILLED → output [LOOP_COMPLETE] if so
```

### Orchestrator responsibilities (you — the main process):
1. **Read TRACKER.md** — determine status of all N ideas
2. **For each active idea** (not KILLED, not MVP_COMPLETE), **spawn one Agent** using the Agent tool:
   - Pass the agent a complete brief: idea name, folder path, current status, last iteration's "What's next", blockers, which step to execute (Plan or Build), and the relevant skill to invoke if applicable
   - Set `isolation: "worktree"` is NOT needed — each agent works in its own `projects/<name>/` folder, so they don't conflict
   - **Launch ALL agents in a SINGLE message** (parallel tool calls) — do NOT wait for one to finish before starting the next
3. **After all agents return**, read each idea's updated `docs/audit-log.md` and consolidate into TRACKER.md
4. **Check completion** — if all ideas are MVP_COMPLETE or KILLED, output `[LOOP_COMPLETE]`

### Agent brief template (what you pass to each spawned agent):
```
You are building the MVP for [IDEA NAME].

## Current state
- Folder: projects/[folder]/
- Status: [from TRACKER.md]
- Last iteration did: [from audit-log "What was done"]
- Next task: [from audit-log "What's next"]
- Blockers: [from audit-log or "None"]

## What to do this iteration
[Either PLAN (Step 1) or BUILD (Step 2) — be specific about the deliverable]

## Skill to invoke (if applicable)
[The ONE skill for this deliverable, or "None"]

## Tech stack (mandatory)
[Include the full tech stack rules from this command]

## When done
Write your results to:
1. projects/[folder]/docs/audit-log.md — append iteration entry
2. projects/[folder]/docs/plan.md — check off completed items
Do NOT update TRACKER.md — the orchestrator handles that.
```

### How to determine iteration number:
1. Read `research/implementation/TRACKER.md` — check "Last iteration" column for each idea
2. For each idea, read its `docs/audit-log.md` — count existing `## Iteration N` headers
3. Each idea has its OWN iteration counter (they progress independently)
4. If no audit-log exists for an idea, it's iteration 1 for that idea

### Scope per agent per iteration:
- **One meaningful deliverable per agent.** Examples: "NestJS project scaffolded with Prisma + first migration", "changelog crawler service working for 3 APIs", "landing page hero + pricing section done".
- **If the last iteration left something broken, the agent fixes it FIRST** before new work.
- **Max ONE skill invocation per agent** — skills are heavy.

### Handling agent failures:
- If an agent errors or times out, note it as a blocker in TRACKER.md for that idea
- The other agents' work is NOT affected — they run independently
- Next iteration will retry the failed idea

### When to skip an idea (don't spawn an agent):
- Status is `MVP_COMPLETE` — done, no agent needed
- Status is `KILLED` — dead, no agent needed
- Status is `LAUNCHED` — post-launch, no agent needed

---

## STEP 0: ORCHESTRATOR READS STATE + DISPLAYS STATUS (mandatory, every iteration)

### 0A) Read state

**You MUST read these files before doing anything:**

1. `research/implementation/TRACKER.md` — current status of all ideas, which iteration each is on, blockers
   - **If this file does not exist**, create it using the format in the TRACKER.md FORMAT section below, seeded from the leaderboard's top N ideas.
2. For EACH active idea, read its `docs/audit-log.md` (if it exists) — what was done last time, what's next, what's broken
   - **If this file does not exist**, the agent brief should say "PLAN this idea (Step 1)".
3. For EACH active idea, read its `docs/plan.md` (if it exists) — what phase we're in, what's the next deliverable
   - **If this file does not exist**, the agent brief should say "PLAN this idea (Step 1)".

### 0B) Display status dashboard (output to user — NO input needed, NO waiting)

**Before spawning agents, output this dashboard as text so the user sees progress. Then immediately proceed to spawn agents — do NOT wait for user input.**

```
## /implement iteration — [DATE]

| # | Idea | Status | Phase | Iteration | MVP | Next Deliverable | Blocker |
|---|------|--------|-------|:---------:|:---:|-----------------|---------|
| 1 | DriftWatch | BUILDING | Phase 1 | 4 | 3/10 | Build crawler service | None |
| 2 | Freight TMS | PLANNING | — | 1 | 0/10 | Scaffold monorepo | None |
| 3 | Acquisition | SCOUTING | — | 2 | 0/5 | Research targets | None |

Spawning 3 agents in parallel...
```

Fill in actual values from TRACKER.md and audit-logs. The MVP column shows checklist progress (X/10 for builds, X/5 for acquisition). Then immediately proceed — this is a status display, not a prompt.

### 0C) Prepare agent briefs and spawn

- For each active idea: determine its iteration number, current status, next deliverable, applicable skill
- Determine which step each agent should execute (Plan vs Build vs Quality Gate)
- **Then spawn ALL agents in parallel using a single message with multiple Agent tool calls — do NOT wait for user input between the dashboard and the spawn**

---

## AVAILABLE SKILLS (invoke via the Skill tool)

You have access to specialized skills that produce higher-quality output than doing it manually. **Max ONE skill per agent per iteration.** The orchestrator assigns the skill in each agent's brief.

### CRITICAL RULE: One skill per agent per iteration
Each skill is a full analysis/generation pass. Each agent should invoke at most ONE skill per iteration. The orchestrator assigns the skill in the agent brief based on the deliverable. **Since agents run in parallel, up to N skills can run simultaneously (one per agent).**

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

## AGENT INSTRUCTIONS (Steps 1-4 below are what each AGENT executes — passed via the brief)

The orchestrator does NOT execute these steps directly. They are included here as the specification for what agents do. The orchestrator copies the relevant step into each agent's brief.

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
8. **STOP.** Do NOT write application code in the planning iteration. Plan first, build next.
   *(The orchestrator will update TRACKER.md after this agent returns.)*

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

## STEP 4: AGENT WRITES ITS OWN TRACKING (every iteration, non-negotiable)

Each agent writes to its OWN project files only. **Do NOT touch TRACKER.md** — the orchestrator handles that after all agents return.

### A) `projects/<name>/docs/audit-log.md` — append new entry:
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
- Skills used: [skill-name or "none"]
- MVP checklist: X/10 complete
### What's next
- [THE single next deliverable — be specific]
### Blockers
- [anything preventing progress, or "None"]
```

### B) `projects/<name>/docs/plan.md` — check off completed deliverables

### C) The orchestrator reads the above after all agents return, then updates TRACKER.md

### D) Check for MVP completion (orchestrator reads this from audit-log):
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

## STEP 5: ORCHESTRATOR CONSOLIDATION (after all agents return)

This is what YOU (the orchestrator) do after all parallel agents complete. **Do NOT ask the user for input — proceed automatically.**

1. **Read each idea's updated `docs/audit-log.md`** — extract status, MVP score, blockers, what's next
2. **Update `research/implementation/TRACKER.md`** with consolidated data:
   - Status column: derive from audit-log (PLANNING if just planned, BUILDING if code written, etc.)
   - Phase column: current phase from plan.md
   - Last Iteration column: today's date + idea's iteration number
   - Blockers column: from audit-log
3. **Output a results summary** (no user input needed):
   ```
   ## Results

   | # | Idea | Did | MVP | Next |
   |---|------|-----|:---:|------|
   | 1 | DriftWatch | Built crawler service | 4/10 | Dashboard page |
   | 2 | Freight TMS | Wrote plan + scaffolded | 0/10 | pnpm install + first migration |
   | 3 | Acquisition | Researched 2 targets | 1/5 | Due diligence on Target A |
   ```
4. **Check completion**: if ALL ideas are MVP_COMPLETE or KILLED → output `[LOOP_COMPLETE]`
5. **Commit tracking updates** if any research/ files changed: `git add research/ && git commit -m "update implementation tracker"`

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

1. **ALL active ideas run in PARALLEL every iteration.** Spawn one agent per idea in a single message. This is the core execution model.
2. **Each agent: ONE deliverable, max ONE skill.** Agents work independently within their own `projects/<name>/` folder.
3. **Agents write their own audit-logs. Orchestrator writes TRACKER.md.** This avoids write conflicts. Agents must NOT touch TRACKER.md.
4. **Tracking files are the ONLY memory.** Read them thoroughly at the start. Write them thoroughly at the end. If it's not in the files, it didn't happen.
5. **Fix broken things before building new things.** If an agent's audit-log shows a FAIL or blocker, its next iteration brief should say "fix this first."
6. **Landing page is NOT optional.** It ships in Phase 2, before polish. No landing page = no customers = dead product.
7. **Working > perfect.** An ugly feature that works beats a beautiful one that doesn't.
8. **Never let any idea stall 3+ iterations.** If blocked, either solve the blocker or kill the idea with a reason in TRACKER.md.
9. **If an idea hits a fundamental blocker** (API doesn't exist, legal issue, technical impossibility), the agent should note it in audit-log and the orchestrator updates TRACKER.md with status `KILLED` and reason.
10. **Respect project boundaries** — each idea is its own folder. Agents must NOT modify files outside their assigned `projects/<name>/` folder.
11. **Check Plata (projects/costs-tracker/) for patterns** — it's the reference implementation for how Jobelo ships products. Match its doc structure.
12. **When all ideas reach MVP_COMPLETE or KILLED**, output `[LOOP_COMPLETE]` so the loop gets cancelled.
