# Tool Ideas — Iteration 6 (2026-04-05)

## Focus: Stress-test ScanAble — find hidden competitors and validate demand

After 5 iterations and 70+ killed categories, ScanAble at 20/25 is the clear winner. This iteration stress-tested it by searching for additional competitors and validating demand with hard data.

### Additional Competitors Found

| Tool | Price | Model | Gap vs ScanAble |
|------|-------|-------|----------------|
| **CompliScan** | Free scan (dashboard only) / $49-299/mo subscription | Subscription | Free scan shows results in browser. PDF reports only on $149/mo+ tier. No per-report option. |
| **OnePageAudit** | Free (top 3 violations) / $49 per full report | Per-report | Closest competitor! $49/report. Free tier only shows top 3 violations, no PDF. |
| **The Audit Base** | $99 (50 pages min) | Per-report | Targets gov/healthcare. $99 minimum overpays for small sites. |
| **AccessibilityChecker.org** | $89-299/mo | Subscription | No per-report option. Overkill for SMBs. |
| **Accessible.org** | $350+ VPAT / $1,250+ audit | Professional service | Manual human audit. Way too expensive. |

**Key finding**: OnePageAudit at $49/report VALIDATES the per-report model. ScanAble at $15-25 would be the cheapest per-report option by 2-4x.

### Demand Validation (Hard Data)

- **8,667 ADA web accessibility lawsuits in 2025** — growing annually
- **14% increase in lawsuits** from 2023 to 2024
- **94.8% of websites fail WCAG** compliance (2025 Web Almanac data)
- **77% of ADA lawsuits target businesses under $20M revenue** — EXACTLY the ScanAble target market
- **EAA fines: €5,000-€300,000** depending on EU member state
- **ADA Title II deadline: April 24, 2026** for state/local gov websites serving 50K+ populations
- **EAA microenterprise exemption**: Businesses with <10 employees AND <€2M turnover exempt from SOME requirements. This narrows the EU market slightly but US ADA has NO such exemption.

### Revised Competitive Positioning

```
FREE                           $15-25                    $49               $99+
WAVE, CompliScan free    →    ScanAble (proposed)   →  OnePageAudit  →  The Audit Base
(no PDF, inline only)         (full PDF report)        (full report)     (50-page min)
```

ScanAble uniquely fills the gap between free inline scanners and $49+ per-report tools. No competitor offers a sub-$49 downloadable compliance PDF.

### Revised Score: 21/25

| Criterion | Score | Notes |
|-----------|-------|-------|
| Demand | 5/5 | 8,667 lawsuits/year, 94.8% failure rate, EAA + ADA enforcement. Not hypothetical — litigation-driven demand. |
| Build speed | 5/5 | axe-core + Playwright + PDF. Proven stack (Audit Base, CompliScan use same tech). |
| Unit economics | 5/5 | Zero API costs. >95% margin. |
| Competition gap | 3/5 | OnePageAudit at $49 is closest. No one at $15-25. But WAVE free might be "good enough" for some. |
| SEO | 3/5 | Growing queries. Can target 50-state + EU-country landing pages. Market education still needed for SMBs. |
| **Total** | **21/25** | Bumped from 20 due to stronger demand validation (lawsuits data, 94.8% failure rate). |

### Pricing Recommendation
- **$19/report (single URL)** — not $15 (leaves money on table) or $25 (too close to psychological barrier). $19 is 2.5x cheaper than OnePageAudit ($49) and 5x cheaper than Audit Base ($99).
- **$39/site (up to 10 pages)** — competitive with OnePageAudit's single-page $49.
- **Free tier**: Scan 1 URL, show top 5 violations in browser (no PDF). Converts to paid for full report.

### Final Recommendation

**STOP RESEARCHING. START BUILDING.**

After 6 iterations, 70+ killed categories, and thorough adversarial review with actual competitor site visits, ScanAble at 21/25 is definitively the strongest idea. Every additional iteration is diminishing returns. The compliance-gated + zero-API-cost + litigation-driven-demand combination is uniquely strong.
