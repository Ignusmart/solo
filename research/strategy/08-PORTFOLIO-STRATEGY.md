# Portfolio Strategy — April 2026

## The Thesis

The software market isn't dead — the "find an empty niche" strategy is dead. After 330+ ideas across SaaS, tools, and agent models, the lesson is clear: **winners in 2026 aren't single products in empty niches. They're portfolios where one technical investment powers multiple revenue channels.**

Marc Lou ($1M/yr, solo): 4 interconnected products, each $10-30K/mo.
Plausible ($3.1M): OSS core → hosted cloud → organic distribution.
IPinfo (1.95T requests/yr): Single API, usage-based pricing, zero churn.

**Our play**: Two validated scanning/monitoring engines (ScanAble + APIDelta) → wrap each in 4-5 business model layers → let them compound.

---

## Current State (updated April 18, 2026)

| Product | Stage | Revenue | Signal Strength |
|---------|-------|---------|-----------------|
| **ScanAble** | LAUNCHING — Google Ads running ($10/day since Apr 10) | $0 (waiting for first conversion) | STRONG — 8,667 ADA lawsuits, 94.8% WCAG failure rate, EAA enforcement, zero API costs, >95% margin |
| **APIDelta** | LAUNCHING — community launch Apr 15 | $0 (pre-launch) | WEAK — dead competitors, absent from surveys, free alternatives cover 80% |
| **Competitive audits & bounties** | Active via `claude-bug-bounty` harness | **$0 paid across ~170 projects** as of 2026-04-18; 6 submissions pending (ssvnetwork ESCALATED 2026-04-17) | **UNDER REVIEW** — target-saturation problem, not harness failure. See `memory/project_bounty_roi_warning.md` |

**Critical dates:**
- Apr 17: ScanAble Google Ads review (7 days learning)
- Apr 15: APIDelta community launch (8 posts over 10 days)
- Apr 29: APIDelta kill checkpoint (< 5 signups → kill)
- May 15: APIDelta hard kill (< 2 paying → kill)

---

## The Portfolio Architecture

```
┌─────────────────────────────────────────────────────┐
│                  SOLO PORTFOLIO                      │
│                                                     │
│  ┌──────────────┐          ┌──────────────┐        │
│  │  ScanAble    │          │  APIDelta    │        │
│  │  (compliance │          │  (monitoring │        │
│  │   scanning)  │          │   engine)    │        │
│  └──────┬───────┘          └──────┬───────┘        │
│         │                         │                 │
│    ┌────┼────┐              ┌────┼────┐            │
│    │    │    │              │    │    │            │
│    ▼    ▼    ▼              ▼    ▼    ▼            │
│  Web  API  pSEO          Web  pSEO  Audit        │
│  App  SaaS Pages         App  Pages  Report      │
│  $19  /scan  Free→       $49  Free→  $99-199    │
│  /rpt usage  convert     /mo  convert  one-time  │
│         │                         │                 │
│    ┌────┼────┐              ┌────┘                 │
│    │    │    │              │                       │
│    ▼    ▼    ▼              ▼                       │
│  OSS  Sec   Bundle       OSS                      │
│  CLI  Scan  Pack         Core                     │
│  npm  $29   $39          GitHub                   │
│       /rpt               stars                     │
│                                                     │
│  ┌──────────────┐          ┌──────────────┐        │
│  │  Future #3   │          │  Content     │        │
│  │  (next scan  │          │  (audience   │        │
│  │   product)   │          │   building)  │        │
│  └──────────────┘          └──────────────┘        │
└─────────────────────────────────────────────────────┘
```

---

## Product 1: ScanAble (Compliance Scanning Engine)

### Why ScanAble is the portfolio anchor

ScanAble has the strongest fundamentals of anything found across 330+ ideas:
- **Compliance-gated**: ADA/EAA enforcement creates LEGAL requirement to buy
- **Zero API costs**: axe-core is free/open-source
- **>95% margin**: no AI inference, no cloud processing costs
- **Simple value exchange**: URL in → PDF out → $19 paid
- **The scanning engine is reusable**: same infra can scan for different things

### Layer 1: Web App (DONE)
- scanable.dev live, Stripe integrated, Google Ads running
- $19/report, guest checkout, no accounts needed
- **Metric to watch**: first conversion by Apr 17

### Layer 2: Programmatic SEO Pages
- **What**: Generate thousands of pages targeting long-tail keywords
- **Pages**:
  - `scanable.dev/check/[domain]` — "Is [domain] accessible?" (e.g., /check/shopify.com)
  - `scanable.dev/cms/[platform]` — "[Platform] Accessibility Guide" (WordPress, Shopify, Squarespace, Wix)
  - `scanable.dev/industry/[vertical]` — "Accessibility for [Restaurants/Lawyers/eCommerce]"
  - `scanable.dev/law/[regulation]` — "ADA vs EAA: What You Need to Know"
