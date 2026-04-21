# Wallet Persona API — Technical Spec

**Date**: 2026-04-20
**Status**: Pre-build spec. Decision point after Weekend 1 kill checkpoint.
**Parent research**: `research/reports/2026-04-20-ml-portfolio-product-ideas.md`
**Positioning**: ML-showcase portfolio piece + dev-facing API. NOT a Web3-security product — this is **trader / growth / research analytics**, explicitly non-security framing.

---

## 1. Product Definition

### One-liner

> "Nansen-lite with open methodology: input an EVM wallet, get a calibrated trader archetype + the 20 most behaviorally-similar wallets — via a simple developer API with a free tier."

### Primary users

| Segment | Use case | Entry product |
|---|---|---|
| Crypto newsletter writers / researchers | Shareable persona cards for posts about any wallet (viral loop) | Free tier + OG image card |
| Retail copy-trading tool builders | "Find 20 wallets similar to this known alpha" | Similarity API ($29-99/mo) |
| Token / L2 growth teams | "What % of our holders are mercenary farmers vs diamond hands?" | Token-holder segmentation API ($99/mo) |
| ML-curious recruiters reviewing Jobelo's portfolio | "Did he really train a GNN on on-chain data?" | GitHub repo + technical blog post |

### Explicit non-goals

- **NOT** identity attribution ("who owns this wallet") — that's Arkham's lane and borders security.
- **NOT** compliance / OFAC / malicious / risk scoring — Webacy day-job conflict.
- **NOT** generic dashboard / portfolio tracker — Zerion/DeBank already won.
- **NOT** multi-chain at v1 — Ethereum mainnet only to ship in 3 weekends.

---

## 2. Archetypes (v1 taxonomy, 8 classes)

Framing is **behavioral patterns**, not pejorative labels. Each wallet gets multi-label probabilities; sum > 1 allowed.

| # | Archetype | Defining behavioral signals |
|---|---|---|
| 1 | **Day Trader / Scalper** | High tx velocity, short hold times, many DEX swaps, median hold < 7d |
| 2 | **Long-term Holder** | Low tx velocity, concentrated portfolio, median hold > 180d |
| 3 | **Yield Farmer** | LP deposits, staking, reward claims, protocol-count high |
| 4 | **Airdrop Hunter** | Low-value tx across many protocols, min-required activity, "sybil shape" |
| 5 | **Automated / High-Frequency Trader** | Sub-minute tx intervals, deterministic gas patterns, 24/7 entropy |
| 6 | **Whale** | High $ value per tx, concentrated holdings, influence signals |
| 7 | **NFT Flipper** | High NFT trade frequency, short NFT hold, collection churn |
| 8 | **Casual / Newbie** | Low activity, mainstream tokens only, few approvals |

**Safety rails on framing**:
- Archetype 5 is labeled **"Automated / HFT"** — explicitly NOT "MEV bot / sandwich attacker / exploiter." We detect *behavioral automation*, never *harm*.
- No "malicious", "scam", "exploit" language anywhere in output. If a reviewer asks whether this is security, the answer must be: "No — we classify trading behavior patterns, not risk."

---

## 3. Data Pipeline

### 3.1 Sources

| Source | Purpose | Cost | Rate limit |
|---|---|---|---|
| **Dune API** (`/v1/sql`) | Historical feature backfill (batched SQL) | Free tier = 2.5K credits/mo; Pro = $390/mo for 25M credits | ~1 credit per row returned |
| **Alchemy** (Ethereum mainnet) | Fresh reads, real-time features at inference | Free = 300M CUs/mo | Plenty for <10k lookups/day |
| **Flipside Crypto** | Backup / cross-validation | Free tier | ~100 queries/day |
| **Etherscan API** | Address labels + verified contract check (minimal) | Free (5 req/s) | — |

**Primary plan**: Dune free tier for initial 50k-wallet training set; Alchemy for real-time inference. Upgrade to Dune Pro only if paid customers justify.

### 3.2 Sampling strategy (training set)

