# Solo — Monorepo for Personal Projects & Research

This is Jobelo's solo workspace: a collection of personal projects, entrepreneurial research, and experiments. It is NOT a single application — it's an organized workspace.

## Repo Structure

```
solo/
├── CLAUDE.md                  # You are here
├── README.md                  # Project overview and status
├── .claude/commands/          # Slash commands (/implement, /research-ideas)
├── research/                  # Strategy docs, market research, reports
│   ├── strategy/              # Income strategy, ideas, playbooks (00-06 series)
│   ├── reports/               # Deep-dive audits, analyses, research outputs
│   └── implementation/        # TRACKER.md for /implement command
└── projects/                  # ALL projects live here (gitignored — each has own repo)
    ├── bounty/                # Bug bounty & competitive audit work
    ├── costs-tracker/         # Plata — LATAM expense tracker (Flutter + NestJS) [own git]
    ├── cv/                    # Resume / CV generator [own git]
    ├── games/                 # Game experiments (crawling_chaos, sprites-generator)
    ├── ignusmart/             # IgnuSmart — Next.js project [own git]
    ├── open-saas/             # Open SaaS template reference [own git]
    ├── saas-costs-tracker/    # SaaS costs tracker
    ├── salary-comparison/     # Python salary/credit analysis scripts
    ├── driftwatch/            # (planned) API dependency change monitor
    └── freight-tms/           # (planned) Freight broker micro-TMS
```

## Key Context

- **Owner profile**: Principal Engineer, 10+ years. Three pillars: Solidity/Web3 security, AI/agentic systems, full-stack TS/Python.
- **Constraint**: Async-only, no calls. Products and competitive audits over freelance/consulting.
- **All projects live in `projects/`** — this folder is gitignored. Each project has its own git repo.
- **This root repo tracks**: research, strategy, commands, and implementation progress. NOT project code.

## Important: Off-Limits Product Domains

- **Web3 security products are OFF LIMITS** — no wallet risk scoring, smart contract monitoring/auditing tools, compliance/OFAC tooling, transaction classifiers, depegging monitors, or anything adjacent. This is Jobelo's professional domain at Webacy and would conflict with his employment.
- His security/blockchain skills are **transferable building skills** (architecture, data pipelines, API design) but the product vertical must be completely different.
- When brainstorming micro SaaS or product ideas, target non-Web3-security verticals.
- **Target global markets** — not Colombia/LATAM-specific niches. English-first, global distribution. LATAM can be secondary but not the primary value proposition.

## Working in This Repo

- **Research before building**: Use `research/` to capture market research, competitive analysis, feasibility studies, and decision docs before starting a new project.
- **Reports go in `research/reports/`**: Named as `YYYY-MM-DD-topic.md` for chronological ordering.
- **Strategy docs live in `research/strategy/`**: The 00-06 numbered series covers skills, ideas, playbooks, killed ideas. Update these as the strategy evolves.
- **New projects go in `projects/`**: Create `projects/<name>/`, add a README and CLAUDE.md, optionally `git init`. The `/implement` command handles this automatically.
- **Don't refactor subprojects from here** — cd into `projects/<name>/` and work with their own CLAUDE.md.

## Commands

- **`/implement`** — Build micro-SaaS MVPs from the idea leaderboard. Works with `/loop 30m`. Tracks progress in `research/implementation/TRACKER.md`.
- **`/research-ideas`** — Find new micro-SaaS ideas. 13 iterations done, 170+ killed. Works with `/loop`.

## Current Revenue Strategy (as of April 2026)

1. **Competitive audits** (Code4rena, Sherlock) — primary income, 60-70% of time
2. **Plata app** (projects/costs-tracker/) — already shipped, needs distribution/marketing
3. **New micro-SaaS MVPs** — DriftWatch + Freight TMS + Acquisition play (see TRACKER.md)
4. **Technical content** — builds audience and reputation

## Common Tasks

- **Add new research**: Create a file in `research/reports/` with the date prefix
- **Update strategy**: Edit the relevant `research/strategy/0X-*.md` file
- **Start a new project**: Run `/implement` or create `projects/<name>/` manually
- **Review progress**: Check `research/implementation/TRACKER.md` or `research/reports/`