- **How**: Crawl top 1,000 Alexa sites, run free scans, publish scores with "Get Full Report" CTA
- **Effort**: 1-2 weeks
- **When**: After first paying customer confirms model works (Phase 1)
- **Expected impact**: 5,000-50,000 organic visits/mo within 3-6 months

### Layer 3: API as a Service
- **What**: RESTful API — `POST /api/v1/scan` with URL, get WCAG violations back as JSON
- **Pricing**: Free tier (50 scans/mo), $29/mo (1,000 scans), $99/mo (10,000 scans)
- **Buyers**: Web agencies running bulk audits, CI/CD integrations, other SaaS tools
- **Distribution**: RapidAPI marketplace, API directories, dev blog posts, npm package
- **Effort**: 1 week (scanning endpoint exists, add API key auth + usage metering)
- **When**: Phase 2 (after pSEO is driving organic traffic)

### Layer 4: Security Scan Variant — FROZEN
- **What**: Same scanning model but for web security posture
- **Checks**: Security headers (CSP, HSTS, X-Frame-Options), SSL/TLS config, mixed content, exposed secrets in HTML, cookie flags, CORS misconfiguration
- **Pricing**: $29/report standalone, or **$39 bundle** (Accessibility + Security)
- **Status**: FROZEN (April 2026). Demand is weaker than accessibility — no enforcement deadline, free tools are more capable in security than in a11y. Revisit only if ScanAble hits $5K+/mo and needs a cross-sell lever. See `11-SECURITY-SCAN-PLAN.md` for full rationale.

### Layer 5: OSS CLI Tool
- **What**: `npx scanable https://example.com` — free accessibility scan in terminal
- **Publish**: npm package, GitHub repo
- **Upsell**: "Want a PDF report? Visit scanable.dev" in terminal output
- **Distribution**: GitHub stars → dev community adoption → organic conversions
- **Effort**: 1 week (extract scanning logic into standalone package)
- **When**: Phase 3 (after API layer proves developer demand exists)

### ScanAble Revenue Ceiling (realistic)

| Layer | Revenue/mo | Timeline |
|-------|-----------|----------|
| Web app (10 reports/day) | $5,700 | Month 3-6 |
| pSEO traffic (2% conversion) | Included above | Month 4-8 |
| API subscriptions (50 customers) | $2,500 | Month 6-12 |
| Security variant (5 reports/day) | $4,350 | Month 6-12 |
| **Realistic total** | **$8-12K/mo** | **Month 12** |

---

## Product 2: APIDelta (Monitoring Engine)

### Honest assessment

APIDelta has WEAKER demand signals than ScanAble:
- Dead competitors (API Drift Alert, Optic.dev, GetChanges.io)
- Pain point absent from Postman 2025 / Stack Overflow 2024 surveys
- Free alternatives cover 80% of value (oasdiff, RSS feeds, PageCrawl $8/mo)

**Strategy**: Invest zero additional engineering. Launch with existing content. Validate or kill by May 15. If validated, THEN build flywheel layers.

### Layer 1: Web App (DONE — launching Apr 15)
- apidelta.dev live, launch schedule set
- Kill criteria: 5 signups by Apr 29, 2 paying by May 15

### Layer 2: Programmatic SEO (ONLY if validated)
- **Pages**:
  - `apidelta.dev/api/[name]` — "[API Name] Changelog & Reliability History"
  - `apidelta.dev/compare/[a]-vs-[b]` — "Stripe vs Braintree API Stability"
  - `apidelta.dev/status/[api]` — "[API] Recent Breaking Changes"
- **Data source**: APIDelta's own crawling data becomes the content
- **Effort**: 2 weeks
- **When**: ONLY if kill criteria pass (May 15+)

### Layer 3: One-Time API Dependency Health Report
- **What**: Submit your package.json/requirements.txt → get scored dependency risk report
- **Checks**: Breaking change history, deprecation signals, maintainer activity, license risk
- **Pricing**: $99-199/report (one-time, no subscription commitment)
- **Purpose**: Lead gen for APIDelta subscription + standalone revenue
- **Effort**: 1-2 weeks
- **When**: Phase 2 (after subscription model validated)

### Layer 4: OSS Change Detection Core (CONTINGENT)
- Open source the changelog crawling + diffing engine
- Other developers use it → contribute connectors → grow ecosystem
- Hosted APIDelta for alerting/team features/AI classification
- Depends on having real adoption and community interest