- **Universe**: Ethereum mainnet, last 90d
- **Filter**: wallets with ≥10 tx in the last 90d AND ≥$100 total tx value (excludes dust/inactive)
- **Stratified sample** to ensure archetype diversity: 50k wallets with balanced draws across activity tiers (10-50 tx, 50-500 tx, 500+ tx)
- **Exclusions**: known exchange hot wallets (Binance, Coinbase), bridge contracts, known smart contracts (EOA only for v1)
- **Storage**: raw tx data in DuckDB (Parquet files on disk, ~1-5 GB total)

### 3.3 Feature schema (~42 features per wallet, 90d rolling window)

```
# Activity & volume (6)
tx_count_total, tx_count_out, tx_count_in, unique_days_active,
total_value_usd, gas_spent_usd

# Temporal (5)
hours_of_day_entropy, inter_tx_time_median_sec, inter_tx_time_cv,
tx_count_nighttime, tx_count_business_hours

# Tokens & portfolio (6)
unique_erc20_held, unique_erc20_touched, portfolio_hhi,
unique_nft_collections, nft_trade_count, stablecoin_ratio

# Protocol interaction (7)
unique_contracts, dex_tx_count, lending_tx_count, staking_tx_count,
bridge_tx_count, nft_marketplace_tx_count, protocol_diversity_index

# Holding behavior (4)
median_hold_days, pct_positions_held_over_30d, pct_positions_held_over_180d,
quick_flip_ratio  # (bought+sold within 24h)

# PnL proxies (3)
realized_pnl_usd_estimate, win_rate_swaps, avg_trade_size_usd

# Gas behavior (3)
avg_gas_price_percentile, priority_fee_aggressiveness, gas_failure_rate

# Network & approvals (4)
unique_counterparties_out, recurring_counterparty_ratio,
unique_approvals, revoke_ratio

# Launch-day activity (2)
pct_tokens_bought_within_24h_of_deploy, first_buyer_count

# Archetype-specific signals (2)
airdrop_claim_count, min_required_activity_score  # sybil-shape heuristic
```

**Feature engineering lives in Polars** (fast, lazy, laptop-scale). See §8 for pipeline code structure.

---

## 4. ML Pipeline

### 4.1 Phase 1 — Unsupervised archetype discovery

**Goal**: derive human-interpretable clusters from raw behavior.

1. **Standardize**: `RobustScaler` (sklearn) — robust to outliers, critical given whale features.
2. **Reduce**: UMAP (umap-learn), 42 → 15 dims. Use `n_neighbors=50, min_dist=0.1` to preserve global structure.
3. **Cluster**: HDBSCAN (`min_cluster_size=200, min_samples=50, cluster_selection_method='eom'`). Expected output: 8–20 clusters + noise.
4. **Backup clustering**: Gaussian Mixture Model (15 components, full covariance) on standardized features — yields soft probabilities we'll reuse for calibrated labels.
5. **Manual archetype labeling**: for each cluster, sample 10 wallets, look them up on Etherscan + open-source label sets (Flipside tags, Dune public labels), write a 1-line description, map to one of the 8 archetypes in §2.
6. **Cluster → archetype map**: 1 cluster → 1 primary archetype; many-to-one allowed (multiple "flipper" clusters collapse into archetype 7).

**Kill checkpoint**: if clusters don't produce interpretable archetypes after 2 UMAP/HDBSCAN param sweeps, kill the project — the feature set is too weak.

### 4.2 Phase 2 — Calibrated supervised classifier

**Goal**: turn cluster assignments into per-wallet multi-label probabilities.

1. **Labels**: cluster → archetype mapping from Phase 1 becomes weak labels. Multi-label where a wallet's GMM soft probabilities put >15% on a secondary cluster.
2. **Model**: **LightGBM** one-vs-rest multi-label classifier (`sklearn.multioutput.MultiOutputClassifier` wrapping `lgb.LGBMClassifier`). 8 binary heads, one per archetype.
3. **Handle imbalance**: `class_weight='balanced'` + SMOTE on rare classes (whale, HFT) via `imbalanced-learn`.
4. **Calibration**: wrap each head in `CalibratedClassifierCV(method='isotonic', cv=5)` — critical for honest confidence scores ("this wallet is 78% scalper").
5. **Train / eval split**: 80/10/10, stratified on primary archetype.
6. **Metrics**:
   - Macro-F1 across archetypes (target > 0.6)
   - Per-archetype precision/recall
   - Brier score (calibration quality, target < 0.15)
   - Log-loss
