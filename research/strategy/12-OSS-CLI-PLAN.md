# ScanAble OSS CLI Plan

## The Opportunity

The accessibility CLI space has established players but a clear gap:

| Tool | Weekly Downloads | Status | Paid Tier |
|------|-----------------|--------|-----------|
| axe-core (engine) | ~35M | Actively maintained (Deque) | No (MIT license) |
| @axe-core/cli | Low (thin wrapper) | Maintained | No |
| pa11y | ~210-288K | Community maintained | No |
| lighthouse | ~2M | Google maintained | No |

**Every existing accessibility CLI is pure OSS with zero commercial upsell.** None funnel users to a paid hosted product. This is the Plausible/PostHog/Sentry pattern waiting to happen.

## The Funnel

```
Developer finds ScanAble CLI on npm/GitHub
            │
            ▼
    npx scanable https://example.com
            │
    Free terminal output: score + top violations
            │
            ▼
    "Want a PDF report? Visit scanable.dev/report/abc123"
    "Want CI/CD integration? See scanable.dev/api"
    "Want historical tracking? See scanable.dev/dashboard"
            │
            ▼
    2-5% convert to paid (API, reports, or dashboard)
```

## What the CLI Does

```bash
# Quick scan (free, always)
$ npx scanable https://example.com

  ScanAble — WCAG 2.2 Accessibility Scanner

  URL:    https://example.com
  Score:  72/100 (Grade: C)
  Level:  AA

  ┌─────────────────────────────────────────┐
  │ CRITICAL  2 violations                  │
  │ SERIOUS   5 violations                  │
  │ MODERATE  12 violations                 │
  │ MINOR     4 violations                  │
  │ PASSED    87 rules                      │
  └───────────────���─────────────────────────┘

  Top violations:
  ❌ color-contrast (serious) — 5 elements
  ❌ image-alt (critical) — 2 elements
  ❌ link-name (serious) — 3 elements
  ⚠️ heading-order (moderate) — 4 elements
  ⚠️ region (moderate) — 8 elements

  Full report: https://scanable.dev/report/abc123
  API docs:    https://scanable.dev/docs/api

# JSON output (for CI/CD)
$ npx scanable https://example.com --format json

# Fail CI if score below threshold
$ npx scanable https://example.com --threshold 80
  # Exit code 1 if score < 80

# Scan multiple URLs
$ npx scanable --urls urls.txt --format csv

# With API key (higher limits, full violation details)
$ SCANABLE_API_KEY=sk_live_... npx scanable https://example.com --full
```

## Differentiation from pa11y / @axe-core/cli

| Feature | pa11y | @axe-core/cli | ScanAble CLI |
|---------|-------|---------------|-------------|
| Compliance score (0-100) | No | No | **Yes** |
| Letter grade (A-F) | No | No | **Yes** |
| Severity-weighted scoring | No | No | **Yes** |
| PDF report generation | No | No | **Yes (via hosted)** |
| CI threshold flag | Via config | No | **--threshold N** |
| Historical tracking | No | No | **Yes (via hosted)** |
| Beautiful terminal output | Basic | Basic | **Branded, colored** |
| JSON/CSV export | JSON | JSON | **JSON + CSV** |
| Hosted API upsell | No | No | **Yes** |
| WCAG 2.2 support | 2.1 | 2.2 | **2.2** |

The key differentiator isn't technical (all use axe-core under the hood). It's the **funnel**: free CLI → paid reports/API/dashboard.

## Technical Implementation

### Package Structure
```
packages/
  scanable-cli/
    src/
      index.ts        # CLI entry point (commander.js)
      scanner.ts       # Reuse from existing lib/scanner.ts
      formatter.ts     # Terminal output formatting (chalk)
      json-output.ts   # JSON/CSV formatters
      api-client.ts    # Optional: call hosted API instead of local scan
    package.json       # @scanable/cli or just "scanable"
    README.md          # Installation, usage, CI examples
```

### Two Modes

**Local mode (default)**: Runs puppeteer locally. No API key needed. Free forever.
- Pros: No dependency on hosted service, works offline
- Cons: Requires Chrome/Chromium installed, slower startup

**API mode (with key)**: Calls scanable.dev API. Faster, no local Chrome needed.
- Pros: Faster, lighter, full violation details, usage tracked
- Cons: Requires API key, internet connection, counts against quota
- Trigger: `SCANABLE_API_KEY` env var or `--api-key` flag

### npm Publishing
- Package name: `scanable` (check availability — if taken, use `@scanable/cli`)
- `npx scanable` for zero-install usage
- Global install: `npm install -g scanable`

### GitHub Repo
- Separate repo: `github.com/scanable/cli` (or monorepo with main product)
- README with: badges, GIF demo, installation, CI examples
- GitHub Actions workflow template included in repo
- MIT license (same as axe-core)

## GitHub Actions Template (included in README)

```yaml
# .github/workflows/accessibility.yml
name: Accessibility Check
on: [pull_request]
jobs:
  scan:
    runs-on: ubuntu-latest
    steps:
      - uses: actions/checkout@v4
      - name: Start dev server
        run: npm start &
      - name: Run ScanAble
        run: npx scanable http://localhost:3000 --threshold 80 --format json
```

This template alone drives adoption — developers copy-paste it into their repos.

## Distribution Channels

1. **npm**: Primary distribution. `npx scanable` for instant use.
2. **GitHub**: Stars + README + Actions template. SEO for "accessibility CI/CD".
3. **Dev.to / Hashnode**: "How to add accessibility testing to your CI pipeline" tutorials.
4. **Awesome lists**: Submit to `awesome-accessibility`, `awesome-testing`, `awesome-ci`.
5. **Reddit**: r/webdev, r/accessibility, r/devops — launch post.
6. **VS Code extension** (Phase 3): Right-click → "Scan for accessibility" in editor.

## Revenue Model

The CLI itself is free. Revenue comes from:

| Upsell | Price | Trigger |
|--------|-------|---------|
| PDF report | $19 | CLI output includes link to hosted report |
| API subscription | $19-149/mo | Developers wanting API mode (no local Chrome) |
| Dashboard | Future | Historical score tracking, team sharing |

**Expected conversion**: 2-5% of active CLI users → paid product.

| Metric | Month 3 | Month 6 | Month 12 |
|--------|---------|---------|----------|
| npm weekly downloads | 500 | 2,000 | 8,000 |
| Monthly active users | 200 | 800 | 3,000 |
| Paid conversions (3%) | 6 | 24 | 90 |
| MRR from CLI funnel | $114 | $456 | $1,710 |

Conservative. The real value is **distribution** — GitHub stars and npm downloads create organic discovery that feeds all other revenue channels.

## Effort

| Task | Days |
|------|------|
| Extract scanner into standalone package | 1 |
| CLI interface (commander.js + chalk) | 1 |
| JSON/CSV output formatters | 0.5 |
| API mode (call hosted endpoint) | 0.5 |
| CI threshold flag + exit codes | 0.5 |
| README + GIF demo + GitHub Actions template | 1 |
| npm publish + GitHub repo setup | 0.5 |
| **Total** | **5 days** |

## When to Build

**Phase 1A, weeks 5-6** (per portfolio strategy). After pSEO, API, and security scan are running. The CLI is a distribution multiplier — it makes all other channels work harder by creating a new discovery funnel. But it's lower priority than revenue-generating layers.

Exception: If ScanAble's paid conversion rate is low but the product gets developer attention (HN, Reddit engagement), building the CLI earlier could accelerate the developer adoption → API subscription pipeline.
