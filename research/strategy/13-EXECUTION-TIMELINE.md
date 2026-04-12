# Master Execution Timeline

## The Complete ScanAble Flywheel Build Order

```
PHASE 0          PHASE 1A              PHASE 1A         PHASE 1A
(NOW)            (Week 1-2)            (Week 3)          (Week 4-5)
                                                     
VALIDATE    →    pSEO Pages       →    API Layer    →    OSS CLI
                                                         
Google Ads       1,000+ domain         API keys          npm package
running          score pages           /api/v1/scan      GitHub repo
                                                        
APIDelta         CMS guides            RapidAPI          GH Actions
launch           Industry pages        listing           template
Apr 15                                                   
                 Comparison            Direct docs       Dev.to posts
Wait for         pages                 + playground      Awesome lists
conversion                                               
                 Sitemap               npm SDK            
$0 eng           generation            (optional)        
effort                                 
                 ~2 weeks              ~1 week            ~1 week

[FROZEN] Security Scan Variant — revisit if ScanAble > $5K/mo
```

## Week-by-Week Plan (starts when Phase 0 validates)

### Prerequisite: Phase 0 Must Pass

| Checkpoint | Date | Condition to proceed |
|-----------|------|---------------------|
| ScanAble first conversion | By ~Apr 24 | At least 1 paid report purchased (ads or organic) |
| APIDelta signup check | Apr 29 | 5+ trial signups (or kill) |
| ScanAble ad spend review | Apr 30 | CPA analysis — if CPA > $19, pause ads immediately |

**If ScanAble gets zero conversions after $300 ad spend**: Skip to pSEO immediately (ads may not work for $19 product, but organic can).

### Week 1-2: Programmatic SEO (highest leverage, zero cost)

| Day | Task | Output |
|-----|------|--------|
| 1 | Fetch Tranco top 1,000 domains | Domain list |
| 1-2 | Build batch preview scanner (cron job) | 1,000 domain scores in DB |
| 3 | Build `app/check/[domain]/page.tsx` with ISR | Dynamic domain pages |
| 4 | Structured data + meta tags + OG images | SEO-ready pages |
| 5 | Auto-generated sitemap.xml | Google indexing |
| 6-7 | CMS guide pages (15) + industry pages (10) | 25 high-intent static pages |
| 8 | Comparison pages (5 "ScanAble vs X") | Competitive SEO |
| 9-10 | Internal linking + submit to Google Search Console | Crawl discovery |

**Deliverable**: 1,050+ indexed pages targeting long-tail keywords.

### Week 3: API Layer

| Day | Task | Output |
|-----|------|--------|
| 1-2 | API key auth + /api/v1/scan endpoint | Working API |
| 3 | Usage metering + quota enforcement | Abuse prevention |
| 4 | Stripe billing for API tiers | Monetization |
| 5 | API docs page + OpenAPI spec | Developer adoption |
| 5 | RapidAPI listing | Discovery channel |

**Deliverable**: Live API at api.scanable.dev + RapidAPI listing.

### ~~Week 4-5: Security Scan Variant~~ — FROZEN

Deprioritized April 2026. Demand weaker than accessibility (no enforcement deadline, free tools more capable in security). Revisit only if ScanAble > $5K/mo and needs cross-sell. See `11-SECURITY-SCAN-PLAN.md`.

### Week 4-5: OSS CLI

| Day | Task | Output |
|-----|------|--------|
| 1 | Extract scanner into npm package | @scanable/cli |
| 2 | CLI interface + terminal formatting | Beautiful output |
| 3 | JSON/CSV output + CI threshold flag | CI/CD ready |
| 4 | README + GIF + GitHub Actions template | Developer docs |
| 5 | Publish to npm + GitHub repo + submit to awesome lists | Distribution |

**Deliverable**: `npx scanable https://example.com` works. Published to npm.

---

## Revenue Milestones

| Milestone | Target Date | Metric |
|-----------|-------------|--------|
| First paid report | Apr 24, 2026 | $19 |
| 10 reports/week | June 2026 | $760/mo |
| First API subscriber | June 2026 | $19-49/mo |
| 100 reports/week | Sept 2026 | $7,600/mo |
| 50 API subscribers | Oct 2026 | $1,500-3,000/mo |
| Combined $10K/mo | Dec 2026 | Reports + API + CLI funnel |

---

## Strategy Documents Index

| Document | File | Contents |
|----------|------|----------|
| Portfolio Strategy | `08-PORTFOLIO-STRATEGY.md` | Master strategy, product architecture, phasing, decision tree, revenue projections |
| API-as-a-Service Plan | `09-SCANABLE-API-PLAN.md` | API design, pricing tiers, RapidAPI listing, distribution, unit economics |
| Programmatic SEO Plan | `10-SCANABLE-PSEO-PLAN.md` | Page types, implementation, keyword targets, traffic projections |
| Security Scan Plan | `11-SECURITY-SCAN-PLAN.md` | What to check, compliance mapping, bundle pricing, PDF template |
| OSS CLI Plan | `12-OSS-CLI-PLAN.md` | CLI features, npm strategy, GitHub distribution, conversion funnel |
| Execution Timeline | `13-EXECUTION-TIMELINE.md` | This file — week-by-week build order |