7. **Hand-label test set**: 100 wallets (mix of famous addresses + random draws), hand-assign archetype, compare against model.
8. **Baseline to beat**: naive rules-based classifier on 5–10 hand-written thresholds. Model must beat rules on F1 or we're adding complexity for no reason.

### 4.3 Phase 3 — Graph embeddings for similarity

**Goal**: 128-dim wallet embeddings for k-NN "similar wallets" endpoint.

1. **Graph construction**:
   - **Nodes**: wallets (EOA) + contracts (ERC20 + NFT + DeFi protocols)
   - **Edges**: wallet → contract if any interaction in 90d window; edge weight = log(tx_count)
   - **Node features**: for wallets → the 42 engineered features; for contracts → (tx_count, unique_users, category_onehot)
   - **Size**: ~50k wallet nodes + ~10k contract nodes = ~60k nodes, ~500k–1M edges
2. **Model**: **GraphSAGE** (`torch_geometric.nn.SAGEConv`), 2-layer, hidden=256, output=128. Inductive — critical so new wallets embed without retraining.
3. **Training objective**:
   - **Primary**: semi-supervised — classifier head on top of embeddings uses Phase 2 archetype labels as auxiliary signal. Cross-entropy loss + small L2.
   - **Self-supervised option**: BGRL (Bootstrap Graph Latent) or simpler — sampled neighbor reconstruction. Use if the semi-supervised version underfits.
4. **Output**: 128-dim L2-normalized embedding per wallet. Stored in Postgres via **pgvector** with HNSW index.
5. **Inference on unseen wallets**: rebuild local 2-hop subgraph from Alchemy, run forward pass, return embedding + top-K cosine-neighbors.
6. **Evaluation**:
   - **Recall@10** against public label sets: take wallets with Nansen-free public labels (Vitalik, a16z, Binance 1, etc.), check if top-10 neighbors share the label.
   - **Qualitative**: sample 20 query wallets, manually review top-10 neighbors on Etherscan for plausibility.

### 4.4 Versioning & retraining

- Weekly retrain cadence (cron on Modal), rolling 90d window.
- Model artifacts versioned in S3 (or Modal volumes). SemVer: `v1.x.0` for data refreshes, `v1.0.x` for code patches.
- API exposes `model_version` field in every response for reproducibility.

---

## 5. API Design

### 5.1 Endpoints

```
POST /api/v1/personas/wallet
  Body: { "address": "0x...", "chain": "ethereum" }
  Returns: archetypes[], features[], model_version
  Rate: 10/day free, 1k/day Pro, 10k/day Build

POST /api/v1/personas/batch
  Body: { "addresses": ["0x...", "0x..."], "chain": "ethereum" }
  Max 100 addresses per call.

POST /api/v1/personas/similar
  Body: { "address": "0x...", "k": 20, "chain": "ethereum" }
  Returns: [{ "address", "similarity_score", "archetypes" }, ...]

POST /api/v1/personas/token-holders
  Body: { "token_contract": "0x...", "chain": "ethereum", "sample_size": 1000 }
  Returns: { "archetype_distribution": { "scalper": 0.12, "holder": 0.34, ... }, "sample_size": 1000 }

GET  /api/v1/personas/archetypes
  Returns: archetype definitions + methodology link

GET  /api/v1/health
```

### 5.2 Response shape

```json
{
  "address": "0xAbC...",
  "chain": "ethereum",
  "model_version": "1.3.0",
  "computed_at": "2026-04-20T10:23:00Z",
  "archetypes": [
    { "name": "yield_farmer", "probability": 0.78, "confidence": "high" },
    { "name": "long_term_holder", "probability": 0.34, "confidence": "medium" }
  ],
  "primary_archetype": "yield_farmer",
  "features_snapshot": {
    "tx_count_90d": 312,
    "median_hold_days": 47.2,
    "unique_protocols": 14,
    "...": "..."
  },
  "explain": {
    "top_features": ["lending_tx_count", "staking_tx_count", "protocol_diversity_index"],
    "methodology_url": "https://walletpersona.app/methodology"
  }
}
```

### 5.3 Auth & rate limiting

