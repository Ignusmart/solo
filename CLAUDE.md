# Solo — Monorepo for Personal Projects & Research

This is Jobelo's solo workspace: a collection of personal projects, entrepreneurial research, and experiments. It is NOT a single application — it's an organized workspace.

## Repo Structure

```
solo/
├── CLAUDE.md                  # You are here
├── README.md                  # Project overview and status
├── .claude/commands/          # Slash commands (/implement, /research-ideas, /research-tool-ideas, /ideas-status, /auto-audit)
├── research/                  # Strategy docs, market research, reports
│   ├── strategy/              # Income strategy, ideas, playbooks (00-07 series)
│   ├── reports/               # Deep-dive audits, analyses, research outputs
│   └── implementation/        # TRACKER.md for /implement command
└── projects/                  # ALL projects live here (gitignored — each has own repo)
    ├── bounty/                # Bug bounty & competitive audit work
    ├── costs-tracker/         # Plata — LATAM expense tracker (Flutter + NestJS) [own git]
    ├── cv/                    # Resume / CV generator [own git]
    ├── games/                 # Game experiments (crawling_chaos, sprites-generator)
    ├── hackathons/            # Hackathon tracker & entries (like bounty/ but for hackathons)
    ├── ignusmart/             # IgnuSmart — Next.js project [own git]
    ├── open-saas/             # Open SaaS template reference [own git]
    ├── saas-costs-tracker/    # SaaS costs tracker
    ├── salary-comparison/     # Python salary/credit analysis scripts
    ├── apidelta/            # APIDelta — API dependency change monitor [BUILDING]
    ├── stubsnap/              # StubSnap — IRS-compliant paystub generator [KILLED — competitors are full tax platforms]
    ├── acquisition-play/      # Acquisition play [KILLED — market depleted]
    └── freight-tms/           # Freight broker micro-TMS [KILLED — offline buyers]
```

## Key Context

- **Owner profile**: Principal Engineer, 10+ years. Three pillars: Solidity/Web3 security, AI/agentic systems, full-stack TS/Python.
- **Constraint**: Async-only, no calls. Products and competitive audits over freelance/consulting.
- **All projects live in `projects/`** — this folder is gitignored. Each project has its own git repo.
- **This root repo tracks**: research, strategy, commands, and implementation progress. NOT project code.

## Important: Off-Limits Product Domains

- **Web3 SECURITY products are OFF LIMITS** (narrow rule — Web3 broadly is fine): no wallet risk scoring, smart contract monitoring/auditing tools, compliance/OFAC tooling, transaction classifiers, depegging monitors, or anything adjacent. This is Jobelo's professional domain at Webacy and would conflict with his employment.
- **Web3 non-security IS allowed**: trading systems, arbitrage bots, DeFi tooling, yield strategies, NFT tools, on-chain analytics (non-security angle), wallet UX, dev tooling, RPC/indexers, bridges, cross-chain UX, MEV infra. Before rejecting a Web3 idea, ask: "Is this specifically a *security* product?" If no → it's on the table.
- His security/blockchain skills are **transferable building skills** (architecture, data pipelines, API design) — and his Solidity/EVM/Solana expertise is a *building advantage* for non-security Web3 products too.
- When brainstorming micro SaaS or product ideas, target non-Web3-security verticals (but Web3 non-security is fair game).
- **Target global markets** — not Colombia/LATAM-specific niches. English-first, global distribution. LATAM can be secondary but not the primary value proposition.

## Working in This Repo

- **Research before building**: Use `research/` to capture market research, competitive analysis, feasibility studies, and decision docs before starting a new project.
- **Reports go in `research/reports/`**: Named as `YYYY-MM-DD-topic.md` for chronological ordering.
- **Strategy docs live in `research/strategy/`**: The 00-07 numbered series covers skills, ideas, playbooks, killed ideas. Update these as the strategy evolves.
- **New projects go in `projects/`**: Create `projects/<name>/`, add a README and CLAUDE.md, optionally `git init`. The `/implement` command handles this automatically.
- **Don't refactor subprojects from here** — cd into `projects/<name>/` and work with their own CLAUDE.md.

## Commands

- **`/implement`** — Build micro-SaaS MVPs from the unified leaderboard (SaaS + tools). Works with `/loop 30m`. Tracks progress in `research/implementation/TRACKER.md`.
- **`/research-ideas`** — Find new micro-SaaS ideas. 16 iterations done, 190+ killed. Works with `/loop`.
- **`/research-tool-ideas`** — Find transactional utility tool ideas. 3 iterations done. Works with `/loop`.
- **`/ideas-status`** — Read-only dashboard of all ideas across both research tracks and implementation pipeline.
- **`/auto-audit`** — Audit workspace for staleness, inconsistencies, and broken cross-references. Use `--fix` to auto-repair safe issues.

## Current Revenue Strategy (as of April 2026)

1. **Competitive audits & bounties** — historically framed as primary income (60-70% time), but claude-bug-bounty harness has produced **$0 paid across ~170 projects audited** as of 2026-04-18 (see `projects/bounty/claude-bug-bounty/BOUNTIES.md`). Root cause is target saturation (most live programs have 5-20 prior audits + Certora FV). One live signal: `immunefi-ssvnetwork` F-12 High ESCALATED to team 2026-04-17; 5 other submissions pending. Allocation is **under review** until ssvnetwork resolves — do not default to "primary income" framing.
2. **ScanAble** (projects/scanable/) — LAUNCHING, Google Ads live since Apr 10, pSEO + compliance moat
3. **APIDelta** (projects/apidelta/) — **V2 LAUNCHED 2026-04-29** (post-V2 metric window now active). Originally community-launched 2026-04-15; the May 15 / Day 30 pre-V2 checkpoint was deferred on 2026-04-28 (~14 visitors/7d, 0 signups, 0 MRR) and a 4-phase V2 was built and shipped the next day. V2 ships: curated catalog (39 entries at `/catalog`), MCP server (5 tools at `/api/mcp`), workflow integrations (HMAC-signed webhooks + GitHub Issues + team invites), three named-competitor compare pages, a "why not just build this?" content page, and new pricing (Starter $49 / Team $199 / Business contact-sales). Full timeline in `projects/apidelta/docs/v2-tracker.md`. **Three checkpoints, not one** (B2B dev-tools cold launch reality — Sentry / Linear / Convex / MicroConf founder data shows 6-9 months to first paying customer): (a) **Day 30 = 2026-05-29 — distribution diagnostic** (read visitors/conversion, fix tactic not product); (b) **Day 60 = 2026-06-28 — positioning checkpoint** (if traffic fixed but 0 trials, buyer/value-prop mismatch); (c) **Day 90 = 2026-07-28 — hard kill backstop** ($0 MRR with consistent marketing → reassess PMF, consider sunset/pivot). Day-30 floor: >500 visitors/week, >10 trials, >1 paying customer, >$49 MRR.
4. **Plata app** (projects/costs-tracker/) — already shipped, needs distribution/marketing
5. **New tool/SaaS MVPs** — backfill from unified leaderboard as slots open (see TRACKER.md)
6. **Technical content** — builds audience and reputation

## Common Tasks

- **Add new research**: Create a file in `research/reports/` with the date prefix
- **Update strategy**: Edit the relevant `research/strategy/0X-*.md` file
- **Start a new project**: Run `/implement` or create `projects/<name>/` manually
- **Review progress**: Check `research/implementation/TRACKER.md` or `research/reports/`
