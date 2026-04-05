# Action Plan — April 2026

What to build, based on what's actually making money for solo devs.

---

## The Patterns That Work

From 25 real solo/tiny-team products making $5K–$50K+/mo:

### Pattern 1: AI Workflow Tool (best fit)
Wrap AI capabilities in a polished UI for ONE specific use case.

| Product | Revenue | What | Solo? |
|---------|---------|------|-------|
| TypingMind | $130K+/mo | Better UI for ChatGPT | Yes |
| Chatbase | $5M ARR | Train chatbot on your docs | Started solo |
| PhotoAI | $132K MRR | AI headshots from selfies | Yes |
| HeadshotPro | $300K/mo | AI professional headshots | Started solo |
| PDF.ai | $25K MRR | Chat with your PDFs | Small team |

**Common thread**: Take an AI capability, wrap it in a better UX than raw APIs, charge $29–$99/mo. Distribution: Twitter build-in-public + Product Hunt + SEO.

### Pattern 2: API Product
Build an API that solves one specific automation problem. Docs + SEO + self-serve.

| Product | Revenue | What |
|---------|---------|------|
| Bannerbear | $52.5K MRR | Auto-generate images via API |
| ScreenshotOne | $12.9K MRR | Screenshot API |
| PDFShift | $9K MRR | HTML-to-PDF API |

### Pattern 3: Open Source + Cloud
Build in TypeScript/Next.js, open-source it, monetize the cloud version.

| Product | Revenue | What |
|---------|---------|------|
| Postiz | $14K/mo | Social media scheduler (14K GitHub stars) |
| Papermark | $45K MRR | DocSend alternative |
| Plausible | $258K/mo | Privacy analytics |
| Dub.co | $1.4M/2yr | Link shortener + attribution |

### Pattern 4: Developer Tool Portfolio
Ship many small tools, revenue compounds.

| Builder | Revenue | Products |
|---------|---------|----------|
| Marc Lou | $94K/mo | 13 products (ShipFast, CodeFast, DataFast, etc.) |
| Pieter Levels | $3M+/yr | Nomad List, RemoteOK, PhotoAI, InteriorAI |

---

## The Two-Track Strategy

### Track 1: Premium MCP Servers on MCPize (This Week)

**MCPize is confirmed real:**
- 85/15 revenue share (you keep 85%)
- Payouts monthly via Stripe Connect
- CLI: `npx mcpize init` → develop → `mcpize deploy`
- TypeScript and Python supported
- 100+ servers published, $200K+ paid to creators
- PostgreSQL Connector: $4,200/mo. AWS Security Auditor: $8,500/mo.

**What to build (pick 2 this week):**

Focus on services that (a) don't have official MCP servers, (b) developers use daily, (c) have complex APIs that benefit from AI access:

| Server Idea | Why | Price |
|-------------|-----|-------|
| **Supabase MCP** | Hugely popular, no official MCP, complex API (auth + DB + storage + edge functions) | $29/mo |
| **Vercel MCP** | Deploy, manage projects, check logs, manage domains via AI | $29/mo |
| **Resend/Email MCP** | Send, track, manage email campaigns via AI | $19/mo |
| **Cloudinary MCP** | Upload, transform, manage media assets via AI | $29/mo |
| **PlanetScale/Neon DB MCP** | Database management, branching, queries via AI | $29/mo |
| **Sentry MCP** (enhanced) | Official one exists but basic — add error analysis, suggested fixes, alert management | $29/mo |
| **Analytics MCP** (Plausible/Umami/PostHog) | Query analytics data, create reports via AI | $29/mo |

**Ship cadence**: 1 server/week. Build a portfolio like Marc Lou builds products.

**Revenue target**: 
- Month 1–2: 2–3 servers, $500–$1,500/mo
- Month 6: 10+ servers, $3,000–$5,000/mo  
- Month 12: 20+ servers, $5,000–$10,000/mo

### Track 2: Find Your AI Workflow Product (In Parallel)

The highest-revenue solo products follow the Chatbase/TypingMind pattern: take an AI capability, make it accessible for a specific use case, charge $29–$99/mo.

**Your advantages:**
- TypeScript/Next.js expert (the stack of choice: Chatbase, Papermark, Postiz, Dub.co all use it)
- AI/ML experience (Claude API, CrewAI, LangGraph)
- Extreme build velocity (ship MVP in days)
- API design at scale

**The process to find it:**
1. While shipping MCP servers weekly, you'll see which services developers struggle with
2. The MCP servers give you distribution (MCPize listings, GitHub, npm)
3. The MCP servers give you revenue while you search
4. When you spot a pattern ("everyone wants X but the tools suck"), that's your product

**What the product should look like:**
- Web only (Next.js + API). No mobile.
- AI-powered but solving a specific workflow, not a generic chatbot
- $29–$99/mo pricing
- Self-serve (docs + onboarding, no calls)
- One distribution channel deep: SEO, open-source, or build-in-public on Twitter

**Examples of what it could be (not prescriptive — let it emerge):**
- A better AI interface for a specific dev workflow (like TypingMind did for ChatGPT)
- An AI-powered automation tool for a specific business process (like Chatbase did for customer support)
- An open-source tool with a paid cloud version (like Postiz/Papermark)

---

## What NOT to Do

- Don't publish Plata to App Store (park it)
- Don't build MCP infrastructure tooling (monitoring, testing, token optimization — all crowded or no demand)
- Don't build for regulated industries (biotech, healthcare, fintech compliance)
- Don't build LATAM-specific tools
- Don't build Web3 security tools
- Don't build mobile apps
- Don't spread across 5 ideas — MCP servers + 1 product, max

---

## Week 1 Action Items

- [ ] Create MCPize account, connect Stripe
- [ ] Run `npx mcpize init` and explore the CLI/templates
- [ ] Pick first 2 MCP server targets (check what's already on MCPize to avoid duplicates)
- [ ] Ship first MCP server by end of week
- [ ] Set up Twitter/X for build-in-public (post about MCP server development)

---

*Generated 2026-04-04.*
