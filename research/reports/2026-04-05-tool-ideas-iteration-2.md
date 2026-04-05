# Tool Ideas — Iteration 2 (2026-04-05)

## Focus: Non-AI tools, B2B niches, seasonal/compliance tools

Followed iteration 1's recommendation to explore categories beyond "X generator" AI tools.

### Categories Explored & Killed
- Product mockups (Printify/Mockey free, 20K+ templates)
- Offer letter generators (Zoho/Canva/Easy-Peasy all free)
- Moving cost calculators (lead-gen for movers, all free)
- Wedding/tax calculators (all free)
- Barcode/QR/shipping labels (Shopify free, Avery free)
- Email deliverability/warm-up (11+ tools, already killed in SaaS)
- Screenshot-to-code (Figma built-in, Codia)
- Tariff/customs calculators (Flexport/Gateway/AMZ Prep all free)
- Certificate generators (Canva/Certifier free)
- Social proof widgets (15+ tools, free options dominate)
- Lien waiver generators (Built and Terms.Law both free)
- GBP audit tools (Merchynt free, SaaS territory)
- Etsy/Amazon seller tools (already killed in SaaS research)

---

## Deep Dives

### 1. StubSnap — Modern Paystub Generator ⭐ FIRST 16+ SCORE

**Concept**: Pay-per-stub paystub generator with modern UX, accurate 2026 IRS tax tables, all 50 states. $3.99/stub.

**Why this works (unlike most killed ideas):**
- **Compliance-gated**: IRS tax tables, FICA, state taxes. ChatGPT CAN'T do this accurately.
- **Proven market**: ThePayStubs gets 117K visits/month at $5.99/stub.
- **Repeat use**: Every pay period (weekly/biweekly/monthly). Not one-and-done.
- **Pay-per-use model already works**: 9+ competitors all charge $3-6/stub successfully.
- **Zero API costs**: Pure computation (tax math), no AI inference needed. ~95%+ margin.

**Competition**: ThePayStubs ($5.99, 117K visits/mo), SecurePayStubs ($2.99), StubCreator ($4.99), 123PayStubs ($3.99), Wix (free basic), PayStubMakers (free tier).

**Differentiation angle**: Most paystub sites look dated and have a "scammy" vibe (associated with fake paystubs for fraud). A clean, professional tool with:
- Modern UI (not 2015 WordPress)
- Batch generation for employers (generate stubs for all employees at once)
- Salary vs hourly calculator
- Year-to-date tracking
- Mobile-friendly (competitors are desktop-only)

**Unit economics**: Cost ~$0 per stub (just math + PDF). At $3.99/stub, margin >95%. Need 251 stubs/mo for $1K/mo. With 117K visits to ONE competitor, very achievable.

**Adversarial review (5 kill tests):**
1. Free tool test: Wix free exists but basic. For compliance documents, people pay for accuracy. **PASS** (borderline).
2. ChatGPT test: Cannot generate IRS-compliant stubs with accurate withholding calculations. **HARD PASS**.
3. Volume test: "Paystub generator" is a massive keyword (117K+ visits to one competitor). **STRONG PASS**.
4. Margin test: 95%+. No API costs. **STRONG PASS**.
5. Solo maintainability: Update tax tables annually (IRS Pub 15-T). Medium effort. **PASS**.

**Risk factors:**
- Fraud association (fake paystubs for loan applications). Need ToS disclaimers.
- Payment processor risk (Stripe may flag). Existing competitors operate fine.
- Tax calculation accuracy liability. Need disclaimers + testing.

**Score**: Search 5 | Build 4 | Economics 5 | Competition 3 | SEO 3 | **Total: 20/25 → 17/25 after adversarial** (fraud risk, payment processor concern, established SEO competitors)

**MVP (1 week)**: Next.js app. Form: employee info, pay period, salary/hourly, deductions. Output: IRS-accurate PDF paystub. Stripe per-stub payment. SEO landing pages for "[state] paystub generator".

**Kill criteria**: <50 stubs in first month. Stripe account flagged/banned.

---

### 2. ScanAble — Website Accessibility Report Generator

**Concept**: Input website URL → get a prioritized WCAG 2.2 compliance report with fix suggestions. $10-25 per report.

**Demand**: 10K+ ADA web lawsuits/year. Professional audits cost $1,250-2,750. SMBs can't afford full audits but face real legal risk.

**Competition**: WAVE (free, raw data), axe (free, dev-focused), accessiBe ($59/mo, controversial), Siteimprove (enterprise), professional audits ($1,250+).

**Gap**: Free tools give raw violations. Professional audits cost $1K+. No middle ground: a $10-25 automated report that's more actionable than WAVE but cheaper than professional audits.

**Unit economics**: $0 per scan (DOM crawling, no AI). At $15/report, margin >95%. Need 67/month.

**Adversarial review:**
1. Free tool test: WAVE exists but gives raw data. The REPORT format is the value. **BORDERLINE**.
2. ChatGPT test: Can't scan live websites. **PASS**.
3. Volume test: "Accessibility checker" has volume but less than paystubs. **BORDERLINE**.
4. Margin test: 95%+. **PASS**.
5. Solo maintainability: WCAG updates slowly. **PASS**.

**Risk**: Automated tools catch only ~25% of WCAG issues. Liability if business relies on report. Needs clear "automated scan, not a full audit" disclaimers.

**Score**: Search 3 | Build 3 | Economics 5 | Competition 3 | SEO 3 | **Total: 17/25 → 15/25 after adversarial** (WAVE free, liability risk)

---

## Key Discovery: Compliance-Gated Tools

Iteration 2's biggest insight: **compliance-gated tools resist the "free and good enough" pattern.** When getting the calculation wrong has legal/financial consequences, users pay for accuracy even when free tools technically exist.

Paystubs proved this: 9+ competitors all charging $3-6/stub successfully despite Wix offering a free version. The compliance requirement (IRS tax tables) creates pricing power that "AI generator" tools lack.

**Pattern to explore in future iterations:**
- Other compliance-gated calculations (payroll tax, sales tax, overtime)
- Document generators with legal requirements (W-2, 1099, I-9 forms)
- State-specific compliance tools (each state = separate SEO keyword)

## Next Iteration Should Explore
- Payroll-adjacent tools (overtime calculators, time-and-a-half tools)
- Sales tax calculators for ecommerce
- Niche professional calculators (contractor markup, project estimators)
- Tools leveraging Jobelo's technical depth (code analysis, security scanning)
- Social media scheduling tools (pay-per-post model?)
