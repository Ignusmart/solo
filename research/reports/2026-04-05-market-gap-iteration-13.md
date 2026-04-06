# Iteration 13: Distribution-First Marketplace Scanning

**Date**: 2026-04-05
**Strategy pivot**: After 12 iterations of problem-space scanning with zero viable results, this iteration scanned specific distribution channels (Chrome Web Store, VS Code Marketplace, Slack/Teams App Directory) for gaps where built-in discovery could carry a product.

---

## Search Coverage

### A) Chrome Web Store Analysis
- Revenue benchmarks: GMass ($130K/mo), Closet Tools ($42K/mo), Bubbles ($160K/mo), GoFullPage ($10K/mo)
- Manifest V3 killed ~26.6% of extensions in mid-2025, creating some gaps
- B2B workflow extensions outperform consumer by 10-50x
- Subscription at $8-30/mo is the dominant B2B model
- Honey ($4B acquisition), Loom ($975M), SquareX (to Zscaler Feb 2026) validate the channel

### B) VS Code Marketplace Analysis
- GitLens Pro ($12.99/user/mo), Copilot ($19/mo), Wallaby.js (~$16/mo) prove willingness to pay
- **Critical finding: VS Code Marketplace has NO native payment infrastructure.** Must use third-party licensing.
- Developer WTP for VS Code extensions is near zero (Indie Hackers consensus)
- SQLTools: 6.4M installs, 3.5 stars, effectively abandoned (last update Sep 2025)

### C) Slack/Teams App Directory Analysis
- Solo-founder Slack apps top out at $1-5K MRR on autopilot
- Slack absorbed AI channel summaries natively in 2025
- Platform risk extreme — Slack controls distribution, API access, can absorb features
- Best use: distribution channel for standalone product, not the entire product thesis
- Teams (320M+ MAU) is more underserved but weaker third-party ecosystem

---

## Ideas Evaluated This Iteration

### 1. AI Meeting Prep Chrome Extension ($15/mo)

**Concept**: Auto-pulls attendee LinkedIn profile, company info, recent news before calendar meetings. Generates 1-page briefing for salespeople.

**Why it seemed promising**: Clear pain (salespeople spend 10-30 min prepping), B2B buyer with budget, Chrome Web Store distribution.

**Adversarial findings — KILL**:

**8-12 direct/near-direct competitors**: Briefcase by Birch, Wudpecker, Read.ai, Fellow.app, Fireflies (added pre-meeting briefs), Tactiq, Clari Copilot, Grain.

**Platform absorption — severe**: Apollo.io, ZoomInfo, Gong, LinkedIn Sales Navigator all adding meeting prep as a feature. They already OWN the data. A standalone tool can't compete with platforms that have the contact/company database.

**LinkedIn scraping — legal/technical minefield**: LinkedIn aggressively blocks scraping extensions (sued HiQ Labs). Extensions get banned from Chrome Web Store via DMCA. Reliable LinkedIn data requires their API (expensive, restricted) or data providers ($50-200/mo) — destroying $15/mo unit economics.

**ChatGPT substitute**: "Summarize [person] at [company]" takes ~60 seconds. Saves 2-3 min per meeting. At 5 meetings/week = 15 min/month saved for $15/mo. Weak value prop.

**Weekly use, not daily**: Average salesperson has 3-8 external meetings/week. Sporadic use at $15/mo = high churn.

**Score**: KILL — crowded, platforms absorbing, LinkedIn data access risk, ChatGPT substitute, weekly use

---

### 2. VS Code Database GUI Extension ($8-15/mo)

**Concept**: Premium database client inside VS Code. SQLTools has 3M+ (now 6.4M) downloads but only 3.5 stars. "TablePlus but inside VS Code."

**Why it seemed promising**: Massive install signal on SQLTools (proven demand), poor execution by incumbents, developers don't want to context-switch.

**Adversarial findings — KILL**:

**DBCode already captured this opportunity**: 50+ database support, AI features, $3/mo pricing, 150K installs, actively updated (April 2026). It IS "TablePlus inside VS Code."

**VS Code has no native payment infrastructure**: Microsoft explicitly doesn't support paid extensions. Third-party licensing (code-checkout) takes 10% cut. Structural disadvantage.

**Developer WTP near zero**: Indie Hackers consensus — most devs have never paid for a VS Code extension. DBCode's $3/mo appears to be the market ceiling.

**The pricing math is impossible**: DBCode charges $3/mo for 50+ databases. To compete, you'd need equivalent breadth AND differentiation, all while building your own payment system.

**Score**: KILL — DBCode already here at $3/mo, no payment infrastructure, near-zero WTP

---

### 3. AI Gmail Triage Sidebar Extension ($12/mo)

**Concept**: Lightweight Chrome extension adding AI email prioritization, smart labels, quick-reply suggestions to Gmail. Not a full client replacement like Superhuman ($30/mo).

