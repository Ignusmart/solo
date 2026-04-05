# MCP Tooling Deep Dive — April 2026

Detailed expansion of the MCP infrastructure opportunity: what exists, what's broken, where the money is, and what to build.

---

## 1. The MCP Ecosystem — State of Play

### Scale

| Metric | Number |
|--------|--------|
| MCP SDK downloads | 97M+/month |
| MCP servers listed | 11,000+ across registries (17,186 on mcp.so alone) |
| MCP clients | 300+ |
| Remote servers growth | 4x since May 2025 |
| Enterprise adoption | Block, Bloomberg, Amazon, hundreds of Fortune 500 |
| Market size (2025) | $1.8B |
| Servers monetized | <5% |
| Servers that are "toy demos" | ~95% (9,500 of 10,000+) |

### Quality Crisis

- **66% of 1,808 scanned servers had security findings** (AgentSeal)
- **82% have file operations vulnerable to path traversal**
- **53% rely on insecure long-lived static secrets** (API keys, PATs)
- **Only 8.5% use OAuth** for auth
- **492 servers publicly exposed** without basic authentication
- **30 CVEs in 60 days** in early 2026
- **10 MCP plugins = 92% exploitation probability** (VentureBeat)
- OWASP published an MCP Top 10 security risks list

### The Maturity Gap

The ecosystem is in a "npm circa 2016" state: massive growth, minimal quality control, no production tooling standards. This is exactly when infrastructure tooling companies get built.

---

## 2. Competitive Landscape — What Already Exists

### Gateways (CROWDED — 40+ products, avoid building another)

| Product | Focus | Pricing |
|---------|-------|---------|
| MintMCP | SOC 2/HIPAA governance, one-click deploy | Enterprise |
| TrueFoundry | High performance (3-4ms latency, 350+ RPS) | Enterprise |
| Composio | 500+ managed integrations, 18K GitHub stars | Free tier + paid |
| Lunar.dev MCPX | Granular ACLs | Enterprise |
| ContextForge (IBM) | Open source, federation, REST/MCP/A2A bridge | Free |
| Jetski | Open source, auth + analytics, no code changes | Free |
| MCP Mesh | RBAC, token vaulting, OpenTelemetry | Free |
| AIRIS MCP Gateway | 60+ tools behind 7 meta-tools (major token reduction) | Free |

**Verdict: Do NOT build a gateway.** The space is saturated with well-funded and open-source options.

### Monitoring/Observability (GAP — no standalone lightweight tool)

| Product | What It Actually Does | Limitation |
|---------|----------------------|------------|
| Grafana Cloud MCP | Dashboard for protocol health + tool analytics | Requires Grafana infrastructure |
| Datadog MCP Server | Exposes Datadog data VIA MCP (not monitoring MCP) | Wrong direction — monitors through MCP, not OF MCP |
| IBM Instana | Enterprise APM with MCP feature | Enterprise-only, heavy |
| Honeycomb Hosted MCP | Traces/metrics inside IDEs | Using observability data through MCP |
| MCP Manager | Enterprise controls, audit logging | Enterprise-focused |
| MCP Inspector | Protocol validation, dev testing | Dev-only, cannot observe production traffic |

**The gap is clear**: No simple, affordable tool for a dev or small team running MCP servers to see call volumes, error rates, latency, and token usage. Everything is either enterprise-grade or the wrong direction (using MCP to access monitoring data vs monitoring MCP itself).

### Testing (GAP — nothing exists)

| Tool | What It Does | Limitation |
|------|-------------|------------|
| MCP Inspector | Protocol frame validation, CLI mode for CI | Barebones. No assertions, mocking, regression, team features, history |
| Apify Tester | Lightweight smoke testing | Minimal |

**No "pytest for MCP servers" exists.** No assertion library, no mocking, no regression testing, no CI/CD-native test suites.

### Config Management (GAP — single macOS-only option)

| Tool | What It Does | Limitation |
|------|-------------|------------|
| Conductor | Cross-client config sync, visual editor, keychain credentials, 7,300+ Smithery servers | **macOS only**. No Windows/Linux. No cloud/team sync. |
| MCP Config Generator | Browser-based config file generator | One-off generation, not sync |

### Token Optimization (GAP — proven solutions, no productized version)

