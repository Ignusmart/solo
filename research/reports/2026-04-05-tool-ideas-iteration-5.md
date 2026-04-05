# Tool Ideas — Iteration 5 (2026-04-05)

## Strategy Pivot: Emerging Demand + Re-evaluation

After 60+ killed categories, pivoted from grinding new categories to hunting EMERGING regulatory demand and re-evaluating existing leaderboard ideas with new data.

### Quick Kills (8 more categories)
- AI content detection, YouTube thumbnails, PDF table extraction, teacher worksheets, Bill of Lading generators, SVG/Cricut generators, email deliverability testing, multi-tool aggregator model (TinyWow — requires 200+ tools, essentially SaaS)

### Key Discovery: European Accessibility Act (EAA)

The EAA became enforceable **June 28, 2025**. As of March 2026:
- France's DGCCRF issuing formal notices to retailers
- Germany's Bundesnetzagentur investigating complaints
- US: ADA Title II deadline for state/local government websites = **April 24, 2026**
- 23M+ EU SMBs potentially affected

This creates MASSIVE new demand for accessibility compliance tools — specifically for the **long tail of small businesses** that can't afford enterprise solutions.

---

## Deep Dive: ScanAble Re-evaluation (20/25)

### Concept
URL → automated WCAG/EAA compliance scan → professional PDF report with score, violations by severity, remediation guidance, and compliance statement. $15/report for single URL, $35 for full site (up to 10 pages).

### Competitive Landscape (VISITED actual sites)

| Tool | Price | What It Does | Gap |
|------|-------|-------------|-----|
| **WAVE** (wave.webaim.org) | Free | Inline error overlay on webpage. AIM score. | **No downloadable PDF compliance report.** Can't file this with a regulator. |
| **axe DevTools** | Free (browser ext) | Inline error list for developers. | Dev-focused, not business-owner friendly. No report. |
| **AccessibilityChecker.org** | $89-299/mo | Subscription monitoring platform. Continuous rescans, auto-statements. | **Subscription-only.** Overkill for a cafe needing one annual check. |
| **The Audit Base** | $99 min (50 pages) | PDF report with compliance score. AI-powered. Uses axe-core + Playwright. | **$99 minimum.** Targets gov/healthcare/higher ed. Overpays for small sites. |
| **Professional audits** | $1,250-2,750 | Manual human audit with remediation plan. | Way too expensive for SMBs. |

**The gap**: A cafe in Berlin with 3 pages pays $99 minimum at The Audit Base (overpaying for 47 unused pages) or $89/mo at AccessibilityChecker.org (absurd for a one-time check). **$15 for a single-URL compliance report fills a genuine void.**

### Kill Tests (all 5 pass)
1. **Free tool test**: WAVE doesn't generate downloadable compliance reports. **PASS.**
2. **ChatGPT test**: Can't scan live websites — requires DOM rendering + WCAG rule engine. **PASS.**
3. **Volume test**: 23M EU SMBs. 0.01% = 2,300 reports × $15 = $34K (conservative). **PASS.**
4. **Margin test**: axe-core free, Playwright free, PDF generation free. >95% margin. **PASS.**
5. **Solo maintainability**: axe-core handles rule updates. No AI, no complex APIs. **PASS.**

### Why This Differs From StubSnap (key lesson)
- StubSnap's competitor (ThePayStubs) was a **full platform** with 30+ products
- ScanAble's competitors are either **free but limited** (WAVE) or **priced for enterprises** (Audit Base, AccessibilityChecker)
- No competitor offers a simple $15 per-report model for SMBs
- The Audit Base IS per-report but targets large institutions ($99 min, 50 pages)

### Scoring

| Criterion | Score | Justification |
|-----------|-------|---------------|
| Demand | 4/5 | EAA enforced, France/Germany actively enforcing. ADA Title II deadline April 2026. Growing search volume. |
| Build speed | 5/5 | axe-core + Playwright + PDF generator. Stack proven (The Audit Base uses same tech). 1 week MVP. |
| Unit economics | 5/5 | Zero marginal cost per scan. Hosting: ~$20-50/mo. >95% margin at $15/report. |
| Competition gap | 3/5 | Clear gap but Audit Base at $99 serves some of the market. WAVE might be "good enough" for some. |
| SEO | 3/5 | Growing queries ("EAA compliance check", "WCAG report online"). Market education needed for small businesses. |
| **Total** | **20/25** | **PASSES 16+ threshold. First idea to survive full adversarial review.** |

### Risks
1. Small businesses may not yet know about EAA → requires content marketing/education
2. The Audit Base could lower minimum to $29 → competitive pressure
3. WAVE could add a downloadable report feature → free competition
4. Trust: unknown brand vs established accessibility firms → mitigate with detailed methodology docs

### MVP Scope (1 week)
- **Input**: URL field + email
- **Processing**: Playwright loads page → axe-core scans → collect violations
- **Output**: PDF report with compliance score, violations by severity (critical/serious/moderate/minor), WCAG criterion references, plain-English remediation hints, scan metadata
- **Payment**: Stripe checkout, $15/report (single URL), $35/site (up to 10 pages)
- **SEO**: Landing pages for "EAA compliance check", "WCAG accessibility report", "website accessibility audit online"
- **Tech**: Next.js + serverless function (or simple Express server) + Puppeteer/Playwright + axe-core

### Kill Criteria
- <30 reports in first month after launch
- Competitor (WAVE or Audit Base) adds $10-25 tier
- EAA enforcement stalls across EU

---

## Recommendation

**ScanAble should proceed to build.** After 5 iterations and 70+ categories:
- It's the ONLY idea to score 16+ after full adversarial review with competitor site visits
- The compliance-gated pattern holds (EAA = legal consequences = willingness to pay)
- Unit economics are exceptional (zero API costs, >95% margin)
- Build is straightforward (1 week, proven tech stack)
- The competitive gap is real and verified by visiting actual competitor sites
