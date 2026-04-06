# Iteration 16: Revenue-Reverse Engineering

**Date**: 2026-04-05
**Strategy**: Instead of scanning for problems, reverse-engineered from REAL solo-founder revenue ($2K-50K/mo). Studied what's actually making money in 2026 and looked for adjacent gaps.

---

## Real Revenue Examples Found

| Product | MRR | How they grow | Adjacent gap? |
|---------|-----|---------------|---------------|
| Bannerbear | $50K | SEO, dev docs, content | PDF generation API — but PDFShift/PDFMonkey exist |
| Photo AI | $132K | Twitter, viral, PH | Niche AI photo tools — but AI wrapper risk |
| Simple Analytics | $40K | SEO ("GA alternative") | Vertical analytics — but Plausible/Fathom saturate |
| Carrd | $30K | Word-of-mouth, organic | "Carrd for X" — but single-page builders are commodified |
| FounderPal | $10K | PH, free tools, SEO | AI business generators — AI wrapper kill filter |
| Capgo | $25K | Capacitor ecosystem | OTA for React Native — Expo dominates |
| Karma | $25K | Slack App Directory | Niche Slack bots — platform absorption risk |

## Key Patterns

1. **SEO + content → $10K+ MRR** is the dominant growth path (Bannerbear, Simple Analytics, Plausible)
2. **Marketplace distribution** (Slack, Chrome, Capacitor) provides discovery but carries platform risk
3. **Median MRR is $500/mo** — 70% of micro-SaaS never breaks $500. The bar is high.
4. **5-7x ARR acquisition multiples** — $5K MRR = $300-420K exit value

## Adjacent Gaps Evaluated

All mapped back to existing kill patterns:
- PDF generation API → PDFShift, PDFMonkey, DocSpring exist
- Vertical privacy analytics → Plausible + Fathom + Simple Analytics saturate
- Screenshot-to-docs → AI wrapper risk, too niche
- OTA updates for React Native → Expo dominates
- Niche Slack bots → platform absorption (kill filter #16)
- AI business generators → AI wrapper (kill filter #1)

## Conclusion

**This iteration confirms APIDelta is the right call.** The winning pattern from revenue data (clear B2B pain → simple tool → SEO growth) is exactly APIDelta's playbook:
- Clear pain: 67% of devs hit unexpected breaking API changes
- Simple tool: changelog crawler + AI classification + alerts
- SEO growth: "API changelog monitoring", "breaking change alerts"
- Engineering buyer: company credit card, daily use, sticky

**Research is officially exhausted.** 16 iterations, 190+ ideas, 6 strategy pivots. Every remaining adjacent gap maps to killed patterns. Recommend: cancel research loop, ship APIDelta.

---

Running total: 16 iterations, 190+ ideas, APIDelta at 22/30 (only idea meeting bar)
