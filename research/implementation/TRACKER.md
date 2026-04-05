# Implementation Tracker

Last updated: 2026-04-05

## Active Ideas

| # | Idea | Type | Folder | Status | Phase | Last Iteration | Blockers |
|---|------|------|--------|--------|-------|---------------|----------|
| 1 | DriftWatch — API dependency change monitor | SaaS | projects/driftwatch/ | POLISHING | Phase 3 | 2026-04-05 (#12) | DB URL + Stripe keys + domain needed for production deploy |
| 2 | StubSnap — Paystub Generator | Tool | projects/stubsnap/ | KILLED | — | 2026-04-05 (#1) | Killed in tool leaderboard: ThePayStubs.com is a full tax platform (30+ IRS forms), not a simple tool. One feature vs full platform = no viable path. |
| 3 | Freight Broker Micro-TMS | SaaS | projects/freight-tms/ | KILLED | Phase 2 | 2026-04-05 (#7) | Distribution requires high-touch sales to offline buyers (freight brokers). Incompatible with async/automated marketing. |
| 4 | Acquisition Play — buy underperforming extension | — | projects/acquisition-play/ | KILLED | — | 2026-04-05 (#3) | Sub-$5K market depleted after 3 iterations, 8 marketplaces, 8/8 candidates eliminated. Build > buy at this budget. |

## Status Key
- `NOT_STARTED` — idea selected, no work done yet
- `PLANNING` — plan written, monorepo scaffolded, no application code yet
- `BUILDING` — actively implementing features
- `POLISHING` — MVP checklist 9-10/10, running 10 polish/audit gates
- `MVP_COMPLETE` — all 10 checklist items + 10/10 polish gates done
- `LAUNCHING` — executing launch strategy (2-3 iterations)
- `LAUNCHED` — live, accepting users, launch posts published
- `GROWING` — V2/growth phase, continuous improvement
- `STABLE` — 10+ growth iterations done, diminishing returns, can stop
- `KILLED` — abandoned (with reason)
- `SCOUTING` — (acquisition only) researching targets
- `DUE_DILIGENCE` — (acquisition only) evaluating a specific target

## Idea Context

### 1. DriftWatch (Score: 22/30 — meets SaaS threshold)
- **What**: Crawls third-party API changelogs, uses AI to classify breaking vs non-breaking changes, alerts engineering teams
- **Buyer**: Engineering leads at B2B SaaS companies (10-100 person teams)
- **Price**: $49-99/mo
- **Evidence**: 52% of devs cite breaking changes as top API concern (Postman 2025)
- **Competitor**: API Drift Alert (early/weak)
- **Edge**: AI classification, aggressive pricing, modern DX

### 2. StubSnap (Score: 17/25 — meets Tool threshold)
- **What**: Modern IRS-compliant paystub generator. $3.99/stub. Pay-per-use.
- **Buyer**: Small business owners, freelancers, contractors who need paystubs
- **Price**: $3.99/stub (transactional)
- **Evidence**: 117K visits/mo to top competitor. Compliance-gated tools resist "free and good enough" pattern.
- **Edge**: Modern UX, IRS-compliant calculations, zero API costs, SEO-friendly transactional model

### 3. Freight Broker Micro-TMS (KILLED — Score: 13/30)
- **Kill reason**: AscendTMS free tier + OSS LoadPartner. Offline buyers require high-touch sales.

### 4. Acquisition Play (KILLED)
- **Kill reason**: Sub-$5K market depleted. 8 marketplaces scanned, 8/8 candidates eliminated.

## MVP Completion Checklist (10 items)

### DriftWatch
- [ ] 1. Core feature works end-to-end (changelog crawling + AI classification + alerting)
- [ ] 2. Landing page (Next.js + shadcn/ui + Tailwind) with value prop, pricing, CTA
- [ ] 3. Auth (NextAuth.js or custom JWT — sign up, log in, sessions)
- [ ] 4. Billing (Stripe Checkout + webhooks in NestJS — can be test mode)
- [ ] 5. Frontend deployable to Vercel
- [ ] 6. Backend deployable to Railway/Fly.io (Dockerfile or config)
- [ ] 7. Prisma migrations run cleanly on fresh database
- [ ] 8. `.env.example` documents all required environment variables
- [ ] 9. README has setup instructions (pnpm install, DB setup, env vars, dev server)
- [ ] 10. No hardcoded secrets or obvious security issues

### StubSnap
- [ ] 1. Core feature works end-to-end (input employee/employer info → generate IRS-compliant paystub PDF)
- [ ] 2. Landing page (Next.js + Tailwind) with value prop, pricing, CTA
- [ ] 3. Auth (NextAuth.js or guest checkout — may not need full auth for transactional tool)
- [ ] 4. Billing (Stripe Checkout — $3.99 per stub, one-time payment)
- [ ] 5. Frontend deployable to Vercel
- [ ] 6. Backend deployable (API routes or separate NestJS if needed)
- [ ] 7. Database migrations run cleanly (if using DB)
- [ ] 8. `.env.example` documents all required environment variables
- [ ] 9. README has setup instructions
- [ ] 10. No hardcoded secrets or obvious security issues
