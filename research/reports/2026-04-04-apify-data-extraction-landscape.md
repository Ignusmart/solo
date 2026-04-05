# Apify Data Extraction & MCP Server Landscape — April 2026

## Platform Overview

- **Apify revenue**: $13.3M (Oct 2024), up from $6.4M in 2023 (~108% YoY growth)
- **Total Actors in Store**: ~23,000+ (as of April 2026)
- **Monthly active users**: 50,543 (Oct 2024), up from 20,843 (Jan 2024) — 142% growth
- **130K+ monthly signups**, 36K+ active developer community
- **Actor runs**: 37M by Oct 2024 (doubled since 2023)
- **API calls**: 6.8B (2024), up from 3.6B (2023)
- **$596K paid out to developers in December 2025 alone**
- **Many developers earn $3K+/month**; top independent creators earn **$10K+/month**

---

## 1. Top-Earning Actors & Categories

### Tier 1: Social Media Scrapers (DOMINANT)

| Actor | Users | Rating | Notes |
|-------|-------|--------|-------|
| Instagram Scraper (apify) | ~179K | 4.59 | Highest user count in store |
| TikTok Scraper (clockworks) | ~92K | 4.66 | clockworks dominates TikTok niche |
| Instagram Profile Scraper | ~86K | — | |
| Instagram Post Scraper | ~67K | — | |
| Instagram Reel Scraper | ~52.5K | — | |
| Facebook Posts Scraper | ~35.7K | 4.56 | |
| TikTok Data Extractor (clockworks) | ~33K | 4.80 | |
| Instagram Hashtag Scraper | ~31K | — | |
| Facebook Pages Scraper | ~29.9K | 4.57 | |
| Tweet Scraper V2 (apidojo) | ~26K | 3.80 | Lower rating = opportunity? |
| TikTok Comments Scraper (clockworks) | ~17K | 4.89 | |
| Facebook Comments Scraper | ~17.5K | 4.46 | |

### Tier 2: Maps & Local Business

| Actor | Users | Rating |
|-------|-------|--------|
| Google Maps Search | ~193K | 4.8 |

Google Maps is the single most-used actor on the entire platform.

### Tier 3: E-commerce

- Amazon Product Scraper, Amazon Reviews Scraper, eBay Items Scraper, Shopify Scraper, Etsy Scraper
- No specific user counts published, but e-commerce is a major category
- Product pricing is the #1 use case for web scraping globally (34.8% of all scraping activity)

### Tier 4: Lead Generation & B2B

- LinkedIn scrapers (profiles, jobs, companies)
- Email finders and enrichment tools
- Lead scrapers with email are "rising stars" in 2026

### Category Revenue Estimates (inferred from pricing)

At $1-10 per 1,000 results (the typical range), actors with 50K+ users doing regular runs can generate:
- Top social media actors: likely **$5K-$20K/month** each
- Google Maps actor: possibly **the single highest earner** given 193K users

---

## 2. Oversaturated Niches (AVOID or DIFFERENTIATE HARD)

### Red Zone — Extremely Crowded

**Social Media Scrapers**
- Instagram: 5+ major actors, 179K users on the leader
- TikTok: clockworks has a near-monopoly with multiple actors
- Facebook: 3+ well-established actors
- Twitter/X: Multiple actors, but leader only has 3.8 rating (possible quality gap)
- YouTube: Multiple competing scrapers
- Reddit: Multiple options available

**Google Maps/Places**: 193K users on the leader; extremely hard to compete

**Generic Web Crawlers**: Fast Website Content Crawler and similar tools — commodity market

**Amazon Scrapers**: Product + Reviews scrapers are well-established

### Yellow Zone — Competitive but Gaps Exist

**LinkedIn**: Multiple job scrapers exist, but scraping LinkedIn is technically challenging (login walls, rate limits). Quality differentiation possible.

**E-commerce Price Monitoring**: Several actors exist (Price Monitor, Competitor Price Tracker) but the space keeps growing (34.8% of all scraping is product pricing).

**App Store Reviews**: ~7+ Google Play review scrapers visible. Getting crowded.

---

## 3. Underserved Niches (OPPORTUNITY ZONES)

### Strong Opportunities

