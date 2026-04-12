# ScanAble API-as-a-Service Plan

## The Opportunity

**No WCAG scanning API exists on RapidAPI.** The only competitor is the WAVE API (wave.webaim.org) at $0.025-0.12 per scan, which is:
- Dated interface (basic HTTP GET, limited customization)
- Returns less structured data (no compliance score, no fix suggestions, no severity weighting)
- No modern developer experience (no SDKs, no OpenAPI spec, no playground)

ScanAble already has a scanning engine (axe-core + puppeteer + @sparticuz/chromium) that returns richer data. Exposing it as an API is ~1 week of work.

**ADA Title II deadline: April 24, 2026** — demand spike imminent.

---

## Current ScanAble Technical State

| Component | Status | File |
|-----------|--------|------|
| Scanning engine | ✅ Built | `lib/scanner.ts` — puppeteer + axe-core, WCAG 2.2 AA |
| Full scan endpoint | ✅ Built | `app/api/scan/full/route.ts` — POST, returns violations + score |
| Preview scan endpoint | ✅ Built | `app/api/scan/preview/route.ts` — free, top 5 issues only |
| PDF generation | ✅ Built | `lib/pdf-generator.tsx` — @react-pdf/renderer |
| Rate limiting | ✅ Built | `lib/rate-limit.ts` — IP-based, in-memory, 3 full/hr |
| API key auth | ❌ Not built | Need: key generation, validation middleware, usage tracking |
| Usage metering | ❌ Not built | Need: per-key scan counting, quota enforcement, overage handling |
| Billing integration | ❌ Not built | Need: Stripe subscription tiers for API plans |

---

## What to Build (1-week sprint)

### Day 1-2: API Key Infrastructure
```
POST /api/v1/keys          → Generate API key (tied to Stripe customer)
DELETE /api/v1/keys/:id    → Revoke key
GET /api/v1/usage          → Current period usage stats
```

- API keys: `sk_live_` prefix, SHA-256 hashed in DB, displayed once on creation
- Store in Prisma: `ApiKey { id, hashedKey, userId, plan, createdAt, lastUsedAt }`
- Middleware: validate key from `Authorization: Bearer sk_live_...` header

### Day 3-4: Scan API Endpoint
```
POST /api/v1/scan
  Body: { "url": "https://example.com", "level": "AA" }
  Headers: Authorization: Bearer sk_live_...

Response (JSON):
{
  "url": "https://example.com",
  "scannedAt": "2026-04-15T10:30:00Z",
  "score": 72,
  "level": "AA",
  "summary": {
    "totalViolations": 23,
    "critical": 2,
    "serious": 5,
    "moderate": 12,
    "minor": 4,
    "passCount": 87
  },
  "violations": [
    {
      "id": "color-contrast",
      "impact": "serious",
      "description": "Elements must have sufficient color contrast",
      "wcagCriteria": ["1.4.3"],
      "helpUrl": "https://dequeuniversity.com/rules/axe/4.9/color-contrast",
      "count": 5,
      "nodes": [
        {
          "html": "<p class=\"text-gray-400\">...",
          "selector": "#hero > p:nth-child(2)",
          "failureSummary": "Fix any of the following: Element has insufficient contrast ratio of 3.2:1 (expected 4.5:1)"
        }
      ]
    }
  ],
  "passes": 87,
  "scanDurationMs": 8234
}
```

### Day 5: Usage Metering + Quota Enforcement
- Prisma model: `ApiUsage { id, apiKeyId, period (YYYY-MM), count, limit }`
- Increment on each scan, check quota before running
- Return `429 Too Many Requests` with `X-RateLimit-Remaining` header when quota exceeded
- Overage: either hard-stop or charge per-scan (start with hard-stop, simpler)

### Day 6: Stripe Billing Integration
- Create Stripe Products for each API tier
- Webhook: on subscription created/changed → update plan limits in DB
- Webhook: on subscription canceled → downgrade to free tier
- Usage dashboard page at scanable.dev/dashboard/api

### Day 7: Documentation + RapidAPI Listing
- OpenAPI 3.0 spec (auto-generates docs)
- Interactive playground at scanable.dev/docs/api
- RapidAPI listing (see below)
- npm helper package: `@scanable/sdk` (thin wrapper, optional — can do later)

---

## Pricing Architecture

### Unit Economics

| Item | Cost |
|------|------|
| Vercel function execution (~10s × 1GB) | ~$0.0005/scan |
| Bandwidth (JSON response ~10-50KB) | ~$0.0001/scan |
| Database write (usage log) | ~$0.0001/scan |
| **Total cost per scan** | **~$0.001** |