The problem is massive:
- Cloudflare's 2,500 endpoints = **244,000 tokens** as MCP tool metadata
- GitHub MCP: 93 tools = 55,000 tokens
- Power user setup: **75,000 tokens consumed before any user input** (1/3 of context window)
- One team burned **143,000 of 200,000 tokens (72%)** on tool definitions
- Cursor enforces a **hard limit of 40 tools**
- MCP costs **4–32x more tokens** than CLI equivalents
- Claude quality **visibly degrades after 50+ tools**

Proven solutions exist but aren't productized:
- Hierarchical routing: 2 meta-tools instead of hundreds → 98% reduction
- AIRIS Gateway: 60+ tools behind 7 meta-tools
- Cloudflare Code Mode: spec lives server-side → 99.9% reduction
- Semantic routing (MCPToolRouter): embedding-based filtering → 70–85% savings

**No plug-and-play product exists that a developer can install and immediately reduce their token overhead.**

### Marketplaces Where Creators Make Money

| Platform | Servers | Revenue Share | Creator Payout Data |
|----------|---------|--------------|-------------------|
| **MCPize** | Growing | **85%** to creator | Top earners $3K–$10K+/mo. New creators $100–$500/mo |
| **Apify** | Growing | **80%** to creator | Paid **$596K total** to creators (Dec 2025). 130K+ monthly subs |
| **Smithery** | 2,880+ verified | 0% to creators | Creators pay for hosting. Discontinuing stdio Sept 2025 |
| **Glama** | 9,000+ | 0% to creators | Discovery only |
| **mcp.so** | 17,186+ | 0% | Discovery only |

### Real Revenue Examples

| MCP Server | Revenue | Model |
|------------|---------|-------|
| AWS Security Auditor (MCPize) | **$8,500/mo** | 82 enterprise subs @ $149/mo |
| PostgreSQL Connector (MCPize) | **$4,200/mo** | 207 subs @ $29/mo |
| Figma Sync Server (MCPize) | **$2,800/mo** | 210 subs, freemium |
| 21st.dev Magic MCP (Cline) | Undisclosed | Free trial → Pro $16/mo → Pro Plus $32/mo |
| Anonymous Apify creator | **$2,000/mo** | Usage-based |

### Funded MCP Startups

| Company | Funding | Focus |
|---------|---------|-------|
| Manufact (YC) | $6.3M Seed | mcp-use SDK, 5M+ downloads, 9K GitHub stars |
| Alpic (Paris) | $6M Pre-seed | MCP server deployment platform |
| Castari (YC) | YC-backed | Tool connectors, snapshots, observability |
| Klavis AI (YC) | YC-backed | Open source MCP integration platform |
| Composio | Undisclosed | 500+ managed integrations |

All seed/pre-seed. No Series A in pure MCP infra yet. The space is very early.

---

## 3. Technical Foundation

### Transport: Streamable HTTP Is the Production Path

| Transport | Use Case | Monitoring Feasibility |
|-----------|----------|----------------------|
| **stdio** | Local dev, Claude Desktop | Very hard — must intercept stdin/stdout subprocess |
| **SSE** | Legacy, being superseded | Medium — HTTP-based but one-directional |
| **Streamable HTTP** | Production | **Easy** — standard HTTP middleware, JSON-RPC over POST |

Streamable HTTP makes MCP servers look like regular HTTP APIs. Standard infrastructure (load balancers, reverse proxies, observability) applies directly.

### SDK State

**TypeScript SDK**: v1.x stable, v2 pre-alpha. Two packages: `@modelcontextprotocol/server` and `@modelcontextprotocol/client`. Supports Zod v4 validation, Express/Hono adapters, stdio + Streamable HTTP.

**Python SDK**: v1.26.0. `FastMCP` class with decorator-based registration. Built-in OpenTelemetry instrumentation. ASGI mounting.

**What SDKs DON'T provide**: Rate limiting, health checks, circuit breaking, token counting, middleware pipeline, OpenTelemetry (TS SDK). You must add all production concerns yourself.

### OpenTelemetry Integration

- **FastMCP (Python)**: Best integration. Auto-generates spans: `tools/call {name}`, `resources/read {uri}`. Semantic attributes: `mcp.method.name`, `mcp.session.id`, `mcp.resource.uri`. Works with any OTLP backend.
- **opentelemetry-instrumentation-mcp (TypeScript)**: Community package, zero-config.
- **No spec-level standard** yet — Discussion #269 on GitHub is the active proposal.

