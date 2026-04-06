# Implementation Tracker

Last updated: 2026-04-05 (iteration 27)

## Active Ideas

| # | Idea | Type | Folder | Status | Phase | Last Iteration | Blockers |
|---|------|------|--------|--------|-------|---------------|----------|
| 1 | DriftWatch — API dependency change monitor | SaaS | projects/driftwatch/ | LAUNCHING | Launch C | 2026-04-05 (#27) | Manual: domain, Neon DB, Stripe products, deploy — code complete, all pre-deploy work done |
| 2 | ScanAble — Accessibility Report | Tool | projects/scanable/ | POLISHING | Phase 3 | 2026-04-05 (#12) | None |
| 3 | StubSnap — Paystub Generator | Tool | projects/stubsnap/ | KILLED | — | 2026-04-05 (#1) | Killed in tool leaderboard: ThePayStubs.com is a full tax platform (30+ IRS forms), not a simple tool. One feature vs full platform = no viable path. |
| 4 | Freight Broker Micro-TMS | SaaS | projects/freight-tms/ | KILLED | Phase 2 | 2026-04-05 (#7) | Distribution requires high-touch sales to offline buyers (freight brokers). Incompatible with async/automated marketing. |
| 5 | Acquisition Play — buy underperforming extension | — | projects/acquisition-play/ | KILLED | — | 2026-04-05 (#3) | Sub-$5K market depleted after 3 iterations, 8 marketplaces, 8/8 candidates eliminated. Build > buy at this budget. |

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

### 5. ScanAble (Score: 21/25 — meets Tool threshold)
- **What**: URL → WCAG/EAA compliance PDF report. Automated accessibility audit with actionable fix suggestions.
- **Buyer**: Small business owners, freelancers, web agencies needing compliance documentation
- **Price**: $19/report (pay-per-use)
- **Evidence**: 8,667 ADA lawsuits in 2025, 94.8% of sites fail WCAG. EAA enforcement creates regulatory demand.
- **Competitor gap**: Free tools (WAVE) don't generate reports. Paid tools start at $49+ (OnePageAudit) or $99+ (Audit Base). $19 is cheapest per-report.
- **Edge**: Zero API costs (axe-core is free), >95% margin, simple transactional model

### 6. Acquisition Play (KILLED)
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

### ScanAble
- [ ] 1. Core feature works end-to-end (URL input → axe-core scan → PDF report generation)
- [ ] 2. Landing page (Next.js + Tailwind) with value prop, pricing, CTA
- [ ] 3. Auth (NextAuth.js or guest checkout — transactional tool may use guest checkout)
- [ ] 4. Billing (Stripe Checkout — $19/report, one-time payment)
- [ ] 5. Frontend deployable to Vercel
- [ ] 6. Backend deployable (API routes or separate NestJS if needed)
- [ ] 7. Database migrations run cleanly (if using DB)
- [ ] 8. `.env.example` documents all required environment variables
- [ ] 9. README has setup instructions
- [ ] 10. No hardcoded secrets or obvious security issues

### StubSnap (KILLED)
- N/A
