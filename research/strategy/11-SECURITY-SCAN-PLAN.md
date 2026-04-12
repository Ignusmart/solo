# Security Scan Variant Plan

> **STATUS: FROZEN (April 2026)**
> Deprioritized. Demand is weaker than accessibility — no single enforcement deadline like ADA Title II or EAA. Free tools (Mozilla Observatory, SSL Labs, SecurityHeaders.com) are more capable in this space than free accessibility tools are in theirs. SOC 2 and cyber insurance create some payment pressure, but it's diffuse and unproven for a $29 per-report model. Engineering time is better spent on the OSS CLI (distribution multiplier for existing API subscribers) and validating that people actually pay for accessibility reports before extending to a weaker vertical. Can revisit if ScanAble hits $5K+/mo and needs a cross-sell lever.

## The Opportunity

Three signals converged to create a gap:

1. **SecurityHeaders.com killed its API** — no new subscriptions, renewals stopped. Supply gap.
2. **Mozilla Observatory is free, zero monetization.** SSL Labs is free, no paid tier. None produce PDF reports.
3. **Cyber insurers and SOC 2 auditors now demand documented evidence** of web security controls — not just scores, but exportable proof.

**The gap**: No tool generates a branded, compliance-framed PDF report of web security posture that a team can attach to a vendor security questionnaire (VSQ), SOC 2 audit, or insurance renewal form.

This is the EXACT same pattern as ScanAble: free tools do the check, nobody generates the report.

## Demand Assessment (honest)

**Weaker than accessibility.** There's no WCAG-equivalent legal mandate for HTTP security headers specifically. However:

| Driver | Strength | Notes |
|--------|----------|-------|
| SOC 2 audits | MEDIUM | Auditors check TLS, HSTS, CSP as part of "System Operations" criteria |
| Cyber insurance | GROWING | Insurers shifted from questionnaires to demanding technical evidence in 2025-2026 |
| Vendor security questionnaires | STRONG | Every B2B sale to enterprise requires a VSQ — documented posture helps |
| PCI DSS | STRONG (for ecommerce) | Requires TLS 1.2+, secure headers, quarterly scans |
| General best practice | WEAK | Developers check for free, no payment pressure |

**Verdict**: Not as strong as accessibility (no single enforcement deadline), but SOC 2 + insurance + VSQ create real payment pressure for a subset of buyers. Worth building as a low-effort extension of ScanAble.

## What to Check

Using open-source tools (zero API cost, same as ScanAble's axe-core model):

### HTTP Security Headers (SecurityHeaders.com replacement)
- Content-Security-Policy (CSP) — 70% of apps missing/misconfigured
- Strict-Transport-Security (HSTS) — 34% still lack this
- X-Frame-Options / frame-ancestors
- X-Content-Type-Options
- Referrer-Policy
- Permissions-Policy
- Cross-Origin-Opener-Policy (COOP)
- Cross-Origin-Resource-Policy (CORP)

### TLS/SSL Configuration
- TLS version (1.2+ required, 1.0/1.1 flagged)
- Certificate validity and expiration
- HSTS preload list membership
- HTTP → HTTPS redirect present

### Cookie Security
- Secure flag on all cookies
- HttpOnly flag
- SameSite attribute
- No sensitive data in non-secure cookies

### Content Security
- Mixed content (HTTP resources on HTTPS page)
- Exposed server version headers (Server, X-Powered-By)
- Directory listing enabled
- Exposed .env, .git, or config files (basic check)

### Overall Score
- Letter grade A+ through F (familiar from SecurityHeaders.com)
- Numeric score 0-100 (consistent with ScanAble accessibility score)
- Severity categorization: Critical / Warning / Info / Pass

## Technical Implementation

### Scanning Engine
- **No headless browser needed** for most checks (unlike accessibility)
- Simple HTTP HEAD/GET request + header parsing
- TLS checks via Node.js `tls` module or `ssllabs-scan` npm package
- Cookie inspection from response headers
- Exposed file checks: quick HEAD requests to `/.env`, `/.git/config`, `/wp-config.php.bak`
- **Cost per scan: < $0.001** (no browser, just HTTP requests)

### Where It Lives
- Same ScanAble codebase (monorepo or feature flag)
- New route: `scanable.dev/security` (or separate domain `securityscan.dev`)
- Shared: Stripe, PDF generation, DB, auth infrastructure
- **Effort: 2 weeks** (1 week scanning logic, 1 week PDF template + UI)

### PDF Report Template
```
[SecurityScan Logo]
Web Security Posture Report
═══════════════════════════
Site: example.com
Date: April 12, 2026
Grade: B (78/100)

EXECUTIVE SUMMARY
━━━━━━━━━━━━━━━━
✅ TLS 1.3 active
✅ HSTS enabled (max-age: 31536000)
⚠️ CSP missing — critical for XSS prevention
⚠️ Permissions-Policy not set
❌ X-Powered-By header exposes server tech
✅ Cookies: Secure + HttpOnly flags present

DETAILED FINDINGS
━━━━━━━━━━━━━━━━
[Each check with: status, description, impact, fix recommendation]

COMPLIANCE MAPPING
━━━━━━━━━━━━━━━━━
SOC 2 CC6.1: [relevant findings]
PCI DSS 4.1: [relevant findings]
Cyber Insurance: [relevant findings]

This report can be attached to vendor security questionnaires,
SOC 2 audit evidence packages, or cyber insurance renewal forms.
```

**The compliance mapping section is the differentiator.** Free tools give you a grade. This report maps findings to specific SOC 2 criteria and PCI DSS requirements — that's what makes it worth paying for.

## Pricing

| Option | Price | Notes |
|--------|-------|-------|
| Security Report (standalone) | $29 | Same checkout flow as ScanAble |
| Accessibility Report (existing) | $19 | Already built |
| **Full Compliance Bundle** | **$39** | Both reports, 18% savings. Anchor pricing. |

The bundle is the key play. Buyers who need accessibility reports for ADA/EAA compliance are the SAME buyers who need security documentation for SOC 2/insurance. Offering both at $39 (vs $48 separate) creates a natural upsell.

## Distribution

1. **Cross-sell on ScanAble checkout** — "Add Security Scan for just $20 more"
2. **pSEO pages**: `scanable.dev/security/check/[domain]` (same model as accessibility)
3. **Comparison SEO**: "SecurityHeaders.com alternative" (they killed their API — orphaned users searching)
4. **SOC 2 prep content**: "Web Security Evidence for SOC 2 Type II" blog post
5. **Cyber insurance content**: "What Your Cyber Insurer Checks on Your Website" blog post

## Risk Assessment

| Risk | Severity | Mitigation |
|------|----------|------------|
| Free tools are "good enough" for most | HIGH | The REPORT (PDF for compliance) is the value, not the check itself |
| No single enforcement deadline like ADA/EAA | MEDIUM | SOC 2 + insurance are ongoing, not deadline-driven — slower but steady demand |
| Low conversion on standalone security reports | MEDIUM | Bundle with accessibility to guarantee cross-sell revenue |
| SecurityHeaders.com relaunches API | LOW | They were acquired by Snyk — likely going enterprise, not indie pricing |

## When to Build

**Phase 1A, week 4** (per portfolio strategy). After pSEO and API are running. Low-effort extension (2 weeks) with natural cross-sell to existing ScanAble buyers.