- API keys via simple Postgres-backed table. No OAuth in v1.
- Rate limiting: Upstash Redis (free tier) or simple Postgres counters with advisory locks.
- Public rate-limited endpoint for persona-card generation (no key needed, 5/IP/min).

### 5.4 Pricing

| Tier | Price | Wallets/day | Features |
|---|---|---|---|
| Free | $0 | 10 | Single wallet lookup, persona card |
| Pro | $29/mo | 1,000 | Batch API, CSV export, similarity search (k≤5) |
| Build | $99/mo | 10,000 | Similarity (k≤50), token-holder segmentation, priority queue |
| Enterprise | Custom | 100k+ | Multi-chain, SLA, custom archetypes |

---

## 6. Frontend

### 6.1 Pages (Next.js 15 App Router + Tailwind + shadcn/ui)

- `/` — landing: hero ("Classify any Ethereum wallet in 200ms"), live input box (try any address), 3 sample persona cards
- `/w/[address]` — public wallet detail page (SEO target: long-tail `wallet <addr>` searches). OG image dynamically generated.
- `/methodology` — **open methodology doc** (the differentiator vs Nansen). Explains archetypes, features, model. GitHub link.
- `/docs` — API reference (auto-generated from OpenAPI via Scalar or Fumadocs)
- `/pricing`
- `/explore` — browse by archetype, famous-wallet examples per category
- `/dashboard` — logged-in user: API key, usage, billing (Stripe Checkout)

### 6.2 Persona Card (viral loop)

- Dynamic OG image via `@vercel/og` at `/og/[address].png`
- Format: wallet short address → primary archetype + secondary → 3 signature stats (tx/day, median hold, unique protocols) → QR to `/w/[address]`
- Twitter card meta tags, Farcaster Frame support
- "Share this wallet" button copies `https://walletpersona.app/w/0x...` — triggers re-fetch and re-generation

### 6.3 SEO strategy

- Programmatic pages for every wallet queried at least 3 times (cached on CDN)
- Sitemap by archetype: `/archetypes/yield-farmer` with top 100 public examples
- Blog: "Methodology deep-dive", "Top 10 yield farmers on Ethereum this week" (autogenerated weekly)

---

## 7. Stack Summary

| Layer | Tech | Why |
|---|---|---|
| Language (ML/API) | Python 3.12, managed with **uv** | Fast installs, lockfile |
| Language (frontend) | TypeScript + Next.js 15 | Jobelo's strength, Vercel deploys |
| API framework | **FastAPI** + Pydantic v2 | Async, OpenAPI auto-gen, ecosystem |
| Data processing | **Polars** + **DuckDB** | Lazy, laptop-scale, no Spark needed |
| Classical ML | scikit-learn (HDBSCAN, UMAP, GMM, CalibratedClassifierCV), **LightGBM**, imbalanced-learn | Proven, fast, reviewable |
| Deep learning | **PyTorch 2.x** + **PyTorch Geometric** | GraphSAGE is the showcase piece |
| Vector search | **Postgres + pgvector** (HNSW index) | One less service than Qdrant |
| Compute / serving | **Modal** (autoscale, GPU cold-starts) | Generous free tier, Python-native |
| Scheduling | Modal cron (weekly retrain) | Already in Modal |
| Database | Postgres (Neon or Supabase free tier) | Vector + relational in one |
| Cache / rate limit | Upstash Redis (free) | Simple |
| Frontend | Next.js 15 App Router, Tailwind, shadcn/ui, `@vercel/og` | Jobelo's stack |
| Payments | Stripe Checkout + Stripe webhooks | Standard |
| Blockchain data | Dune API (backfill) + Alchemy (fresh) + Flipside (cross-validation) | Free tiers sufficient initially |
| Observability | Logfire or OpenTelemetry + Grafana Cloud free tier | Cheap |
| Hosting | Vercel (frontend) + Modal (backend) + Neon (DB) | Zero-ops |

**Total fixed cost to ship**: ~$0–50/mo ($0 for frontend/DB/Modal free tiers; $29/mo optional Logfire; add $390/mo Dune Pro only when paid customers justify).

---

## 8. Repo Structure (projects/wallet-persona/)

