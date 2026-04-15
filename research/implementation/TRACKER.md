# Implementation Tracker

Last updated: 2026-04-13 (iteration 32)

## Active Ideas

| # | Idea | Type | Folder | Status | Phase | Last Iteration | Blockers |
|---|------|------|--------|--------|-------|---------------|----------|
| 1 | APIDelta — API dependency change monitor | SaaS | projects/apidelta/ | LAUNCHING | Launch C | 2026-04-11 (#32) | All infra ✅. Demo GIF ✅ (on landing page). Pending: HN karma, community launch (8 posts). Hard kill criteria set — see launch log. |
| 2 | ScanAble — Accessibility Report | Tool | projects/scanable/ | LAUNCHING | Launch B | 2026-04-13 (#17) | Google Ads paused — advertiser verification submitted 2026-04-13, awaiting Google approval (1-3 biz days). Review date pushed to ~2026-04-20. |
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

### 1. APIDelta (Score: 22/30 — meets SaaS threshold)
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

### APIDelta (MVP COMPLETE — 2026-04-11)
- [x] 1. Core feature works end-to-end (changelog crawling + AI classification + alerting)
- [x] 2. Landing page (Next.js + shadcn/ui + Tailwind) with value prop, pricing, CTA
- [x] 3. Auth (NextAuth.js v5 — email magic link + GitHub OAuth, session-validated API proxy)
- [x] 4. Billing (Stripe Checkout + webhooks in NestJS — production keys configured)
- [x] 5. Frontend deployable to Vercel
- [x] 6. Backend deployable to Railway (NestJS + Prisma)
- [x] 7. Prisma migrations run cleanly on fresh database
- [x] 8. `.env.example` documents all required environment variables
- [x] 9. README has setup instructions (pnpm install, DB setup, env vars, dev server)
- [x] 10. No hardcoded secrets or obvious security issues (auth hardened 2026-04-11)

### ScanAble (MVP COMPLETE — 2026-04-08)
- [x] 1. Core feature works end-to-end (URL input → axe-core scan → PDF report generation)
- [x] 2. Landing page (Next.js + Tailwind) with value prop, pricing, CTA
- [x] 3. Auth (guest checkout — no accounts needed for transactional tool)
- [x] 4. Billing (Stripe Checkout — $19/report, one-time payment)
- [x] 5. Frontend deployable to Vercel
- [x] 6. Backend deployable (Next.js API routes + @sparticuz/chromium for serverless)
- [x] 7. Database migrations run cleanly (Prisma + Neon PostgreSQL)
- [x] 8. `.env.example` documents all required environment variables
- [x] 9. README has setup instructions
- [x] 10. No hardcoded secrets or obvious security issues

### StubSnap (KILLED)
- N/A

## Launch Progress Logs

### ScanAble — Launch Log
| Date | Action | Status | Notes |
|------|--------|--------|-------|
| 2026-04-08 | MVP complete (10/10 checklist + 10/10 polish) | ✅ | Guest checkout, axe-core scanning, PDF generation, Stripe integration |
| 2026-04-08 | Domain secured: scanable.dev | ✅ | |
| 2026-04-08 | Vercel deployment | ✅ | Connected to Neon DB |
| 2026-04-08 | GA4 analytics setup | ✅ | Property ID 532432963 |
| 2026-04-08 | SEO landing pages built | ✅ | /ada-compliance-checker, /eaa-accessibility-audit, /free-wcag-checker, /wcag-compliance-report, /website-accessibility-audit |
| 2026-04-10 | Google Ads campaign launched | ✅ | Performance Max, $10/day budget, Purchases goal, 10 search themes, 6 sitelinks, GA4 linked |
| 2026-04-10 | Google Ads — learning phase | ⚠️ | Campaign paused — Google requires advertiser verification. Submitted 2026-04-13, awaiting approval (1-3 business days). |
| 2026-04-10 | Stripe production keys | ✅ | Configured in Vercel env vars |
| 2026-04-10 | Resend email integration | ✅ | API key + domain verified |
| 2026-04-10 | Replace stock ad images | ✅ | Product screenshots uploaded to Google Ads |
| 2026-04-10 | End-to-end prod test | ✅ | Payment → scan → email (report@scanable.dev) → PDF download all working. scanable.dev scored 100/100. |
| 2026-04-13 | API subscription billing shipped | ✅ | Paid API tiers (Starter $19/mo, Growth $49/mo, Scale $149/mo) live. Stripe Checkout subscription flow, Customer Portal for plan switching/cancellation, dashboard plan card with usage, webhook lifecycle handling. Tested end-to-end in test mode (upgrade Starter→Growth→Scale). Live Stripe price IDs + portal configured. |
| 2026-04-14 | One-time PDF report repriced $19 → $9 | ✅ | Realigned value vs API tiers ($19 PDF was priced at 1,000 API scans). Inline `price_data` — no Stripe Product change needed, takes effect on next checkout. 26 files updated across pricing cards, CTAs, SEO pages, OG/Twitter images, comparison tables. |
| 2026-04-14 | RapidAPI integration — code ready | ✅ | `POST /api/rapidapi/scan` + `lib/rapidapi-auth.ts` + `public/openapi.json` shipped. Proxy-secret auth, full paid-tier response for all RapidAPI users, no local quota (RapidAPI enforces). Next: create RapidAPI provider account, import spec, set `RAPIDAPI_PROXY_SECRET` in Vercel. |
| — | RapidAPI listing live | 🔄 | TODO: (1) create provider account at rapidapi.com/provider, (2) import `https://scanable.dev/openapi.json`, (3) generate Proxy Secret in RapidAPI dashboard and set `RAPIDAPI_PROXY_SECRET` in Vercel prod env, (4) configure pricing tiers (Basic $9/500, Pro $29/2000, Ultra $99/10000), (5) submit for review. Strategy: discovery channel, funnel power users to direct pricing. |
| — | First organic/ad conversion | 🔄 | Waiting for Google Ads data (target: 1+ conversion by 2026-04-17) |
| — | First API subscription conversion | 🔄 | Paid tiers just launched — awaiting first subscriber |
| — | First RapidAPI subscription | 🔄 | Awaiting listing approval + discovery |

#### Google Ads Campaign Config
- **Type**: Performance Max
- **Budget**: $10/day (~$140 over 2 weeks)
- **Goal**: Purchases (conversion URL: scanable.dev/success)
- **Locations**: US, UK, Canada, Australia + EU (France, Germany, Ireland, Netherlands)
- **Languages**: English
- **Search themes**: WCAG compliance report, website accessibility audit, ADA compliance checker, accessibility report generator, WCAG audit tool, EAA accessibility compliance, website accessibility checker, ADA website compliance, accessibility testing tool, WCAG PDF report
- **Estimated**: 8 weekly conversions at $8 CPA
- **Review date**: 2026-04-17 (7 days post-launch)

### APIDelta — Launch Log
| Date | Action | Status | Notes |
|------|--------|--------|-------|
| 2026-04-08 | Domain secured: apidelta.dev | ✅ | |
| 2026-04-08 | Vercel deployment | ✅ | |
| 2026-04-08 | Neon DB provisioned | ✅ | |
| 2026-04-08 | Railway API confirmed | ✅ | |
| 2026-04-10 | Stripe webhook secret | ✅ | Configured |
| 2026-04-10 | Resend email integration | ✅ | API key + domain verified |
| 2026-04-10 | GitHub OAuth app | ✅ | Created and configured |
| 2026-04-10 | Launch content drafted | ✅ | Show HN, Twitter thread, LinkedIn, 4 Reddit posts, IH post — see apidelta-launch-content.md |
| 2026-04-11 | Solidification sprint | ✅ | Cross-run dedup (SHA-256 content hash), classifier idempotency (aiSummary field), isNew lifecycle, duplicate alert prevention, 6 noise filter patterns, auto-disable after 5 failures |
| 2026-04-11 | Auth hardening | ✅ | API proxy validates session + injects x-team-id header, backend ownership checks, removed exposed evaluate endpoint |
| 2026-04-11 | Landing page honesty | ✅ | Removed false claims (50+ formats, weekly digests, team members, priority support). Honest copy deployed. |
| 2026-04-11 | Data cleanup | ✅ | Deleted 164 duplicate entries, 48 failed crawl runs, 7 noise entries. Disabled 6 broken sources. 108 clean entries remain across 9 active sources. |
| 2026-04-11 | Production dedup verified | ✅ | 3 prod crawls (Cloudflare, Slack, Twilio) — 0 duplicates created. Pipeline is solid. |
| 2026-04-11 | Demo GIF + landing page | ✅ | 9-frame GIF (664KB) on landing page "Product tour" section. Demo mode (?demo=true) for screenshots without backend. |
| 2026-04-11 | HN karma check | ⚠️ | Account `Ignusmart`: 1 karma, 0 comments. BLOCKED — need 50+ karma, 15-20 comments. Target Show HN: ~April 28-May 2. Start commenting now. |
| 2026-04-11 | Launch posts finalized | ✅ | 8 posts ready (social-content.md). False Postman stat removed. Kill criteria updated. Links set. Show HN drafted but blocked on karma. |
| — | Community launch (7 posts excl. HN) | ❌ | Launch day: **2026-04-15 (Tuesday)**. Schedule below. Goal: 5-10 trial signups in 2 weeks. |
| — | Show HN post | ❌ | Blocked on karma. Target: ~April 28-May 2. |
| — | Demand validation review | ❌ | 2 weeks after launch — hard kill criteria below |

#### Kill Criteria (non-negotiable)

| Checkpoint | Date | Metric | Kill if |
|-----------|------|--------|---------|
| Day 14 post-launch | ~2026-04-29 | Trial signups | < 5 signups → kill |
| Day 30 post-launch | ~2026-05-15 | Paying customers | < 2 paying ($49+ MRR) → kill |
| Day 30 post-launch | ~2026-05-15 | Organic interest | Zero inbound, no repeat visits → kill |

#### Launch Schedule (starts 2026-04-15)

| Date | Day | Post | Platform | Time (ET) |
|------|-----|------|----------|-----------|
| Tue Apr 15 | 1 | LinkedIn launch post | LinkedIn | 9 AM |
| Tue Apr 15 | 1 | Twitter launch thread | X | 10 AM |
| Tue Apr 15 | 1 | r/webdev discussion | Reddit | 11 AM |
| Thu Apr 17 | 3 | r/devops discussion | Reddit | 10 AM |
| Thu Apr 17 | 3 | IH launch post | Indie Hackers | 11 AM |
| Fri Apr 18 | 4 | LinkedIn pain-point post | LinkedIn | 9 AM |
| Mon Apr 21 | 7 | Dev.to technical article | Dev.to | 10 AM |
| Tue Apr 22 | 8 | r/programming technical post | Reddit | 10 AM |
| Wed Apr 23 | 9 | Twitter build thread | X | 10 AM |
| Thu Apr 24 | 10 | LinkedIn technical post | LinkedIn | 9 AM |
| ~Apr 28-May 2 | 14-18 | Show HN | HN | 10 AM (if karma 50+) |

**Rules**: Copy-paste from `docs/social-content.md`. Reply to every comment for 4-6 hours after posting. No follow-up posts on the same day.

**Context**: Market research (2026-04-11) found weak demand signals — dead competitors (API Drift Alert, Optic.dev, GetChanges.io), pain point absent from Postman 2025/SO 2024 surveys, free alternatives cover 80% of value (oasdiff, PageCrawl $8/mo, RSS feeds). Product is built and polished — launch costs 2-3 days of posting. Don't invest another engineering hour until organic demand appears. If killed, redirect all time to competitive audits (Code4rena/Sherlock).
