---
date: 2026-04-24
iteration: 26
status: ADJACENCY-SCAN
---

# Iteration 26 — ScanAble-Adjacency Targeted Scan

**Strategy**: Iter 25 surfaced 3 adjacency candidates that *might* satisfy ScanAble's full 5-ingredient template (public crawlable input × regulatory deadline × zero-margin pipeline × sub-$50 transactional × pSEO directory). Targeted 30-minute scan to verify or kill each.

---

## Candidate 1 — Hreflang multi-language SEO compliance pSEO

| Ingredient | Status |
|---|---|
| Public crawlable input | ✅ HTML/HTTP headers public |
| Regulatory mandate | ❌ Google guidance, not legal |
| Zero-margin pipeline | ✅ DNS + HTML parse |
| Sub-$50 transactional gap | ❌ free tools dominate |
| Weak incumbent | ❌ 9+ free checkers |

**Existing**: [TechnicalSEO.com](https://technicalseo.com/tools/hreflang/) (free), [SearchViu](https://www.searchviu.com/en/hreflang-testing-tool/) (free), [SEOptimer](https://www.seoptimer.com/hreflang-checker), [Sitechecker](https://sitechecker.pro/hreflang-checker/), [SiteGuru](https://www.siteguru.co/features/hreflang), [Apify hreflang checker](https://apify.com/automation-lab/hreflang-checker), Seomator, [Screaming Frog audit guide](https://www.screamingfrog.co.uk/seo-spider/tutorials/how-to-audit-hreflang/), WebsiteAudit. Plus Ahrefs/SEMrush/Sitebulb cover hreflang in suites.

**Verdict**: KILL. No regulatory cliff to drive paid demand. Free tools fill the same niche ScanAble's $19 PDF would target.

---

## Candidate 2 — App store privacy nutrition label compliance audit

| Ingredient | Status |
|---|---|
| Public crawlable input | ⚠️ partial — labels public, but actual SDK data flows are private |
| Regulatory mandate | ❌ deadline ALREADY PAST |
| Zero-margin pipeline | ❌ requires SDK inspection (binary analysis) |
| Sub-$50 transactional gap | ❌ enterprise (OneTrust) dominates |
| Weak incumbent | ❌ |

**Existing**: [OneTrust Mobile App Compliance & Scanner](https://www.onetrust.com/blog/google-data-safety-vs-apple-nutrition-label/), [TermsBox checklist](https://termsbox.com/blog/app-permissions-disclosure-checklist), automated governance platforms tracking SDK inventory + privacy policy mapping. Apple Privacy Manifest Files (mandatory Q1 2024). Apple Privacy Nutrition Labels (mandatory Dec 2020). Google Play Data Safety (mandatory July 2022).

**Verdict**: KILL. The window closed 2-4 years ago. Apple/Google enforcement has settled. Enterprise tools (OneTrust) own the audit segment.

---

## Candidate 3 — DKIM/SPF/DMARC per-domain audit pSEO

| Ingredient | Status |
|---|---|
| Public crawlable input | ✅ DNS records public |
| Regulatory mandate | ⚠️ Google/Yahoo bulk-sender enforcement Feb 2024 (passed); PCI DSS 4.0 DMARC req March 2025 (passed) |
| Zero-margin pipeline | ✅ DNS lookup |
| Sub-$50 transactional gap | ❌ MxToolbox free + 8 alternatives free |
| Weak incumbent | ❌ heavily saturated |

**Existing**: [MxToolbox](https://mxtoolbox.com/dmarc/dmarc-email-tools) (free), [AutoSPF](https://autospf.com/), [dmarcian](https://dmarcian.com/) (SPF Surveyor), [EasyDMARC](https://easydmarc.com/), [DMARCLY](https://dmarcly.com/tools/), [PowerDMARC](https://powerdmarc.com/), [Red Sift Investigate](https://redsift.com/guides/best-dkim-checker-tools-2026), Mailtrap, DNSChecker. 9+ free per-domain checkers + several full enterprise platforms.

**Verdict**: KILL. Both deadline cliffs (Google/Yahoo Feb 2024, PCI DSS March 2025) have passed; supply collapsed to free during the run-up.

---

## The structural learning that emerged

ScanAble caught a 6-12 month window between **regulatory deadline announcement** and **free-tool race-to-the-bottom**. That window has a predictable shape:

```
Deadline announced   →   Free tools rush in   →   Window closes
        │                       │                        │
        T+0                   T+6mo                   T+12mo
                          ↑
                   ScanAble entered here
                   (axe-core OSS engine + paid PDF format)
```

The three adjacency candidates above are all post-T+12mo:
- Hreflang has no deadline at all (Google never enforced as compliance)
- Privacy nutrition labels: T+ 4 years
- DMARC: T+2 years past Google/Yahoo cliff, T+1 year past PCI DSS

**For an iter 27 to find a ScanAble-template survivor, the search has to filter for regulatory cliffs that (a) are 6-12 months out from now (May 2026 → April 2027), (b) have objective public-crawlable input, and (c) haven't yet attracted free lead-gen tools.** The existence of such a window is unlikely-but-not-impossible — most known 2026/2027 cliffs already have free tools positioning (EU AI Act, EAA, DSA, Data Act).

A genuine candidate would need to be a niche regulatory deadline that the SEO-driven compliance-tool ecosystem hasn't found yet. By definition, those are hard to surface via standard web search — they live in trade publications, specific regulator press pages, and industry-specific compliance newsletters.

---

## Honest closure

5 methodology paths now tested:
1. Top-down vertical (iter 1-22)
2. Bottom-up wishlist (iter 23)
3. Upwork recurring-task mining (iter 24)
4. Below-bar reframe screen (iter 25)
5. ScanAble-adjacency targeted scan (iter 26)

All converge on the same closure. The structural conditions that lifted ScanAble (regulatory cliff at T-6 to T-12 months + public crawlable input + zero-margin OSS engine + free/enterprise polarized incumbents + no sub-$50 player) are rare and short-lived. Either Jobelo got lucky on timing for ScanAble, or the next survivor lives in a regulatory niche too narrow for general web search to surface.

**Recommendation**: stop here. The marginal compute on iter 27 has very low expected value unless the user has access to specific regulatory-trade newsletters or industry-specific compliance signals not indexed by Google. The 5-path triangulation is now structurally explained: closure ≠ "no ideas exist" but "the structural ingredients required for survivors are rare and require timing luck or insider signal access — both of which web search cannot provide."

## Stats updated

- Iterations: 26
- Total ideas killed: 247+
- Methodology paths tested: 5
- Surviving above bar: APIDelta (22/30) — Day 30 pending May 15
- Consecutive zero-result iterations: 14 (13-26)
- Research status: **DEFINITIVELY CLOSED with 5-way methodology triangulation + structural explanation.**