**Government & Regulatory Data**
- SEC EDGAR: Only a handful of actors (constant_quadruped, fortuitous_pirate, ai_solutionist, scraped). Most are recent $1M Challenge entries, meaning they're NEW and unproven. The SEC filing space has high-value users (hedge funds, compliance teams, legal). AI-powered summaries of filings are a premium differentiator.
- FDA data: No specific FDA scraper found in searches
- Federal Register: One compliance data scraper exists (fortuitous_pirate) covering EPA/OSHA. Vast untapped space.

**Court Records & Legal**
- Only 2 actors found: court-records-scraper (automation-lab) for federal cases, and ecourts-case-scraper (codingfrontend) for Indian courts
- Massive unmet demand: legal research, due diligence, litigation monitoring
- State court systems are COMPLETELY uncovered

**Patent & Trademark Intelligence**
- USPTO Patent Search Scraper (fortuitous_pirate) and Patent Trademark Search (hanamira) exist but are very new
- Patent landscape analysis is a high-value niche (law firms, R&D teams pay premium)
- Few actors, low user counts — early mover advantage

**Academic/Research Paper Extraction**
- arXiv: ~5 scrapers exist but all appear to be $1M Challenge entries (new, untested)
- PubMed: 1 scraper found
- Google Scholar: 2 scrapers found
- Semantic Scholar, SSRN, bioRxiv: NO scrapers found
- The AI/RAG boom means demand for academic data is surging

### Moderate Opportunities

**Real Estate**
- Zillow scrapers exist and are actively maintained
- Realtor.com: A few actors ($3/1K records)
- International real estate (Rightmove UK, Idealista Spain, etc.): gaps exist
- Real estate AGENT data scrapers are newer and less competitive

**Job Board Aggregation**
- LinkedIn Jobs: 5+ scrapers (competitive)
- Indeed: Active scraper exists with rental pricing
- However: Multi-platform unified job search is a rising star category
- Glassdoor, ZipRecruiter combined scraper exists but is newer
- Niche job boards (WeWorkRemotely, AngelList, BuiltIn, Dice, etc.): VERY underserved

**Review Aggregation**
- Google Play reviews: 7+ scrapers (crowded)
- G2.com reviews: Rising star, only 1-2 actors
- Trustpilot, Capterra, App Store (iOS): fewer options
- Cross-platform review aggregation (unified API across G2 + Capterra + Trustpilot): GAP

**B2B Supplier/Manufacturer Data**
- ThomasNet scraper is a rising star (500 users, 4.8 rating, $5/1K results)
- Alibaba, IndiaMart, GlobalSources: underserved
- Industrial/supply chain data is high-value

---

## 4. Pay-Per-Event (PPE) Model — How It Works

### Mechanics
- Creator defines custom events in code via JS/Python SDK
- Events fire when specific actions occur (page scraped, result returned, API called)
- User is charged per event; creator gets **80% of revenue**
- Formula: `profit = (0.8 * revenue) - platform_usage_costs`
- Alternative: shift compute costs to user, then `profit = 0.8 * revenue` cleanly

### Default Event
- `apify-actor-start` fires on every run
- Default price: $0.00005 ($0.05 per 1,000 starts)
- Apify covers compute for first 5 seconds of every run

### Typical Pricing Tiers

| Tier | Price/Event | Use Case |
|------|-------------|----------|
| Budget | $0.001–$0.05 | Simple lookups, bulk ops, DNS queries |
| Standard | $0.05–$0.30 | Website scraping, contact extraction |
| Premium | $0.30–$1.00+ | Multi-source intelligence, deep analysis |

### Pricing by Category

| Category | $/result | Value Saved |
|----------|----------|-------------|
| Email finder | $0.05–$0.10 | 3–5 min/lead |
| Contact scraper | $0.10–$0.20 | 10–15 min/site |
| Waterfall enrichment | $0.15–$0.30 | 20–30 min/contact |
| Intelligence reports | $0.50–$1.00 | 1–2 hours/report |

### The 3-5x Rule
Price should be 3-5x your compute cost per result. For most standard tools, this means **$0.05-$0.20 per result**.

### Key Data Points
- PPE actors have **3.2x higher user retention** than rental-priced actors
- Raising price from $0.03 to $0.12/result: volume dropped 15%, **revenue increased 180%**
- Mid-range pricing beats rock-bottom pricing in total revenue
- **Fewer than 12% of published actors have ANY pricing configured** — the rest earn $0

### Timeline
- **April 1, 2026**: No new rental actors can be published
- **October 1, 2026**: All rental actors retired, migrated to PPE

---

## 5. What Makes an Actor Succeed vs Fail

### Success Factors

