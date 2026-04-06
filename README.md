# Solo

Income strategies and personal projects for a full-stack + Solidity + AI developer who hates calls.

## Projects

All projects live in `projects/` (gitignored — each has its own repo).

| Project | Description | Status |
|---------|-------------|--------|
| [projects/costs-tracker/](projects/costs-tracker/) | **Plata** — LATAM expense tracker (Flutter + NestJS). Voice input, AI categorization, receipt scanning. | v1.0.0 — App Store ready |
| [projects/bounty/](projects/bounty/) | Bug bounty & competitive audit framework. AI-powered with Claude Code plugin. 20+ protocols studied. | Active |
| [projects/ignusmart/](projects/ignusmart/) | IgnuSmart — Next.js web app | In progress |
| [projects/cv/](projects/cv/) | Resume/CV generator with PDF export | Maintained |
| [projects/games/](projects/games/) | Game experiments: crawling_chaos, sprites-generator (Gemini API) | Experimental |
| [projects/open-saas/](projects/open-saas/) | Open SaaS template reference (Wasp framework) | Reference |
| [projects/salary-comparison/](projects/salary-comparison/) | Python scripts for salary and car credit analysis | Utility |

### In Progress (from /implement)

| Project | Description | Status |
|---------|-------------|--------|
| projects/apidelta/ | **APIDelta** — API dependency change monitor for SaaS teams | Building (Phase 2, iteration #7) |
| projects/stubsnap/ | **StubSnap** — IRS-compliant paystub generator ($3.99/stub) | Not started |

### Killed

| Project | Reason |
|---------|--------|
| Freight Broker Micro-TMS | Offline buyers, requires high-touch sales |
| Acquisition Play | Sub-$5K market depleted after 3 iterations |

## Research & Strategy

All strategy docs and research reports live in [`research/`](research/).

| Document | Purpose |
|----------|---------|
| [00-SKILLS-PROFILE](research/strategy/00-SKILLS-PROFILE.md) | Skills inventory derived from all repos |
| [01-IDEAS-RANKED](research/strategy/01-IDEAS-RANKED.md) | All ideas ranked by fit, revenue, and effort |
| [02-BUG-BOUNTY-PIVOT](research/strategy/02-BUG-BOUNTY-PIVOT.md) | Why bounties are hard + pivot to competitive audits |
| [03-QUICK-WINS](research/strategy/03-QUICK-WINS.md) | Fastest paths to first dollar (< 30 days) |
| [04-PRODUCT-IDEAS-DEEP-DIVE](research/strategy/04-PRODUCT-IDEAS-DEEP-DIVE.md) | Detailed breakdown of top 3 product ideas |
| [05-NO-CALLS-PLAYBOOK](research/strategy/05-NO-CALLS-PLAYBOOK.md) | Operating with zero synchronous communication |
| [06-KILLED-IDEAS](research/strategy/06-KILLED-IDEAS.md) | 190+ killed ideas from 16 research iterations |
| [07-KILLED-TOOL-IDEAS](research/strategy/07-KILLED-TOOL-IDEAS.md) | Killed tool ideas from /research-tool-ideas |
| [TRACKER](research/implementation/TRACKER.md) | Implementation progress for /implement command |
| [SaaS Leaderboard](research/reports/2026-04-04-idea-leaderboard.md) | Running leaderboard of SaaS ideas (16 iterations, 190+ ideas) |
| [Tool Leaderboard](research/reports/tool-ideas-leaderboard.md) | Running leaderboard of utility tool ideas (3 iterations, 40+ ideas) |

New research and reports go in `research/reports/` with date-prefixed filenames.

## Commands

### `/implement` — Build MVPs from the unified leaderboard

Spawns parallel agents to build micro-SaaS and utility tool MVPs. Designed for continuous use with `/loop`. Each invocation is one iteration: reads state from tracking files, spawns one agent per active idea, consolidates results.

**Usage:**
```
/implement                  # Default: work on 3 ideas in parallel
/implement --ideas 5        # Work on 5 ideas in parallel
/implement --idea apidelta  # Work on a single specific idea
```

**Arguments:**
| Argument | Default | Description |
|----------|---------|-------------|
| `--ideas N` | 3 | Number of ideas to work on in parallel. Spawns N agents, one per idea. |
| `--idea <name>` | — | Work on a single specific idea by name. |

**How it works:**
1. Reads TRACKER.md + both source leaderboards (SaaS and Tools)
2. Builds/updates a unified leaderboard with normalized scores
3. Backfills empty slots from the unified leaderboard (highest score first)
4. Spawns N parallel agents — each advances its idea by one deliverable
5. Consolidates results into TRACKER.md

**Loop usage:** `/loop 30m /implement --ideas 3` — runs every 30 minutes, walking each idea through PLAN → BUILD → POLISH → LAUNCH → GROW phases.

**Key files:**
- `research/implementation/TRACKER.md` — implementation state
- `research/implementation/unified-leaderboard.md` — merged SaaS + Tool rankings
- `projects/<name>/docs/audit-log.md` — per-idea iteration history
- `projects/<name>/docs/plan.md` — per-idea phase plan

---

### `/research-ideas` — Find micro-SaaS ideas

Hunts for subscription SaaS opportunities ($19-99/mo). Multi-source signal hunting across Reddit, HN, Product Hunt, G2, and market research. Each iteration explores new verticals, deep-dives 2-3 ideas, runs adversarial review, and scores on 6 dimensions.

**Usage:**
```
/research-ideas             # Run one iteration
```

**No arguments.** Each invocation is one self-contained iteration. State is tracked in files.

**Scoring:** 6 dimensions, max 30 points. Distribution dimensions weighted 2x. Bar: 22/30 after adversarial review.

**Loop usage:** `/loop 30m /research-ideas` — continuous idea hunting.

**Key files:**
- `research/reports/2026-04-04-idea-leaderboard.md` — ranked SaaS ideas
- `research/reports/YYYY-MM-DD-market-gap-iteration-N.md` — per-iteration findings
- `research/strategy/06-KILLED-IDEAS.md` — killed ideas registry (178+ entries)

**Status:** 16 iterations completed, 190+ ideas considered, SaaS track exhausted. APIDelta (22/30) is the only survivor above bar.

---

### `/research-tool-ideas` — Find transactional utility tool ideas

Hunts for pay-per-use, credit-based, or one-time-purchase tools (think Pieter Levels' PhotoAI model). Different economics from SaaS: no churn problem, but needs high volume and good SEO.

**Usage:**
```
/research-tool-ideas        # Run one iteration
```

**No arguments.** Each invocation is one self-contained iteration.

**Scoring:** 5 dimensions, max 25 points. Bar: 16/25 after adversarial review.

**Loop usage:** `/loop 30m /research-tool-ideas` — continuous tool idea hunting.

**Key files:**
- `research/reports/tool-ideas-leaderboard.md` — ranked tool ideas
- `research/reports/YYYY-MM-DD-tool-ideas-iteration-N.md` — per-iteration findings
- `research/strategy/07-KILLED-TOOL-IDEAS.md` — killed tool ideas registry

**Status:** 3 iterations completed, 40+ ideas killed. StubSnap at 17/25 — first to hit build threshold. Now in TRACKER as NOT_STARTED.

---

### `/ideas-status` — Consolidated ideas dashboard

Read-only command that shows the status of all ideas across both research tracks and the implementation pipeline in a single view. Does not modify any files.

**Usage:**
```
/ideas-status               # Quick dashboard (research pipeline + implementation + unified leaderboard)
/ideas-status --detail apidelta  # Deep dive on a specific idea (audit-log, plan, git log)
```

**Arguments:**
| Argument | Default | Description |
|----------|---------|-------------|
| `--detail <name>` | — | Show detailed info for a specific idea: latest audit-log entry, plan progress, MVP checklist, last 3 git commits. |

**Output includes:**
- Research pipeline stats (iterations, ideas scored/killed, best surviving per track)
- Implementation pipeline table (status, phase, iteration, MVP progress, blockers)
- Unified leaderboard with normalized scores and availability status

---

### `/auto-audit` — Workspace consistency audit

Checks that all tracking files, docs, and commands are in sync. Flags staleness, contradictions, and missing cross-references. Maintains its own changelog at `research/implementation/audit-changelog.md` for loop memory.

**Usage:**
```
/auto-audit                 # Report only — find issues, log to changelog, don't fix
/auto-audit --fix           # Find issues + auto-fix safe ones (README, CLAUDE.md, unified leaderboard)
/auto-audit --deep          # Also check project folders (git status, missing docs, iteration drift)
/auto-audit --fix --deep    # Full audit + fix + project folder checks
```

**Arguments:**
| Argument | Default | Description |
|----------|---------|-------------|
| `--fix` | off | Auto-fix safe issues: sync README/CLAUDE.md from TRACKER, create missing unified leaderboard, update killed-ideas registries. Does NOT fix project folder issues or scoring mismatches. |
| `--deep` | off | Add checks 8-9: `/implement` command internal consistency (step ordering, duplicate labels, prompt length) and project folder health (git init, missing docs, uncommitted changes). |

**9 checks run:**
1. Command inventory — are all commands listed in CLAUDE.md and README?
2. README freshness — do project statuses match TRACKER?
3. CLAUDE.md freshness — iteration counts, commands, revenue strategy current?
4. TRACKER consistency — do project folders and audit-logs exist and match?
5. Leaderboard consistency — unified leaderboard exists? scoring systems match?
6. Strategy docs — 00-07 series complete?
7. Killed ideas cross-reference — killed in TRACKER but missing from registry?
8. `/implement` internals — step ordering, duplicates, prompt length (--deep only)
9. Project folder health — git, docs, uncommitted changes (--deep only)

**Loop usage:** `/loop 1h /auto-audit --fix` — hourly consistency enforcement.

**Changelog:** Each run appends to `research/implementation/audit-changelog.md`. Issues are classified as NEW, RECURRING (with count), REGRESSED, or FIXED. Warnings recurring 3+ times auto-escalate to errors.

## Current Priority

1. Enter next Code4rena competitive audit contest (immediate money)
2. Ship Plata to App Store and focus on distribution
3. Build APIDelta MVP (22/30 — actively building, Phase 2, iteration #7)
4. Run more `/research-tool-ideas` iterations to find viable tool ideas