WAVE API charges $0.025-0.12/scan. ScanAble's cost is 25-120x cheaper.

### Direct API Pricing (api.scanable.dev)

| Tier | Price | Scans/mo | Per-scan | Margin |
|------|-------|----------|----------|--------|
| **Free** | $0 | 100 | — | N/A (acquisition) |
| **Starter** | $19/mo | 1,000 | $0.019 | 94.7% |
| **Growth** | $49/mo | 5,000 | $0.0098 | 89.8% |
| **Scale** | $149/mo | 25,000 | $0.006 | 83.3% |
| **Enterprise** | Custom | 100K+ | Negotiated | — |

**Why this pricing:**
- Free tier is generous (100/mo) → drives adoption and word-of-mouth
- Starter at $19 matches the ScanAble report price → familiar anchor
- Growth at $49 is competitive with WAVE API bulk pricing ($0.025/scan × 5,000 = $125)
- Scale at $149 undercuts WAVE at volume ($0.025 × 25,000 = $625)
- **Key message**: "5x cheaper than WAVE API, 10x more data in the response"

### RapidAPI Pricing (20% commission to RapidAPI)

| Tier | Price | Scans/mo | Your revenue (after 20% cut) |
|------|-------|----------|------------------------------|
| **Free** | $0 | 50 | $0 |
| **Basic** | $9/mo | 500 | $7.20/mo |
| **Pro** | $29/mo | 2,000 | $23.20/mo |
| **Ultra** | $99/mo | 10,000 | $79.20/mo |

**RapidAPI purpose**: Discovery channel only. Push users to direct API for better pricing.

---

## RapidAPI Listing Strategy

### Listing Details

**Name**: ScanAble — WCAG Accessibility Scanner API
**Tagline**: Scan any URL for WCAG 2.2 accessibility violations. Get compliance scores, violation details, fix suggestions, and severity ratings in JSON.

**Category**: Tools (or Data)
**Tags**: accessibility, WCAG, ADA, compliance, web-audit, axe-core, disability

### Description (for RapidAPI listing page)

```
# WCAG Accessibility Scanner API

Scan any URL for WCAG 2.2 Level A/AA accessibility violations.
Returns compliance score (0-100), violations with severity, affected HTML elements,
WCAG success criteria references, and fix suggestions.

## Why ScanAble API?
- **WCAG 2.2 AA**: Latest standard, not outdated WCAG 2.0
- **Rich data**: Compliance score, severity breakdown, HTML snippets, fix suggestions
- **Fast**: Results in 5-15 seconds per page
- **Powered by axe-core**: Industry-standard accessibility engine (used by Microsoft, Google, Deque)
- **5x cheaper than WAVE API** at scale

## Use Cases
- CI/CD accessibility testing (fail builds on critical violations)
- Agency bulk auditing (scan client portfolios)
- SaaS platforms (embed accessibility scores in your product)
- Compliance monitoring (track scores over time)
- SEO tools (accessibility signals affect rankings)

## Response includes:
- Overall compliance score (0-100)
- Violation count by severity (critical, serious, moderate, minor)
- Each violation: rule ID, description, WCAG criteria, impact, affected nodes with HTML + CSS selectors
- Pass count (rules that passed)
- Scan duration
```

### Competitive Positioning on RapidAPI

| Feature | WAVE API | ScanAble API |
|---------|----------|-------------|
| WCAG version | 2.0/2.1 | **2.2** (latest) |
| Compliance score | No | **Yes (0-100)** |
| Fix suggestions | Limited | **Detailed per violation** |
| Severity weighting | Basic | **Weighted scoring** |
| HTML snippets | Yes | **Yes + CSS selectors** |
| Price (1,000 scans) | $25-40 | **$19** |
| Price (10,000 scans) | $250 | **$99** |
| Response format | JSON/XML | **JSON + OpenAPI spec** |

---

## Distribution Plan (beyond RapidAPI)

### Channel 1: RapidAPI Marketplace
- List with free tier for discovery
- Optimize listing for "accessibility API", "WCAG API", "ADA compliance API"
- Goal: 50-100 free tier signups → 5-10% conversion to paid

### Channel 2: Direct API (api.scanable.dev)
- Landing page with interactive playground (paste URL, see results live)
- OpenAPI spec for auto-generated client libraries
- Better pricing than RapidAPI (no 20% cut)
- Blog post: "How to add accessibility testing to your CI/CD pipeline in 5 minutes"

