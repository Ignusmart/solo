# ScanAble Programmatic SEO Plan

## The Opportunity

Per-domain programmatic pages are a proven SEO play (BuiltWith, downforeveryoneorjustme.com, SecurityHeaders.com) but are **underexploited in accessibility checking**. AccessibilityChecker.org claims 50K+ scans/month but doesn't appear to have persistent, indexed per-domain result pages.

**Demand drivers:**
- ADA Title II deadline: April 24, 2026 (large entities), April 2027 (small)
- EAA enforcement: mandatory across EU since June 2025
- 95.9% of sites fail WCAG (WebAIM Million 2026)
- 5,100+ ADA lawsuits in 2025, avg $25K/case

## Page Types

### Type 1: Domain Score Pages (highest volume)
**URL pattern**: `scanable.dev/check/[domain]`
**Example**: `scanable.dev/check/shopify.com`

**Content**:
- Accessibility score (0-100) with letter grade (A-F)
- Top 5 violations found (teaser — not the full report)
- Severity breakdown bar chart
- "Last scanned: [date]" timestamp
- CTA: "Get Full Report with Fix Suggestions — $19"
- CTA: "Monitor this site monthly — coming soon"

**Target keywords**: "[domain] accessibility", "is [domain] accessible", "[domain] ADA compliance"

**Scale**: Start with top 1,000 most-visited sites (Tranco list). Expand to 10,000, then 100,000.

**Implementation**:
- Nightly cron job: scan top N sites with preview scanner (free, top 5 issues)
- Store results in DB with timestamp
- Next.js ISR pages: regenerate weekly
- Each page has structured data (Schema.org WebSite + Review markup)
- Canonical URLs to prevent duplicate content issues

### Type 2: CMS/Platform Guides (high intent)
**URL pattern**: `scanable.dev/guide/[platform]-accessibility`
**Examples**:
- `scanable.dev/guide/wordpress-accessibility`
- `scanable.dev/guide/shopify-accessibility`
- `scanable.dev/guide/squarespace-accessibility`
- `scanable.dev/guide/wix-accessibility`
- `scanable.dev/guide/webflow-accessibility`
- `scanable.dev/guide/nextjs-accessibility`

**Content**:
- Common accessibility issues specific to that platform
- Average score across sites using that platform (from scan data)
- Platform-specific fix instructions
- CTA: "Scan your [Platform] site now — $19"

**Scale**: 15-20 platforms. Static content with data from scans.

### Type 3: Industry Compliance Pages (buyer intent)
**URL pattern**: `scanable.dev/industry/[vertical]`
**Examples**:
- `scanable.dev/industry/ecommerce-accessibility`
- `scanable.dev/industry/healthcare-accessibility`
- `scanable.dev/industry/government-accessibility` (ADA Title II!)
- `scanable.dev/industry/education-accessibility`
- `scanable.dev/industry/banking-accessibility` (EAA)
- `scanable.dev/industry/legal-accessibility`

**Content**:
- Relevant regulations for that industry
- Average accessibility score for sites in that vertical
- Common violations in that industry
- Case studies / lawsuit examples
- CTA: "Audit your site before the deadline — $19"

**Scale**: 10-15 industries. Static content enriched with scan data.

### Type 4: Regulation Explainers (educational → conversion)
**URL pattern**: `scanable.dev/law/[regulation]`
**Already built**: `/ada-compliance-checker`, `/eaa-accessibility-audit`, `/wcag-compliance-report`

**Expand to**:
- `scanable.dev/law/section-508` (US federal)
- `scanable.dev/law/aoda` (Canada/Ontario)
- `scanable.dev/law/en-301-549` (EU standard)
- `scanable.dev/law/title-ii-deadline-2026` (timely!)

### Type 5: Comparison Pages (competitive SEO)
**URL pattern**: `scanable.dev/compare/[tool-a]-vs-[tool-b]`
**Examples**:
- `scanable.dev/compare/scanable-vs-wave`
- `scanable.dev/compare/scanable-vs-accessibe`
- `scanable.dev/compare/scanable-vs-lighthouse`

**Content**: Feature/pricing comparison tables. "ScanAble vs X" targets people already searching for alternatives.

---

## Implementation Plan

### Phase 1: Domain Score Pages (Week 1-2)

**Day 1-2**: Data pipeline
- Script to fetch top 1,000 domains from Tranco list
- Run preview scan on each (top 5 issues, score)
- Store in `DomainScan` table: domain, score, violations, scannedAt
- Rate limit: ~100 scans/hour (10 second each), 1,000 domains = ~10 hours

**Day 3-4**: Page generation
- Dynamic route: `app/check/[domain]/page.tsx`
- ISR with `revalidate: 604800` (weekly refresh)
- SEO: title tag `"[Domain] Accessibility Score — ScanAble"`, meta description, OG image
- Structured data: Schema.org WebSite type

**Day 5**: Internal linking + sitemap
- Auto-generated sitemap.xml with all domain pages
- Internal links: score pages link to relevant CMS guide and industry page
- Footer: "Recently scanned" list for crawl discovery

**Day 6-7**: CMS guides + industry pages
- 15 CMS guides (mostly static content + platform average scores from data)
- 10 industry pages (static content + industry average scores)

### Phase 2: Expand + Monitor (Week 3-4)

- Expand to 5,000 domains
- Add comparison pages (5-10 "ScanAble vs X" pages)
- Add regulation explainers (5-8 new law pages)
- Monitor Google Search Console for indexing + impressions
- Add internal linking between all page types

### Phase 3: Scale (Month 2-3)

- Expand to 25,000-100,000 domains
- Weekly rescan cron job for all indexed domains
- Add "score history" charts to domain pages (shows improvement/decline)
- Add "submit your site" form for domains not yet scanned
- Email capture: "Get notified when your score changes"

---

## Expected Impact

| Metric | Month 1 | Month 3 | Month 6 | Month 12 |
|--------|---------|---------|---------|----------|
| Indexed pages | 1,050 | 5,100 | 25,100 | 100,100 |
| Organic impressions/mo | 1,000 | 15,000 | 80,000 | 300,000 |
| Organic clicks/mo | 50 | 750 | 5,000 | 20,000 |
| Conversion rate | 0.5% | 1% | 1.5% | 2% |
| Report purchases/mo | 0 | 8 | 75 | 400 |
| Revenue/mo | $0 | $150 | $1,425 | $7,600 |

Conservative estimates. pSEO compounds — each page that ranks brings in traffic for months/years.

---

## Technical Cost

- Scanning 1,000 domains: ~10 hours of Vercel function time
- Scanning 100,000 domains: needs batch processing (not Vercel — use Railway cron or dedicated worker)
- DB storage: ~100 bytes per domain scan = negligible
- ISR pages: served from Vercel CDN after first render = negligible

For 100K+ pages, consider:
- Moving batch scanning to Railway worker (cheaper compute for long-running jobs)
- Using ISR or static generation (not SSR) to keep Vercel costs low
- Caching aggressively — scores don't change fast

---

## When to Build

**Phase 1A, weeks 1-2** (per portfolio strategy). This is the FIRST growth investment after Phase 0 validates. Build before the API layer because:
1. Zero marginal cost (free scans using preview endpoint)
2. Compounds over time (SEO takes months to kick in — start early)
3. Creates the data asset that feeds everything else (API, reports, content)