```
wallet-persona/
├── CLAUDE.md
├── README.md
├── .env.example
├── docker-compose.yml          # Postgres + pgvector for local dev
├── apps/
│   ├── web/                    # Next.js 15 frontend
│   │   ├── app/
│   │   ├── components/
│   │   └── lib/og/             # persona card generator
│   └── api/                    # FastAPI serving
│       ├── main.py
│       ├── routes/
│       └── inference/
├── ml/                         # Python ML pipeline
│   ├── pyproject.toml
│   ├── pipelines/
│   │   ├── ingest.py           # Dune/Alchemy pulls
│   │   ├── features.py         # Polars feature engineering
│   │   ├── cluster.py          # UMAP + HDBSCAN discovery
│   │   ├── train_classifier.py # LightGBM multi-label
│   │   └── train_gnn.py        # GraphSAGE in PyG
│   ├── models/                 # saved artifacts (gitignored)
│   ├── notebooks/              # exploratory, shown in portfolio
│   │   ├── 01-feature-exploration.ipynb
│   │   ├── 02-cluster-discovery.ipynb
│   │   └── 03-gnn-embedding-eval.ipynb
│   └── eval/
│       ├── hand_labels.csv     # 100 wallets, manually tagged
│       └── metrics.py
├── infra/
│   └── modal/                  # Modal app definitions (train + serve)
└── scripts/
    ├── retrain.sh
    └── publish_blog_post.sh
```

**git init** — public repo from day 1. Portfolio reviewers look at the repo; commit history matters.

---

## 9. Execution Plan (3 weekends + launch)

### Weekend 1 — Data + Features (kill checkpoint at end)

| Day | Tasks | Output |
|---|---|---|
| Sat AM | Dune queries: 50k active wallet addresses + 90d tx history | `data/wallets.parquet`, `data/txs.parquet` |
| Sat PM | Polars feature pipeline (~42 features) | `ml/pipelines/features.py`, `data/features.parquet` |
| Sun AM | Validate: pull 20 known wallets (Vitalik, a16z, known flipper from Twitter, known yield farmer), inspect features manually | notes in `notebooks/01-feature-exploration.ipynb` |
| Sun PM | **Kill checkpoint**: do the features clearly separate the 20 known wallets? If yes → go to Weekend 2. If no → kill or re-scope. | Go / no-go decision |

### Weekend 2 — ML Discovery + Classifier

| Day | Tasks | Output |
|---|---|---|
| Sat AM | UMAP + HDBSCAN on 50k. Iterate params until ≥8 interpretable clusters | `notebooks/02-cluster-discovery.ipynb` |
| Sat PM | Hand-label clusters → archetype map. Write methodology draft. | `ml/pipelines/cluster_to_archetype.yaml` |
| Sun AM | Train LightGBM multi-label + calibration. Evaluate: macro-F1, Brier, confusion matrix | `ml/pipelines/train_classifier.py`, `eval/metrics_v1.json` |
| Sun PM | Hand-label 100-wallet test set. Compare model vs rules baseline. | `eval/hand_labels.csv` |

**Kill checkpoint**: macro-F1 ≥ 0.55 AND model beats rules baseline. If no → kill or pivot to simpler rules-based product (less portfolio value).

### Weekend 3 — GNN + API + Frontend

| Day | Tasks | Output |
|---|---|---|
| Sat AM | Build bipartite graph + train 2-layer GraphSAGE with semi-supervised archetype head | `ml/pipelines/train_gnn.py`, `models/gnn_v1.pt` |
| Sat PM | Eval embeddings: Recall@10 on public labels, qualitative top-10 review | `notebooks/03-gnn-embedding-eval.ipynb` |
| Sun AM | FastAPI endpoints + pgvector index + Modal deploy | live at `api.walletpersona.app` |
| Sun PM | Next.js frontend: landing + `/w/[address]` + `/og/[address]` | deployed on Vercel |

### Launch Weekend — Distribution

| Day | Tasks |
|---|---|
| Sat | Technical blog post: "Classifying 50k Ethereum wallets with GraphSAGE + HDBSCAN" (Substack + dev.to + Warpcast). Open-source the repo. |
| Sun | Launch posts: X, Warpcast, r/ethdev, r/MachineLearning, Hacker News ("Show HN"). Submit to crypto dev newsletters (Week in Ethereum, Bankless dev). |