1. **Actually set PPE pricing** — 88% of actors earn nothing because they never configured pricing
2. **90%+ success rate** on runs — anything below 85% drives users away
3. **Regular maintenance** — track site changes, respond to issues quickly
4. **Clear README** with use cases, input/output examples, and a logo
5. **Value-based pricing** — charge for time saved, not compute used
6. **Actor start event** at $0.005-$0.01 generates ~$30/month from 3K runs alone
7. **Niche focus** — if 50+ actors exist with leaders at 50K+ users and you can't articulate differentiation, pivot
8. **Fast execution** — rising stars use Cheerio/HTTP requests instead of headless browsers

### Failure Patterns

1. **No pricing configured** (most common)
2. **Underpricing by 3-5x** — attracts price-sensitive users who churn
3. **Charging before data delivery** ("phantom charges destroy reputation faster than anything")
4. **Not updating when target sites change** — users leave immediately
5. **Competing head-on with Apify-maintained actors** — they track changes faster and have official support
6. **Ignoring the 14-day notice period** — start pricing from day one, not after publication

### Earnings Distribution (Power Law)
- Top creators: **$10K+/month**
- Successful creators: **$3K+/month**
- Average monetized actor: likely $100-500/month (inferred)
- 88% of actors: **$0/month** (no pricing set)

---

## 6. MCP-Specific Actors

### Current State

Apify has a dedicated MCP Servers category. The official Apify MCP Server connects AI agents (Claude Desktop, Cursor, VS Code) to 3,000+ actors.

### Top MCP Server Actors

| Actor | Users | Rating | Price |
|-------|-------|--------|-------|
| Fast Google Search Results Scraper | 8K | 4.5 | $0.50/1K results |
| Fast Website Content Crawler | 5K | 4.4 | Pay-per-usage |
| Indeed Job Search | 3K | 4.1 | $3/1K results |
| Threads Search Scraper | 2K | 4.2 | $2/1K results |
| Tavily MCP Server | 1K | 4.5 | Pay-per-usage |

### MCP Opportunity Assessment

- MCP is still early — most actors are "regular" actors that also expose MCP endpoints
- The $1M Challenge (Nov 2025–Jan 2026) produced many new MCP actors, but most are unproven
- Apify is actively promoting MCP: "fastest path to monetize MCP servers" with 130K+ monthly signups
- Protocol just migrated from SSE to Streamable HTTP (April 2026)
- Skyfire agentic payments let AI agents pay autonomously — new monetization vector
- **MCP + AI agents is Apify's strategic bet for 2026**

### MCP Gap Analysis
- Most MCP actors are wrappers around existing web scrapers
- Few purpose-built MCP actors that leverage agent orchestration patterns
- Multi-tool MCP servers (combining several data sources in one server) are rare
- Domain-specific MCP servers (legal, finance, academic) are nearly nonexistent

---

## 7. Strategic Takeaways

### Best Opportunities (High Value, Low Competition)

1. **SEC/Financial Regulatory Intelligence MCP** — Filings, insider trades, enforcement actions. Premium pricing ($0.50-$1.00/result). Few competitors, high-value users.

2. **Court Records & Legal Research** — Federal + state courts unified scraper. Lawyers and compliance teams will pay premium prices.

3. **Patent Intelligence Platform** — USPTO + EPO + WIPO. Patent landscape analysis for R&D teams. Very few actors exist.

4. **Niche Job Board Aggregator** — Not LinkedIn/Indeed (crowded). Target: remote job boards (WeWorkRemotely, RemoteOK), tech-specific (BuiltIn, Dice), crypto/web3 jobs. Unified output format.

5. **B2B Review Intelligence** — G2 + Capterra + Trustpilot unified scraper. SaaS companies need competitive intelligence. Rising star territory.

6. **Academic Paper Multi-Source** — Semantic Scholar + SSRN + bioRxiv + CrossRef. The AI/RAG boom drives demand. Current actors only cover arXiv/PubMed.

### Pricing Sweet Spot
- **$0.10-$0.30 per result** for standard extraction
- **$0.50-$1.00 per result** for intelligence/analysis outputs
- Always include actor-start event at $0.005-$0.01

### What the Market Data Says
- Product pricing scraping (34.8%) and social media (26.1%) are the biggest segments but also the most crowded
- Real estate, research, and enterprise/regulatory data are growth sectors
- AI integration (RAG, agents) is creating entirely new demand categories
- The web scraping market itself is projected to reach $2.49B by 2032
