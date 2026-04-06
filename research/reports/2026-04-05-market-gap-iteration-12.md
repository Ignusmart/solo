# Iteration 12: AI-Adoption Aftermath & Emerging Categories

**Date**: 2026-04-05
**Focus**: Genuinely new categories created by AI adoption (vibe coding, LLM cost management, MCP ecosystem), regulatory timing windows (EAA, DORA, NIS2, US state privacy), and analysis of what's actually working for solo founders in Q1 2026.
**Strategy shift**: Only exploring categories that didn't exist 12-18 months ago, since all established B2B categories are saturated (proven across 11 iterations).

---

## Search Coverage

### A) Post-AI Adoption Problems (8 categories scanned)
- AI tool sprawl (76% of enterprises report negative outcomes from disconnected AI tools)
- LLM cost tracking (CostLayer, StackSpend, Helicone, Portkey, Langfuse, LiteLLM)
- Vibe coding technical debt (8,000+ startups need rebuilds, 40% of AI code has vulnerabilities)
- MCP ecosystem gaps (53% insecure secrets, OAuth at 8.5%)
- AI agent management for SMBs
- Shadow AI / SMB governance
- AI output quality & brand consistency
- AI content fact-checking (best tools cap at ~82% accuracy)

### B) Regulatory Timing Windows (8 regulations checked)
- DORA (Jan 2025, financial sector — enterprise only)
- NIS2 (160K+ new entities, but cybersecurity expertise required)
- EAA (June 2025 deadline already passed, absorbed)
- US state privacy laws (wave of 2025-2026 laws)
- E-invoicing mandates (France Sept 2026, Germany Jan 2027)
- BOI/Corporate Transparency Act (legally frozen)
- ESG/CSRD (too far out for SMBs)
- AI disclosure laws (niche, scattered)

### C) What's Actually Working (Q1 2026)
- Cursor ($500M ARR), Bolt.new ($20M ARR), Lovable ($17M ARR) — AI coding dominates
- Chatbase ($50K MRR solo), Castmagic ($30K+ MRR), Zyki ($7K MRR in 30 days)
- Chrome extensions still lucrative: GMass ($130K/mo), Closet Tools ($42K/mo)
- 70% of micro-SaaS never break $500/mo; top 1-2% win on distribution, not technology
- Pattern: narrow use case + established distribution channel > novel technology

---

## Ideas Evaluated This Iteration

### 1. Vibe Code Health Scanner — AI-generated code security & quality audit

**Problem**: Non-technical founders used Bolt.new/Lovable/Cursor to build apps with AI. 40% of AI-generated code has vulnerabilities. 8,000+ startups estimated to need $50K-$500K rebuilds. Maintenance costs hit 4x traditional levels.

**Why it seemed promising**: Brand new problem (6-12 months old). Jobelo has the exact right skills (security + code review + full-stack).

**Adversarial findings — KILL**:

**8+ dedicated "vibe code scanner" tools already exist:**
- Vibe App Scanner, VibeSecurity, VibeWrench, VibeSafe, VibeCodesecure, VibeEval, SecureStartKit, VibeGuard

**$88M+ in VC already deployed:**
- Escape.tech raised $18M (March 2026) specifically for vibe coding vulnerabilities
- Qodo raised $70M for AI code verification

**Platforms bundling security in:**
- Lovable embedded Aikido pentesting ($100/test)
- Cursor shipped security automation templates
- GitHub Copilot agent runs CodeQL/secret scanning for free
- Anthropic launched a code review tool (March 2026)

**Buyer problem**: Vibe coders are price-sensitive non-devs. Team leads already have Snyk/CodeRabbit. The "post-breach panic" buyer is one-time.

**Verdict**: The window was real 6 months ago. Today it's closed. $88M in VC, 8+ dedicated tools, platforms absorbing. No room for a solo entrant.

**Score**: KILL — window closed, 8+ competitors, $88M in VC, platforms absorbing

---

### 2. LLM Cost Dashboard ("Plausible for AI Spend")

**Problem**: Small teams using 2-5 AI APIs (OpenAI, Anthropic, Google, Replicate) have no simple way to see total spend, per-project costs, budget alerts.

**Why it seemed promising**: Read-only dashboard connecting to billing APIs. No code changes needed. LiteLLM/Helicone require proxy setup.

**Adversarial findings — KILL**:

**CostLayer ($9/mo) does EXACTLY this:**
- Read-only, connects to billing APIs, no code changes
- Tracks OpenAI/Anthropic/Google
- 2-minute setup, budget alerts

**StackSpend also does this:**
- Read-only, no credit card needed to start
- Multi-provider dashboard, 90-day history, anomaly alerts

