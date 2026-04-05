# SaaS Spend Tracker for Small Teams — Opportunity Assessment

---

## The Gap

| Segment | Existing Solutions | Price | Gap? |
|---------|-------------------|-------|------|
| Enterprise (1000+) | Zylo, Productiv | $50K–$150K/yr | Served |
| Mid-market (100–1000) | Cledara, Torii, Zluri | $15K–$36K/yr | Served |
| SMB (20–100) | NachoNacho (partially) | $300+/mo | Partially served |
| **Small team (1–20)** | **Spreadsheets** | — | **WIDE OPEN** |
| **Solo dev / freelancer** | **Nothing** | — | **WIDE OPEN** |

There is a **massive price gap** between NachoNacho ($10/user/mo, marketplace friction) and Cledara ($300/mo). A $19–$49/mo product sits in complete whitespace.

---

## The Pain (Validated)

- Average 1–50 person company uses **40–60 SaaS tools**
- Solo devs spend $200–$800/mo, 10-person startups $3K–$15K/mo
- Common complaints: forgotten subscriptions, ghost seats from departed employees, free trials converting to paid unnoticed, no single view of total spend
- Current "solution": spreadsheets, Notion templates, or nothing at all
- **Nobody combines cloud costs (AWS, Vercel, GCP) + SaaS costs (Slack, Notion, Linear) in one dashboard for small teams**

---

## Why This Fits You

| Dimension | Fit |
|-----------|-----|
| **Personal pain** | You literally tallied $25K+/mo across 23 services from Slack messages at Webacy |
| **Stack** | Next.js + API dashboard — your core strength |
| **No mobile needed** | Pure web app |
| **B2B pricing** | $19–$49/mo (not $5/mo consumer) |
| **Self-serve** | Devs sign up, connect email, done |
| **AI angle** | Receipt parsing, transaction categorization, cost optimization — all LLM-native |
| **Global** | Every startup everywhere has this problem |
| **Async distribution** | SEO, dev communities, build-in-public |

---

## Technical Approach (MVP)

### Phase 1: Manual + Email Parsing (Weeks 1–3)
- User adds subscriptions manually (name, cost, cycle, category)
- Connect Gmail via OAuth → scan for SaaS receipts/invoices
- AI (Claude) extracts: vendor, amount, date, billing cycle, plan tier
- Dashboard: total monthly spend, by category, renewal calendar, trend charts
- **Stack**: Next.js, Prisma, PostgreSQL, Claude API, Gmail API
- **Cost**: Gmail API is free. Claude API for parsing ~$0.01/receipt.

### Phase 2: Bank Connection (Weeks 4–6)
- Plaid integration → pull credit card/bank transactions
- AI categorizes recurring charges as SaaS
- Auto-detect new subscriptions, cancelled ones, price changes
- Anomaly alerts: "Your AWS bill jumped 40% this month"

### Phase 3: Direct Integrations (Weeks 7+)
- AWS Cost Explorer API, Vercel API, Stripe API (many SaaS bills through Stripe)
- Show actual usage data where possible (not just cost)
- "You have 5 GitHub seats but only 3 active users"

---

## Pricing

| Tier | Price | Features |
|------|-------|----------|
| Free | $0 | Manual tracking, up to 15 subscriptions, basic dashboard |
| Pro | $19/mo | Email auto-discovery, unlimited subs, AI categorization, alerts, export |
| Team | $49/mo | Bank connection, multi-user, shared dashboard, cost optimization AI, API integrations |

---

## Distribution

1. **Build-in-public on Twitter/X** — post your own Webacy SaaS spend breakdown (it's shocking enough to go viral)
2. **SEO** — "SaaS expense tracker", "track SaaS spending", "how much do startups spend on SaaS"
3. **Dev communities** — r/startups, r/SaaS, Indie Hackers, HN
4. **Product Hunt** launch
5. **Content** — "We audited our startup's SaaS spend and found $X,000/year in waste" blog posts

---

## Competitive Landscape

| Competitor | Why They Don't Serve Small Teams |
|-----------|--------------------------------|
| Cledara ($300/mo) | Too expensive, enterprise features, virtual card model |
| Zylo ($50K/yr) | Pure enterprise |
| NachoNacho | Marketplace model — must buy SaaS through them, can't track existing subs |
| Vendr Free | Lead gen tool, barely functional, Vendr struggled financially |
| Rocket Money / Truebill | Consumer/personal, not business SaaS |
| Notion/spreadsheets | Manual, no automation, no insights |

**Nobody is doing: affordable + automated + AI-powered + built for devs/small teams.**

---

## Revenue Projections

| Month | Users (Free) | Users (Paid) | MRR |
|-------|-------------|-------------|-----|
| 1–2 | 50 | 5 | $100–$200 |
| 3–4 | 200 | 25 | $500–$1,000 |
| 6 | 500 | 75 | $2,000–$3,000 |
| 9 | 1,000 | 200 | $5,000–$7,000 |
| 12 | 2,000 | 400 | $10,000–$15,000 |

---

## Risks

| Risk | Mitigation |
|------|-----------|
| Low willingness to pay at $19/mo | Start free, prove value with "you're wasting $X/mo", convert on insights |
| Plaid costs eat margin at small scale | Start with email parsing only (free), add Plaid when revenue covers cost |
| Enterprise tools expand down | They won't — their sales model doesn't work at $19/mo |
| Hard to get transaction data | Email parsing is the key unlock — most SaaS sends receipts |

---

*Generated 2026-04-04.*