### Channel 3: npm Package
- `npm install @scanable/node` (thin SDK wrapper)
- README example: 5 lines to scan a URL
- Downloads → GitHub stars → SEO → organic signups
- Link to hosted API in README for those who don't want to self-host

### Channel 4: Integration Guides
- "Add WCAG scanning to GitHub Actions" (blog post + example workflow)
- "Lighthouse + ScanAble: Complete accessibility CI" (blog post)
- "How to audit 1,000 pages for WCAG compliance" (agency-focused)
- "ScanAble API vs WAVE API: Feature and pricing comparison" (competitive SEO)

### Channel 5: Developer Communities
- Post on Dev.to, Hashnode, Reddit r/webdev, r/accessibility
- Show HN: "I built an API for WCAG accessibility scanning"
- Product Hunt launch (API tools category)

### Channel 6: Apify Actor (bonus distribution)
- Publish ScanAble as an Apify Actor (web scraping marketplace)
- Apify already has accessibility scanners but ScanAble's scoring is differentiated
- Different audience: data extraction / bulk processing users

---

## Revenue Projections

### Conservative (organic growth, no paid marketing)

| Month | Free users | Paid users | MRR |
|-------|-----------|------------|-----|
| 1 | 20 | 0 | $0 |
| 2 | 50 | 2 | $38 |
| 3 | 100 | 5 | $145 |
| 6 | 300 | 20 | $680 |
| 12 | 800 | 60 | $2,100 |

### With Active Distribution (blog posts, PH launch, RapidAPI featuring)

| Month | Free users | Paid users | MRR |
|-------|-----------|------------|-----|
| 1 | 50 | 1 | $19 |
| 2 | 150 | 5 | $145 |
| 3 | 300 | 15 | $500 |
| 6 | 800 | 50 | $1,800 |
| 12 | 2,000 | 150 | $5,500 |

### Revenue Stacking (API + Web App Reports)

| Source | Month 6 | Month 12 |
|--------|---------|----------|
| Web app reports ($19 each) | $1,500 | $4,000 |
| API subscriptions | $1,800 | $5,500 |
| Security scan variant | $500 | $2,000 |
| **Total ScanAble revenue** | **$3,800** | **$11,500** |

---

## Technical Decisions

### API versioning
- URL-based: `/api/v1/scan` (simple, clear)
- Version in response headers too

### Authentication
- API key in `Authorization: Bearer sk_live_...` header
- Keys generated via dashboard, hashed with SHA-256 in DB
- No OAuth complexity — API keys are standard for developer APIs

### Rate limiting
- Per-key limits based on plan tier
- Sliding window (not fixed) for better UX
- Headers: `X-RateLimit-Limit`, `X-RateLimit-Remaining`, `X-RateLimit-Reset`

### Error responses
```json
{
  "error": {
    "code": "QUOTA_EXCEEDED",
    "message": "Monthly scan limit reached. Upgrade at scanable.dev/pricing",
    "upgradeUrl": "https://scanable.dev/pricing"
  }
}
```

### Webhook support (Phase 2)
- For large scans (> 30s), return `202 Accepted` with callback
- POST results to customer's webhook URL when scan completes
- Useful for bulk/batch scanning workflows

---

## Implementation Priority

| Priority | What | Effort | Revenue Impact |
|----------|------|--------|----------------|
| P0 | API key auth + /api/v1/scan endpoint | 2 days | Enables everything |
| P0 | Usage metering + quota enforcement | 1 day | Prevents abuse |
| P1 | Stripe billing for API tiers | 1 day | Monetization |
| P1 | API docs page (OpenAPI + playground) | 1 day | Developer adoption |
| P1 | RapidAPI listing | 0.5 day | Discovery channel |
| P2 | npm SDK package | 1 day | Developer convenience |
| P2 | GitHub Actions example | 0.5 day | CI/CD adoption |
| P3 | Webhook support | 1 day | Bulk scanning |
| P3 | Apify Actor | 0.5 day | Bonus distribution |

**Total P0+P1: 5.5 days. Ship in 1 week.**

---

## When to Build This

**NOT NOW.** Per portfolio strategy (08-PORTFOLIO-STRATEGY.md):
1. First: validate that people pay for ScanAble reports (Phase 0, running now)
2. Second: build pSEO pages (Phase 1A, if validated)
3. Third: build API layer (Phase 1A, week 3)

Building the API before validating the core product is premature optimization. But the plan is ready to execute the moment Phase 0 validates.