**10+ tools in the category:**
LiteLLM (38.9K GitHub stars), Helicone (free to 100K requests), Portkey (free tier), Langfuse (OSS, acquired by ClickHouse), plus cloud cost tools (CloudZero, Vantage, Finout) all adding AI cost tracking natively.

**Token prices dropping 67-97% YoY** — the pain of uncontrolled AI spend is shrinking, not growing.

**Verdict**: CostLayer at $9/mo already does this with no code changes. You can't beat $9/mo from an established player. Intermittent pain (checking bills monthly) + shrinking problem = dead.

**Score**: KILL — CostLayer at $9/mo, 10+ tools, shrinking problem

---

### 3. Accessibility Compliance Tool (EAA + ADA Title II)

**Problem**: European Accessibility Act (June 2025 deadline), ADA Title II (2026-2027 deadlines for US state/local govs). WCAG 2.1 AA compliance required.

**Why it seemed promising**: Regulatory deadline creating forced adoption. Clear standard (WCAG).

**Adversarial findings — KILL**:

**50+ tools on G2 in "web accessibility" category:**
- Enterprise: Deque (axe), Level Access, Siteimprove ($500-5K/mo)
- Mid-market: Pope Tech, Monsido, Silktide ($100-300/mo)
- SMB/Overlay: accessiBe ($49/mo), UserWay ($49/mo), AudioEye ($49-99/mo)
- Free: axe-core (open source), Lighthouse, Pa11y, WAVE extension

**Fix-once-and-done = high churn (8-15% monthly)**

**EAA demand spike already absorbed** (deadline was June 2025, a year ago)

**Core scanning tech is commoditized** (axe-core is open source and powers half the market)

**Verdict**: 50+ competitors, commoditized tech, demand spike absorbed, high churn. No entry point.

**Score**: KILL — 50+ competitors, commoditized, high churn

---

## Secondary Signals Considered and Dismissed

| Signal | Why Dismissed |
|--------|--------------|
| MCP server security middleware | MCP infrastructure previously killed. Protocol itself will absorb security standards. Too early for meaningful revenue. |
| SMB AI governance / policy-in-a-box | Adjacent to AIComply Lite (killed). Requires compliance expertise. "Policy generator" is an AI wrapper. |
| Meeting action-item enforcement | Overlaps with PM tools (Asana, Linear). Jobelo's async-only constraint conflicts with meeting-focused products. |
| Shadow AI detection (browser extension) | Requires MDM/centralized deployment. DLP tools exist. Too enterprise for micro-SaaS. |
| US multi-state privacy compliance | Osano, OneTrust, TrustArc, Enzuzo cover this. Free tiers available. |
| NIS2 cybersecurity for mid-sized cos | Requires deep cybersecurity compliance expertise. 160K entities but enterprise sales cycle. |
| AI content fact-checking | Best accuracy is 82%. Too unreliable for B2B. Liability risk. |

---

## Iteration 12 Summary

| Idea | Score | Verdict |
|------|-------|---------|
| Vibe Code Health Scanner | KILL | 8+ dedicated tools, $88M VC, platforms absorbing. Window closed 6 months ago. |
| LLM Cost Dashboard | KILL | CostLayer at $9/mo does exactly this. 10+ tools. Token prices dropping. |
| Accessibility Compliance Tool | KILL | 50+ tools on G2. Commoditized tech (axe-core OSS). Demand absorbed. |

**Running total**: 12 iterations, 160+ ideas considered, 0 scoring 18+. Best surviving: APIDelta at 17/25.

---

## Meta-Learning from Iteration 12

### The "emerging category" hypothesis failed
Even genuinely new categories (vibe code security, LLM cost tracking) fill with competitors within 6-12 months. The vibe code security space went from zero to 8+ tools + $88M in VC in under a year. By the time you identify the category, it's already crowded.

### New kill pattern (#14): Speed of category formation has accelerated
In 2020, a new B2B category took 2-3 years to fill. In 2026, it takes 6-12 months. AI-enabled development means competitors can ship MVPs in days. VC funding cycles have compressed. The "first mover" window for micro-SaaS is now measured in weeks, not months.

### Distribution > Technology (confirmed)
The Q1 2026 solo founder data is unambiguous: 70% of micro-SaaS never breaks $500/mo. The winners win on distribution (Chrome Web Store, Shopify App Store, existing audience, SEO) not on finding unserved problems.

### Potential strategy pivot
After 12 iterations of problem-space scanning with zero viable results, the evidence suggests:
1. **Every identifiable B2B problem is already served by multiple tools**
2. **New categories fill within 6-12 months of emerging**
3. **Solo founder success correlates with distribution advantage, not problem novelty**

Future iterations should potentially focus on: **distribution-first opportunities** (Chrome Web Store gaps, VS Code marketplace gaps, Slack App Directory gaps, specific community/marketplace distribution) rather than problem-space scanning.