### Proxy/Middleware Patterns

Building an MCP proxy requires handling:
1. **Session statefulness** — session IDs, capability negotiation, affinity
2. **Bidirectional communication** — servers can initiate requests to clients
3. **Tool list manipulation** — intercepting `tools/list` responses consistently
4. **Auth propagation** — OAuth flows on behalf of clients
5. **stdio bridging** — wrapping subprocess servers to HTTP

Reference implementations: Traefik Hub (policy-based filtering via JWT claims), Envoy AI Gateway (session multiplexing), IBM ContextForge (federation + protocol translation).

---

## 4. The Three Products to Build

Based on gap analysis, here's what has the clearest market gap and best fit for your skills.

### Product A: MCP Observatory — Lightweight Monitoring Dashboard

**What**: A self-serve monitoring dashboard for MCP servers. Drop-in middleware (npm package + Python package) that instruments your MCP servers and sends telemetry to a hosted dashboard.

**Core features (MVP)**:
- npm/pip install → auto-instruments MCP servers with OpenTelemetry
- Dashboard: call volume per tool, error rates, latency P50/P95/P99, token usage estimation
- Alerts: error rate spikes, latency degradation, server down
- Session tracking: active sessions, session duration, client types
- Works with stdio (via wrapper) and Streamable HTTP (via middleware)

**Why no one has built this**:
- Enterprise players (Grafana, Datadog, Instana) built MCP-as-a-data-source, not MCP-as-a-target
- MCP Inspector is dev-only and can't observe production traffic
- Open-source gateways (Jetski, MCP Mesh) bundle monitoring as a feature of a gateway, not a standalone product
- The ecosystem just crossed from "dev toy" to "production" — monitoring demand is now

**Technical approach**:
- TypeScript middleware: wraps MCP server handlers, auto-generates OTel spans following FastMCP's semantic conventions
- Python middleware: same approach, using FastMCP's existing OTel integration as reference
- Hosted dashboard: Next.js + ClickHouse (or TimescaleDB) for time-series telemetry
- OpenTelemetry collector as the ingestion layer — standard, extensible
- Client libraries auto-detect transport (stdio wrapper vs HTTP middleware)

**Competitive positioning**: "Sentry for MCP servers" — not the enterprise monitoring platform, but the simple drop-in that just works.

**Revenue model**:
- Free: 1 server, 7-day retention, basic dashboard
- Pro: $29/mo — 10 servers, 30-day retention, alerts, team access
- Team: $79/mo — unlimited servers, 90-day retention, API access, custom dashboards

**Distribution**: npm/pip (developers find it where they find MCP SDKs), GitHub, "MCP monitoring" SEO, dev community posts, build-in-public on Twitter.

**Time to MVP**: 3–4 weeks.
**Revenue potential**: $5K–$15K MRR within 6–12 months.

---

### Product B: MCP Test Kit — Testing Framework for MCP Servers

**What**: A testing framework purpose-built for MCP servers. Like pytest/jest but for MCP �� assertions on tool responses, mocking, snapshot testing, CI/CD integration.

**Core features (MVP)**:
- `npm install mcptestkit` / `pip install mcptestkit`
- Programmatic MCP client that connects to your server and runs test suites
- Built-in assertions: tool response schema validation, error code checking, latency thresholds
- Snapshot testing: record tool responses, alert on unexpected changes
- Mock MCP client: test server behavior without a real LLM
- CI/CD integration: GitHub Action that runs MCP tests on every push, outputs JUnit XML
- Coverage report: which tools were tested, which weren't

**Why no one has built this**:
- MCP Inspector's CLI mode is the only option and it's barebones (no assertions, no mocking, no history)
- The ecosystem was hobbyist until recently — nobody needed testing for weekend projects
- Enterprise teams are building internal testing tools but nothing is productized

**Technical approach**:
- Core: TypeScript + Python test runner that speaks MCP client protocol
- Connects via stdio (spawns server) or Streamable HTTP (connects to endpoint)
- DSL for test definitions (YAML or code-based)
- GitHub Action wrapper for CI/CD
- Reporter: JUnit XML, JSON, HTML