### APIDelta Revenue Ceiling (IF validated)

| Layer | Revenue/mo | Timeline |
|-------|-----------|----------|
| Subscriptions (40 teams × $49) | $1,960 | Month 6-12 |
| pSEO → conversions | Included above | Month 8-14 |
| One-time reports (3/week) | $1,200-2,400 | Month 8-14 |
| **Realistic total** | **$3-4K/mo** | **Month 12-14** |

---

## Product 3+: Future Scan Products (Same Engine, Different Checks)

If ScanAble's model proves out (compliance audit → PDF report → pay-per-use), the scanning engine becomes a PLATFORM for launching new audit products. Each shares: Next.js + serverless scanning + Stripe + PDF generation + pSEO pages.

| Potential Product | Compliance Driver | Margin | Effort | Priority |
|-------------------|-------------------|--------|--------|----------|
| Security Posture Report | SOC 2, cyber insurance | High (no API cost) | 2 weeks | HIGH — strongest compliance case after accessibility |
| Performance Report (CWV) | Google ranking signal | High | 1 week | LOW — Lighthouse/GTmetrix are free and excellent |
| Privacy Compliance Scan | GDPR, CCPA | Medium (some crawling cost) | 2 weeks | MEDIUM — free tools exist but no PDF report model |
| SEO Technical Audit | Business value, not compliance | Medium | 2 weeks | LOW — extremely crowded, Screaming Frog is powerful + free |

**Rule**: Only build scan variants where there's a COMPLIANCE/LEGAL driver that creates pricing power. Performance and SEO audits are "nice to have" — they don't survive the "free is good enough" test.

---

## Portfolio Interconnections

### Cross-promotion
- ScanAble checkout success page → "Also monitor your API dependencies with APIDelta"
- APIDelta dashboard sidebar → "Run a compliance audit with ScanAble"
- pSEO pages link between products for SEO juice

### Shared infrastructure
- Both use: Vercel, Neon DB, Stripe, Resend, Next.js, Tailwind
- Scanning engine architecture is reusable
- PDF report generation pipeline is reusable
- API key auth + usage metering (once built) is reusable

### Shared audience
- Both target engineering teams and web professionals
- Content marketing overlaps (dev blogs, Reddit communities, HN)
- Email list from one product promotes the other

### Data flywheel
- ScanAble scans → populate pSEO pages → drive traffic → more scans
- APIDelta crawls → populate changelog pages → drive traffic → more subscribers
- Each scan/crawl makes the data asset more valuable

---

## Sequencing: What Happens When

### Phase 0: VALIDATE (Now — May 15, 2026)
**Goal**: Prove people will pay. Zero new engineering.

| Product | Action | Effort | Kill Criteria |
|---------|--------|--------|---------------|
| ScanAble | Google Ads running. Monitor conversions. | 0 hours (wait) | $0 revenue after $300 ad spend → pause ads, pivot to organic |
| APIDelta | Community launch Apr 15. Post 8x in 10 days. | 8-10 hours (posting + engagement) | < 5 signups by Apr 29 → kill |
| Audits | Continue Code4rena/Sherlock | Primary income | — |

**Decision point (May 15):**
- ScanAble converts → Phase 1A (double down on ScanAble)
- APIDelta converts → Phase 1B (grow APIDelta)
- Both convert → Phase 1A + 1B in parallel
- Neither converts → Phase 1C (pivots below)

### Phase 1A: ScanAble Growth Sprint (May-June 2026)
**Trigger**: At least 1 paid conversion from Google Ads OR organic.

| Week | Action | Effort |
|------|--------|--------|
| 1-2 | Build programmatic SEO page generator (1,000+ "[domain] accessibility score" pages) | 2 weeks |
| 3 | Launch API endpoint with free tier + RapidAPI listing | 1 week |
| 4 | Security scan variant (same infra, new checks, bundle pricing) | 1-2 weeks |
| 5-6 | OSS CLI tool (npm publish + GitHub repo + README) | 1 week |
| 7-8 | Content marketing — 4 blog posts targeting "WCAG compliance 2026", "EAA accessibility guide", "ADA website requirements", "accessibility audit checklist" | 1-2 weeks |

**Target by end of Phase 1A**: 10+ reports/day, $6K+/mo run rate

### Phase 1B: APIDelta Growth (May-June 2026)
**Trigger**: 5+ signups AND 2+ paying customers by May 15.

| Week | Action | Effort |
|------|--------|--------|
| 1-2 | Build pSEO changelog pages for top 50 APIs | 2 weeks |
| 3 | One-time API Health Report product | 1-2 weeks |
| 4-6 | Content marketing — technical blog posts + Show HN (if karma sufficient) | 2 weeks |