---

## 10. Portfolio Narrative

The **GitHub README** and **LinkedIn announcement** should hit every keyword from the LinkedIn post that triggered this:

> Built a dev-facing API that classifies Ethereum wallets into 8 trader archetypes in ~200ms. The ML stack: HDBSCAN on UMAP-reduced behavioral features (unsupervised archetype discovery on 50k active wallets), a calibrated LightGBM multi-label classifier with isotonic calibration (macro-F1 = X.XX, beats rules baseline by Y%), and a 2-layer GraphSAGE GNN trained on the wallet-contract interaction graph for embedding-based similarity search via pgvector. Served from FastAPI on Modal with conformal prediction intervals; shareable persona cards generated with @vercel/og. Open methodology, free tier, and MIT-licensed notebooks.

Keywords hit: embeddings, GNN, classification, clustering, calibration, conformal, fine-tuning implied, production serving, vector DB, open source, eval.

**Companion artifacts** (multiply the portfolio value):
1. **Public Kaggle/Colab notebook** replicating a subset of the training on synthetic data (so recruiters can run it without API keys).
2. **Blog post** with honest methodology + baseline comparison (this is what senior ML hiring managers look for).
3. **Short Loom** (4 min) demoing the API + persona cards — attach to Toptal profile.

---

## 11. Risks & Open Questions

| Risk | Mitigation |
|---|---|
| Nansen labels are copyrighted; can't use as labels | Not using them. Clustering-derived weak labels + manual hand-labels of 100-wallet test set. |
| Archetypes are subjective, reviewers will push back | Publish methodology doc; version the taxonomy; allow user-facing confidence scores + "explain" endpoint. |
| Dune free tier may be insufficient for 50k-wallet backfill | Start with 10k wallets; scale to 50k only after feature validation passes. Flipside as backup. |
| Alchemy free tier exhausted at scale | Add rate limiting + caching. Upgrade only when MRR > $100. |
| "MEV bot" / "automated trader" labels might attract security framing | Use **"Automated / HFT"** label; avoid "bot", "attacker", "exploit" vocabulary. Methodology doc explicitly states: *"we classify behavioral patterns, not risk or harm."* |
| Jobelo's day-job employer (Webacy) objects | Spec is explicitly non-security (trader/growth analytics); avoid *any* OFAC / compliance / malicious framing in docs, marketing, API field names. Worth a proactive sanity-check with manager before public launch. |
| Model drift over time (Ethereum behavior shifts with new chains, Pectra EIPs, etc.) | Weekly retraining. Version model; expose model_version in every response. |
| Privacy / ethics: we're linking public wallets to behavioral labels | Wallet addresses are public; we do not do identity attribution; add "report inaccurate classification" feedback link. |
| Low API signups → feels like a failure | Portfolio value is realized at launch regardless of paying customers. Define success as (a) blog post traction + GitHub stars, (b) ≥1 hiring-manager inbound referencing the repo. |

---

## 12. Success Criteria

### Portfolio success (primary)

- Repo shipped public, README clean, notebooks run end-to-end
- Blog post published on dev.to / Substack with honest metrics
- LinkedIn announcement gets ≥20 substantive reactions from ML/crypto folks
- ≥50 GitHub stars in 4 weeks
- ≥1 inbound recruiter/client mention within 60 days

### Product success (secondary, nice-to-have)

- ≥500 wallets classified via free tier in first month
- ≥3 paying customers on Pro tier in first 90 days
- ≥1 API integration published by a third party (newsletter tool, dashboard, etc.)

### Kill criteria

- Weekend 1: features don't separate known wallets → kill
- Weekend 2: macro-F1 < 0.55 AND rules baseline wins → kill or pivot
- Month 1 post-launch: <10 GitHub stars AND 0 inbound interest → portfolio-complete, move on, don't sink more time

---

## 13. Next Steps

1. Confirm commitment to build (decision required — this is ~50-70 hours of focused work).
2. If yes: create `projects/wallet-persona/` scaffold, `git init`, add project CLAUDE.md.
3. Start Weekend 1 ingest queries on Dune; validate the "20 known wallets" sanity check.
4. Proceed only if kill checkpoint passes.
