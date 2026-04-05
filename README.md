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

### Planned (from /implement)

| Project | Description | Status |
|---------|-------------|--------|
| projects/driftwatch/ | **DriftWatch** — API dependency change monitor for SaaS teams | Not started |
| projects/freight-tms/ | **Freight Broker Micro-TMS** — load tracking + invoicing for small brokerages | Not started |

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
| [06-KILLED-IDEAS](research/strategy/06-KILLED-IDEAS.md) | 170+ killed ideas from 13 research iterations |
| [TRACKER](research/implementation/TRACKER.md) | Implementation progress for /implement command |
| [Idea Leaderboard](research/reports/2026-04-04-idea-leaderboard.md) | Running leaderboard of all ideas scored |

New research and reports go in `research/reports/` with date-prefixed filenames.

## Commands

| Command | Purpose |
|---------|---------|
| `/implement --ideas 3` | Build top N micro-SaaS MVPs (works with `/loop 30m`) |
| `/research-ideas` | Find new micro-SaaS ideas (13 iterations done, 170+ killed) |

## Current Priority

1. Enter next Code4rena competitive audit contest (immediate money)
2. Ship Plata to App Store and focus on distribution
3. Build DriftWatch MVP (best surviving idea at 17/25)
