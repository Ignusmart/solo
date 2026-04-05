# Implementation Tracker

Last updated: 2026-04-05

## Active Ideas

| # | Idea | Folder | Status | Phase | Last Iteration | Blockers |
|---|------|--------|--------|-------|---------------|----------|
| 1 | DriftWatch — API dependency change monitor | projects/driftwatch/ | BUILDING | Phase 2 | 2026-04-05 (#7) | None |
| 2 | Freight Broker Micro-TMS | projects/freight-tms/ | KILLED | Phase 2 | 2026-04-05 (#7) | Distribution requires high-touch sales to offline buyers (freight brokers). Incompatible with async/automated marketing. |
| 3 | Acquisition Play — buy underperforming extension | projects/acquisition-play/ | KILLED | — | 2026-04-05 (#3) | Sub-$5K market depleted after 3 iterations, 8 marketplaces, 8/8 candidates eliminated. Build > buy at this budget. |

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

## Idea Context (from 13 iterations of research)

### 1. DriftWatch (Score: 17/25 — best surviving idea)
- **What**: Crawls third-party API changelogs, uses AI to classify breaking vs non-breaking changes, alerts engineering teams
- **Buyer**: Engineering leads at B2B SaaS companies (10-100 person teams)
- **Price**: $49-99/mo
- **Evidence**: 52% of devs cite breaking changes as top API concern (Postman 2025)
- **Competitor**: API Drift Alert (early/weak)
- **Edge**: Jobelo's API/security expertise, AI classification, full-stack build speed

### 2. Freight Broker Micro-TMS (Score: 13/25 — timing opportunity)
- **What**: Dead-simple load tracking + rate confirmation + invoicing for 1-3 person brokerages
- **Buyer**: Independent freight brokers (17K-78K in US)
- **Price**: $49-99/mo
- **Evidence**: LoadPilot shut down March 2026, customers orphaned
- **Risk**: AscendTMS free tier, LoadPartner (OSS), domain expertise needed
- **Edge**: Clean UX vs clunky incumbents, modern stack

### 3. Acquisition Play
- **What**: Buy a small underperforming Chrome extension or micro-SaaS ($1-5K), reposition + improve
- **Evidence**: HN case study of 3x revenue from repositioning alone
- **Action needed**: Scout acquisition targets on MicroAcquire, Flippa, or direct outreach

## MVP Completion Checklist (10 items — matches /implement command)

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

### Freight Broker Micro-TMS
- [ ] 1. Core feature works end-to-end (load entry + rate confirmation doc + invoicing)
- [ ] 2. Landing page (Next.js + shadcn/ui + Tailwind) with value prop, pricing, CTA
- [ ] 3. Auth (NextAuth.js or custom JWT — sign up, log in, sessions)
- [ ] 4. Billing (Stripe Checkout + webhooks in NestJS — can be test mode)
- [ ] 5. Frontend deployable to Vercel
- [ ] 6. Backend deployable to Railway/Fly.io (Dockerfile or config)
- [ ] 7. Prisma migrations run cleanly on fresh database
- [ ] 8. `.env.example` documents all required environment variables
- [ ] 9. README has setup instructions (pnpm install, DB setup, env vars, dev server)
- [ ] 10. No hardcoded secrets or obvious security issues

### Acquisition Play
- [ ] 1. Targets identified (3-5 candidates with revenue, price, tech stack)
- [ ] 2. Due diligence on top candidate (traffic, revenue verification, code audit)
- [ ] 3. Acquisition completed (payment + asset transfer)
- [ ] 4. Repositioning plan written (new copy, pricing, distribution)
- [ ] 5. Improvements shipped (code quality, UX, landing page)