**Target by end of Phase 1B**: 20+ subscribers, $1K+/mo MRR

### Phase 1C: Pivot Plays (if neither validates)
**Trigger**: Zero conversions after $300 ScanAble ad spend AND APIDelta killed.

| Option | What | Why |
|--------|------|-----|
| **ScanAble organic pivot** | Kill ads, invest in pSEO + OSS CLI for organic distribution | Paid ads may not work for $19 product (CPA too high), but organic could |
| **ScanAble API-first pivot** | Skip consumer web app, go API-first for developer integrations | Developer willingness to pay may exceed small business owner WTP |
| **Security scan standalone** | Launch security posture report as separate product | Different buyer (CTO/IT), different compliance driver (SOC 2), may convert better |
| **Portfolio content play** | Build audience with technical content (blog/newsletter), monetize later | Longer timeline but eliminates product-market-fit risk by leading with audience |

### Phase 2: Portfolio Expansion (July-August 2026)
**Trigger**: Either product at $3K+/mo.

- Launch security scan variant (if not done in Phase 1A)
- Cross-promotion between products
- Explore course/educational content (monetize expertise)
- Consider open-sourcing one scanning engine for distribution

### Phase 3: Compounding (Sept-Dec 2026)
**Trigger**: Combined portfolio at $8K+/mo.

- Dedicated API product (all scans unified under one API)
- White-label scanning for agencies
- Consider raising prices or adding team tiers
- Evaluate whether to build Product #3 or optimize existing

---

## Revenue Model (Conservative)

| Quarter | ScanAble | APIDelta | Audits | Total |
|---------|----------|----------|--------|-------|
| Q2 2026 (now) | $0-500 (validating) | $0-200 (validating) | $3-5K+ | $3-5K+ |
| Q3 2026 | $1-3K (pSEO + API ramping) | $0-1K (if alive) | $3-5K+ | $4-9K |
| Q4 2026 | $3-8K (multi-layer) | $1-3K (if alive) | $3-5K+ | $7-16K |
| Q1 2027 | $5-12K (portfolio mature) | $2-4K (if alive) | $3-5K+ | $10-21K |

**Conservative floor**: $7K/mo by Q4 2026 (audits + ScanAble organic growth)
**Optimistic ceiling**: $16-21K/mo by Q1 2027 (full portfolio firing)

---

## Decision Framework

```
                    ┌─ ScanAble converts? ─┐
                    │                       │
                   YES                      NO
                    │                       │
            ┌── Phase 1A ──┐        ┌── Try organic? ──┐
            │   pSEO       │        │                   │
            │   API        │       YES                  NO
            │   SecScan    │        │                   │
            │   OSS CLI    │    pSEO + OSS         Pivot to
            └──────────────┘    (3 months)      security scan
                                    │           or API-first
                                    │
                              Converts?
                              YES → Phase 1A
                              NO → content play

                    ┌─ APIDelta converts? ─┐
                    │                       │
                   YES                      NO
                    │                       │
            ┌── Phase 1B ──┐          KILL.
            │   pSEO       │     Redirect time to
            │   Health rpt │     audits + ScanAble.
            │   Content    │
            └──────────────┘
```

---

## Hard Rules

1. **No new engineering until validation.** Both products are LAUNCHING. The next dollar comes from posting, not coding.
2. **ScanAble gets priority over APIDelta.** Stronger signals, better unit economics, compliance-gated moat.
3. **Kill fast, redirect faster.** If APIDelta fails kill criteria by May 15, immediately redirect all time to ScanAble growth + competitive audits.
4. **Every new product must reuse existing infra.** No new tech stacks, no new deployment pipelines. Same Vercel + Neon + Stripe + Next.js + PDF engine.
5. **pSEO before paid ads for low-ticket items.** Google Ads for $19 products may not have viable CPA. Organic/pSEO is the sustainable play.
6. **Competitive audits as "floor" is under review.** Originally framed as proven income at ≥50% time. As of 2026-04-18, `claude-bug-bounty` has produced $0 paid across ~170 projects — primarily a target-saturation problem (mature Immunefi/Sherlock/Cantina programs with 5-20 prior audits). Do not treat audits as a guaranteed floor until at least one of the 6 pending submissions pays. Decision gate: ssvnetwork ESCALATED (2026-04-17) outcome — if it pays, restore floor; if it rejects, reallocate time toward products.
7. **Audience compounds.** Every blog post, every HN comment, every Reddit engagement builds the distribution muscle. Products come and go; audience persists.