**Revenue model**:
- Open source core (free, drives adoption)
- Cloud dashboard: $19/mo — test history, trend tracking, team collaboration, badge for READMEs
- Enterprise: $49/mo — custom assertions, parallel test runs, Slack/webhook notifications

**Distribution**: npm/pip, GitHub (star farming via open-source core), "MCP testing" SEO, CI/CD marketplaces (GitHub Actions marketplace).

**Time to MVP**: 2–3 weeks (CLI + basic assertions + GitHub Action).
**Revenue potential**: $3K–$10K MRR within 6–12 months.

---

### Product C: MCP Token Optimizer — Plug-and-Play Token Reduction

**What**: A middleware/proxy that dramatically reduces MCP token overhead. Install it between your MCP clients and servers — it intelligently routes, filters, and compresses tool definitions.

**Core features (MVP)**:
- Drop-in proxy (single binary or npm package)
- **Semantic routing**: embeds tool descriptions, matches queries to relevant tools, forwards only the top-K tools to the LLM. 70–85% token savings.
- **Hierarchical compression**: collapses N tools into 2 meta-tools (`discover` + `execute`). 98% token savings.
- **Description trimming**: AI-optimized shorter tool descriptions that preserve intent. 30–50% savings on top of routing.
- Dashboard: token savings per session, tool usage frequency, routing accuracy

**Why no one has productized this**:
- AIRIS Gateway does tool aggregation but is a full gateway (heavy, not standalone)
- MCPToolRouter (.NET) is a library, not a product
- Cloudflare's Code Mode is Cloudflare-specific, not generalizable
- Everyone knows the problem (75K tokens wasted before user input) but no one sells the fix

**Technical approach**:
- Embedding model: local ONNX model for tool description embeddings (no external API calls, fast)
- Proxy mode: intercepts `tools/list` responses, filters based on session context
- Middleware mode: wraps MCP server SDK, filters at the source
- Supports both stdio (subprocess wrapper) and Streamable HTTP
- Configuration: YAML file defining routing rules, tool groups, compression strategies

**Revenue model**:
- Free: up to 20 tools, basic routing
- Pro: $29/mo — unlimited tools, semantic routing, dashboard, custom rules
- Team: $79/mo — multi-server management, API, team dashboards

**Distribution**: npm/pip, "MCP token optimization" SEO (high-intent — devs actively searching for this), HackerNews/Reddit posts showing before/after token counts, build-in-public.

**Time to MVP**: 3–4 weeks.
**Revenue potential**: $5K–$20K MRR within 6–12 months.

---

## 5. Recommended Strategy

### Build Order

**Phase 1 (Weeks 1–4): Ship MCP Observatory + 2 Premium Servers**

MCP Observatory is the primary product because:
- Clear gap (no lightweight standalone monitoring)
- Developers need it the moment they go to production
- Low complexity MVP (OTel middleware + dashboard)
- Natural upsell path (monitoring → testing → optimization)
- Positions you as "the MCP infrastructure person"

In parallel, ship 2 premium MCP servers on MCPize/Apify for quick initial revenue:
- Pick services with no official MCP server and high developer demand
- $29/mo each, 85% rev share on MCPize
- Target: $1K–$3K MRR from servers alone by month 2

**Phase 2 (Weeks 5–8): Add MCP Test Kit (open source core)**

- Open-source the test runner on GitHub (star farming, reputation building)
- Paid cloud dashboard for test history and team features
- Cross-sell from Observatory users ("you're monitoring your servers — are you testing them?")

**Phase 3 (Weeks 9–12): Add Token Optimizer**

- Highest technical complexity but highest value
- By now you have Observatory users who are seeing their token waste in the dashboard
- Natural pitch: "Your dashboard shows you're burning 75K tokens on tool metadata. Fix it with one line."

### Why This Order

1. **Observatory first** = you become the "MCP infrastructure" brand
2. **Premium servers** = immediate revenue while Observatory ramps
3. **Test Kit second** = open source core builds reputation + GitHub stars
4. **Token Optimizer third** = highest value but needs the audience from 1+2+3

### Pricing Summary

