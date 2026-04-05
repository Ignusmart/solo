# Tool Ideas — Iteration 3 (2026-04-05)

## Focus: Compliance-adjacent tools, payroll-adjacent, technical tools

Doubled down on the compliance-gated pattern from iteration 2 and explored technical tools leveraging Jobelo's depth.

### Categories Explored & Killed
- **Sales tax calculators** — Shopify built-in, Avalara/TaxJar dominate, $19K+/year enterprise pricing. Platform gives it away.
- **Overtime calculators** — 10+ free tools (Omni Calculator, Good Calculators, Connecteam). Zero pricing power.
- **Code review/security scan** — SaaS territory ($9-30/dev/mo). 28+ OSS tools. Dev tools go free.
- **Construction estimating** — Complex SaaS ($100-950/mo). Not utility tool shaped.
- **PDF watermark/protect** — iLovePDF/PDF Candy free. PDF Stamping at 1.5¢/page. Race to zero.
- **BOI/CTA reports** — US companies EXEMPT as of March 2025 interim rule. Market killed by regulation change.
- **Nutrition label generators** — OnlineLabels, Packify, ePackageSupply all free. Kill.
- **PDF accessibility/remediation** — EqualWeb $1-4/page. But technically complex (4-8 week build). Too complex for MVP.
- **P&L statement generators** — Tyms free, QuickBooks/FreshBooks templates free. Kill.
- **Rent receipt generators** — Free generators everywhere. Rent not federally tax-deductible. Kill.
- **W-9 form generators** — IRS form is free. Adobe, CreateW9, SmallPDF all free. Kill.
- **Donation receipt generators** — Zeffy 100% free, Givebutter free. Kill.
- **Employee handbook generators** — Already killed in SaaS research (AirMason, Waybook).
- **Email signature generators** — Already killed (HubSpot free, 10+ tools).

---

## Analysis: Why StubSnap Remains Uniquely Strong

After 3 iterations exploring 50+ categories, **StubSnap is the ONLY idea to score 16+.** Here's why paystubs are special:

1. **Compliance creates trust-based pricing power**: IRS tax tables across 50 states are complex enough that free tools feel risky. People pay $3-6/stub for ACCURACY, not features.
2. **Repeat use**: Every pay period, not one-and-done. A business with 5 employees generates 120+ stubs/year.
3. **Zero API costs**: Pure math (tax calculation) + PDF generation. No AI inference, no cloud APIs. >95% margin.
4. **Proven at scale**: ThePayStubs.com gets 117K visits/month. Market is REAL.
5. **No platform threat**: Neither Canva, Google, nor Adobe is going to build a paystub generator.

### Why most other compliance tools failed to match:
- **W-9, W-4, I-9 forms**: IRS provides free fillable PDFs. No value-add.
- **1099/W-2 e-filing**: Requires IRS integration (complex build) + seasonal-only.
- **Donation receipts**: Fundraising platforms (Zeffy, Givebutter) include for free.
- **Nutrition labels**: Free generators are good enough for small producers.
- **Overtime calculators**: No document output — just a calculator. Free everywhere.
- **Sales tax**: Shopify/Amazon handle it. Avalara for enterprise.

The paystub pattern works because it's a **compliance document + computational complexity + repeat use + no platform threat**. This combination is rare.

---

## Recommendation: Build StubSnap

After 3 iterations, 50+ categories, and 40+ killed ideas, StubSnap is the clear winner:

| Factor | Evidence |
|--------|----------|
| Market proof | 117K visits/mo to ThePayStubs, 9+ competitors charging $3-6/stub |
| Pricing power | Compliance requirement (IRS tax accuracy) resists "free kills everything" |
| Unit economics | >95% margin (zero API costs, pure computation) |
| Repeat use | Every pay period × every employee |
| Build time | 1 week for MVP (form + tax calc + PDF output) |
| SEO potential | 50 state-specific landing pages + long-tail keywords |

**Risk to mitigate**: Fraud association. Use professional branding, require employer info, add disclaimers.

## Next Iteration Should Explore (if StubSnap doesn't proceed)
- Multi-tool portfolio approach (28 simple tools, not one big bet)
- Non-English markets (translation gap)
- Physical-world compliance tools (safety signs, OSHA documents)
- Niche calculators for high-value decisions (loan comparison, real estate ROI)