**Why it seemed promising**: Biggest TAM (1.8B+ Gmail users), email extensions have $100K+/mo ceiling (GMass), no one owns the "lightweight AI layer on Gmail" niche.

**Adversarial findings — KILL**:

**Google killed this in January 2026**: Gmail's Gemini 3 overhaul launched AI Inbox (priority clustering), AI Overviews (summaries), Suggested Replies (context-aware), Help Me Write — all free, all on by default. Every core feature of this extension is now native.

**Saturated at every price point**: Simplehuman ($7.49/mo) is already a lightweight Superhuman alternative. SaneBox ($7-12/mo) does server-side filtering. Half-dozen free AI Gmail extensions on Product Hunt.

**$12/mo not defensible**: SaneBox's $7/mo and Google's free native features bracket the price.

**Platform risk severe**: Google enforced full OAuth 2.0 (March 2025). DOM-scraping breaks on Gmail UI updates. Google controls every layer.

**Score**: KILL — Google absorbed this natively (Jan 2026), SaneBox at $7/mo, severe platform risk

---

## Secondary Signals Dismissed

| Signal | Why Dismissed |
|--------|--------------|
| LinkedIn Inbox CRM | LinkedIn actively fights extensions. Legal/technical risk. |
| Slack feedback triage bot | Narrow buyer pool. Slack AI absorption risk. Platform dependency. |
| Slack approval workflows | Approveit/Wrangle exist. Slack Workflow Builder improving. |
| VS Code AI Prompt Management | Speculative, no proven demand signal. |
| VS Code API Testing (better Thunder Client) | Thunder Client has 7M+ installs. DBCode precedent suggests $3/mo ceiling. |
| VS Code Deployment Dashboard | Vercel/Railway already great. Feature, not product. |
| Manifest V3 migration gaps | Speculative — don't know which specific extensions died. |

---

## Iteration 13 Summary

| Idea | Score | Verdict |
|------|-------|---------|
| AI Meeting Prep Extension | KILL | 8-12 competitors. Sales platforms absorbing. LinkedIn data risk. ChatGPT substitute. |
| VS Code Database GUI | KILL | DBCode at $3/mo already here. No payment infrastructure. Dev WTP ~$0. |
| AI Gmail Triage Sidebar | KILL | Google's Gemini 3 absorbed this natively. SaneBox at $7/mo. Platform risk. |

**Running total**: 13 iterations, 170+ ideas considered, 0 scoring 18+. Best surviving: APIDelta at 17/25.

---

## Meta-Analysis: Why Distribution-First Also Failed

The distribution-first hypothesis was: "stop looking for unserved problems, look for distribution channels with built-in discovery." Here's what we learned:

### 1. Marketplace platform risk is the dominant force
Every marketplace (Chrome Web Store, VS Code, Slack, Gmail) is controlled by a platform that can:
- Absorb your features natively (Google → Gemini in Gmail, Slack → AI summaries)
- Block your access (LinkedIn → extension bans)
- Prevent monetization (VS Code → no payment infrastructure)
- Change APIs at will (Google → OAuth enforcement)

### 2. The successful extensions ($100K+/mo) all have ONE thing in common
GMass (email sending), Closet Tools (Poshmark automation), Honey (coupon aggregation) — they all built on **data that the platform doesn't own or monetize directly**. GMass uses Gmail as a pipe, not a product. Closet Tools automates a marketplace. This is the key insight: the extension must use the platform as infrastructure, not depend on it for the core value.

### 3. New kill pattern (#16): Platform-dependent distribution = borrowed audience
If the platform controls your distribution AND your feature set AND your API access, you're not building a business — you're building a feature that the platform will absorb or block. The only surviving play is "platform as dumb pipe."

---

## Honest Assessment After 13 Iterations

After 170+ ideas across 13 iterations:
- Every B2B problem domain is saturated (iterations 1-11)
- Every emerging category fills in 6-12 months (iteration 12)
- Every marketplace distribution channel has platform risk (iteration 13)
- The bar of 18/25 may be unreachable through desk research alone

### Recommended next steps (not more research):

1. **Build APIDelta** (17/25, best surviving idea) — it's 1 point below bar but has the strongest fundamentals: engineering buyer with budget, daily use, sticky, clear MVP scope. Sometimes a 17 that ships beats a theoretical 18 that doesn't.

2. **Customer-first approach** — stop researching ideas, start talking to a specific buyer segment (e.g., engineering leads at 10-50 person SaaS). Ask what they're duct-taping. Build what they describe. The insight you need may only come from conversation, not desk research.

3. **Acquisition play** — buy a small, underperforming extension/tool (the HN poster who bought an extension and 3x'd revenue through better positioning). Distribution is the bottleneck; buying existing distribution may be more efficient than building from zero.

Research fatigue is real. 13 iterations of negative results doesn't mean nothing is viable — it means the viable idea likely requires direct market contact, not another round of desk research.