| Product | Free | Pro | Team |
|---------|------|-----|------|
| MCP Observatory | 1 server, 7d retention | $29/mo (10 servers, alerts) | $79/mo (unlimited, API) |
| MCP Test Kit | Open source CLI | $19/mo (cloud dashboard) | $49/mo (team, enterprise) |
| MCP Token Optimizer | 20 tools | $29/mo (unlimited, routing) | $79/mo (multi-server) |
| **Bundle** | — | **$59/mo** (all three) | **$149/mo** |

### Distribution Strategy (One Channel Deep)

**Primary (months 1–3)**: Developer content + GitHub
- 1 post/week: "Building MCP infrastructure" series on dev.to + Twitter
- Open-source components on GitHub (test runner, middleware SDKs)
- npm/pip presence (devs find tools where they find MCP SDKs)
- Build-in-public on Twitter/X showing dashboard screenshots, token savings numbers

**Secondary (months 3–6)**: SEO + marketplace
- "MCP monitoring", "MCP testing", "MCP token optimization" — low competition, high intent
- Smithery, Apify, MCPize listings for premium servers
- GitHub Actions marketplace for test kit

**Avoid**: Paid ads, Product Hunt (save for a later coordinated launch), broad marketing.

### Revenue Projections (Conservative)

| Month | Premium Servers | Observatory | Test Kit | Token Optimizer | Total |
|-------|----------------|-------------|----------|----------------|-------|
| 1 | $500 | $0 | — | — | $500 |
| 2 | $1,500 | $300 | — | — | $1,800 |
| 3 | $2,500 | $900 | $0 (launch) | — | $3,400 |
| 4 | $3,000 | $1,500 | $400 | — | $4,900 |
| 6 | $4,000 | $3,000 | $1,200 | $0 (launch) | $8,200 |
| 9 | $5,000 | $5,000 | $2,500 | $1,500 | $14,000 |
| 12 | $6,000 | $7,000 | $4,000 | $3,000 | $20,000 |

This assumes competitive audits continue as primary income during the ramp.

---

## 6. Key Risks & Mitigations

| Risk | Likelihood | Mitigation |
|------|-----------|------------|
| **MCP spec changes break your tools** | Medium | Stay close to the spec. Build on Streamable HTTP (stable). Follow spec discussions. |
| **A funded startup ships monitoring** | Medium | Castari (YC) is closest. Move fast — you have 3–6 month window. Your advantage: lightweight + affordable vs their enterprise focus. |
| **MCP ecosystem stalls** | Low | 97M SDK downloads/mo, Linux Foundation governance, backed by Anthropic + OpenAI + Google. Not stalling. |
| **Token overhead gets fixed in the spec** | Medium | Discussion #532 proposes protocol-level solution. Will take 6–12 months. Your product is the bridge. |
| **Free/OSS alternatives emerge** | High | Open-source your test runner (co-opt this). Keep monitoring and optimization as hosted services where the value is in the dashboard, not the library. |
| **Low willingness to pay** | Medium | Premium MCP servers already prove devs pay ($29–$149/mo on MCPize). Monitoring follows the Sentry/PostHog model — proven in dev tools. |

---

## 7. Sources

Landscape: Grafana Cloud MCP Observability, IBM Instana, Honeycomb Hosted MCP, MCP Manager, MCP Inspector, awesome-mcp-gateways (GitHub), AgentSeal security scan, Astrix Security MCP report, OWASP MCP Top 10, VentureBeat MCP exploit analysis.

Technical: MCP Specification (2025-03-26 + draft), TypeScript SDK, Python SDK/FastMCP, Traefik Hub MCP middleware docs, Envoy AI Gateway, IBM ContextForge, FastMCP OTel integration, opentelemetry-instrumentation-mcp, MCPToolRouter (.NET), ScaleMCP paper.

Monetization: MCPize platform + creator docs, Apify MCP developers portal, Smithery pricing, 21st.dev (Cline) case study, Manufact ($6.3M), Alpic ($6M), Cloudflare Code Mode blog, MCP adoption statistics (MCP Manager), CData enterprise MCP adoption report, Zuplo State of MCP.

Security: Christian Posta OAuth analysis, Stack Overflow MCP auth deep-dive, Simon Willison prompt injection analysis, Palo Alto Unit 42 MCP attack vectors, Red Hat MCP security risks, 30 CVEs in 60 days report.

---

*Generated 2026-04-04. This is a point-in-time analysis — the MCP ecosystem moves fast. Re-evaluate competitive landscape monthly.*
