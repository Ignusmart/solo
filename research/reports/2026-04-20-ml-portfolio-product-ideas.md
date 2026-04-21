# ML Portfolio Product Ideas — Deep Research

**Date**: 2026-04-20
**Trigger**: LinkedIn post on Python + AI/ML engineering premium ($46% salary gap in LATAM). Jobelo wants a portfolio piece that (a) showcases real ML depth (not just LLM wrappers), (b) leverages his Solidity/EVM/DeFi + TS/Python + agentic-AI moat, (c) avoids Web3 SECURITY (day-job conflict at Webacy), (d) respects the "research exhausted, build flywheel layers" directive.

**Credentials baseline** (from CV): DataCamp Data Scientist + Data Analyst with Python tracks (2021), Webacy blockchain data pipelines (Snowflake/Kafka), production LLM/agentic/MCP experience, 10y TS/Python full-stack, 4y Solidity/EVM/DeFi, biotech data pipelines (Miroculus NGS + Integra).

---

## TL;DR — Three Candidate Directions, Ranked

| # | Idea | Portfolio Strength | Revenue Upside | ML Depth Shown | Build Effort |
|---|------|:--:|:--:|:--:|:--:|
| **1** | **APIDelta ML layer — "LLM-agent contract regression detector"** | HIGH | MEDIUM (compounds existing product) | High (fine-tuned ModernBERT + semantic entropy) | 2-3 weekends |
| **2** | **Wallet persona API + similarity search ("Nansen-lite open methodology")** | HIGH | LOW-MED (crowded at product layer) | Very High (GraphSAGE + HDBSCAN + pgvector) | 2-3 weekends |
| **3** | **"APY Half-Life" — calibrated DeFi yield forecaster (vs DeFiLlama baseline)** | MEDIUM-HIGH | LOW (events dominate signal) | High (DeepAR + survival analysis + conformal) | 2-3 weekends |

**Recommended pick**: **#1 (APIDelta ML layer)**. It doesn't require a new product, it compounds the existing APIDelta moat (OpenAPI spec corpus), and "fine-tuned ModernBERT on 50k diffs, <100ms latency, shipped behind FastAPI/Modal" is exactly the portfolio narrative that matches the LinkedIn post's "AI/ML engineering premium" — it's production AI engineering, not toy notebooks.

---

## Direction 1 — APIDelta ML Layer ("LLM-Agent Contract Regression Detector")

### Framing

APIDelta already watches upstream APIs. The ML layer classifies every detected diff as: **cosmetic / breaking-behavior / new-feature / schema-shape**, with calibrated confidence. Sell as "schema regression testing for AI agents" — every team shipping agents that call OpenAI/Stripe/Anthropic/third-party APIs has this bug, nobody owns it.

### Market reality

- LLM eval/observability horizontal (Langfuse, Braintrust, Arize Phoenix, LangSmith, Helicone, Patronus, Ragas, DeepEval, TruLens) is **saturated** — already in `06-KILLED-IDEAS.md`. Skip.
- But **"upstream API regression → downstream LLM agent breakage"** is an under-owned niche. APIDelta is already upstream of this. No direct competitor ships it as a product.
- MCP server eval also under-served (~18-month-old protocol); secondary expansion angle.

### ML models / algorithms

**Primary (portfolio showcase)**: Fine-tune **ModernBERT-base** (149M, Dec 2024, 8k context, built for code/retrieval) on diff-pair classification.
- **Training set (~20–50k labeled pairs)**: APIs.guru OpenAPI directory + git history, oasdiff output as weak labels, semantic-release `BREAKING CHANGE:` footers from GitHub, PyPI yanked releases, hand-labeled gold set (~500) from Stripe/Twilio/Shopify changelogs.
- **Label generation**: Claude Haiku with Pydantic structured output labels 50k diffs → distill into ModernBERT via LoRA (PEFT lib).
- **Eval**: sklearn macro-F1, calibration via `mapie` (conformal prediction intervals).

**Secondary (cheap fallback baseline)**: sentence-transformers (BGE-small-en-v1.5 or jina-embeddings-v3) + XGBoost on `[before_emb, after_emb, delta_features]`. Ships in one weekend, <10ms, proves the classifier isn't just LLM magic.

**Tertiary (runtime layer)**: for the "agent output drift" side, use `selfcheckgpt` + NLI (`MoritzLaurer/DeBERTa-v3-base-mnli-fever-anli`) + **semantic entropy** (Farquhar et al., Nature 2024; ~200 LOC) to detect when agent responses shift after an upstream API change.

### Stack

- **Training/inference**: Python + HuggingFace Transformers + PEFT/LoRA, **Modal** for GPU jobs
- **Serving**: FastAPI + Pydantic, deployed on Modal (autoscale, cold-start-friendly)
- **Vector/embeddings**: pgvector in existing Postgres (avoid adding Qdrant)
- **Orchestration**: Inngest for scheduled diff runs (or Modal cron)
- **Data layer**: Postgres + ClickHouse only if events > 10M/mo
- **Frontend**: Next.js (reuse APIDelta UI)

### Portfolio narrative

> "Built an ML classifier (fine-tuned ModernBERT via LoRA on 50k distilled-label OpenAPI diffs) that tags upstream API changes as breaking/cosmetic/new-feature at <100ms latency. Deployed behind FastAPI/Modal with conformal prediction intervals for calibrated confidence. Shipped as a paid tier on APIDelta."

Hits: real training pipeline, distillation, fine-tuning, calibration, production serving. All the LinkedIn-post keywords (embeddings, eval, function calling adjacent, production ML).

---

## Direction 2 — Wallet Persona API + Similarity Search

### Framing

Developer-facing API: input = EVM wallet address, output = behavioral persona (scalper / yield farmer / airdrop hunter / whale / long-holder / bot) with confidence scores + top-K similar wallets via vector search. Three go-to-market angles layered on same engine:
- **Copy-trading scout** (similarity API, sold to newsletter writers/retail tools)
- **Shareable persona cards** (viral, @vercel/og images)
- **Token-team holder segmentation** (% mercenary farmers vs diamond hands, sold to L2s/protocols)

### Market reality

- **Nansen** owns labels + brand, but **closed API**, **enterprise pricing**, **rules-based/curated**, not ML embeddings.
- **0xScope** does entity clustering for identity resolution, not trader archetypes.
- **Arkham** = attribution ("who owns this"), not behavior.
- **Cielo/Zerion/DeBank/Zapper** = dashboards, no classification.
- **Dune/Flipside** = raw SQL, no shipped product.
- **Gap**: dev-facing ML-backed persona API with open methodology + embedding similarity endpoint. Nansen has data; nobody ships this API.

### ML models / algorithms

- **Feature engineering** (per wallet, rolling windows): avg hold duration, median gas, tx/day, unique contracts, MEV-bundle ratio, DEX-vs-CEX flow, approval count, airdrop-claim ratio, nightowl entropy, token-launch-day buy rate, PnL distribution.
- **Clustering (discover archetypes)**: **HDBSCAN** — handles variable-density clusters (whales sparse, airdrop farmers dense) far better than k-means.
- **Classification (per-wallet scoring on cluster labels)**: **XGBoost** or **LightGBM** multi-label with calibrated probabilities.
- **Graph embeddings (similarity)**: **GraphSAGE** via PyTorch Geometric — inductive (embeds new wallets without retraining), learns from wallet-token-contract tx graph. node2vec as a simpler baseline.
- **Optional flex**: small **transformer over tx sequences** (custom, <10M params) to show off sequence modeling.
- **Vector search**: **pgvector** (one service) or Qdrant (better at 10M+ wallets).

### Stack

- **Data**: Dune API (backfill), Alchemy/QuickNode (fresh reads), Flipside free tier. Skip Erigon self-host.
- **Processing**: **Polars + DuckDB** (laptop-scale feature pipelines)
- **ML**: scikit-learn, `hdbscan`, XGBoost, PyTorch Geometric
- **Serving**: FastAPI on Modal
- **Storage**: Postgres + pgvector
- **Frontend**: Next.js + Vercel, persona cards via `@vercel/og`

### Honest verdict

Crowded at product layer (Nansen), wide open at **ML/API layer**. As a **portfolio artifact demonstrating GNN + clustering + vector search on real Web3 data**, this is exceptional — every LinkedIn-post bullet, plus the Solidity/EVM moat that separates him from 90% of ML-curious backend devs. Revenue upside is capped because Nansen will out-feature him, but **persona cards are viral** and the copy-trading scout API is a real wedge.

---

## Direction 3 — "APY Half-Life" DeFi Yield Forecaster

### Framing

One number per pool: **"expected days until APY drops >30% from current"** — with conformal-interval confidence bands and feature attributions ("driven by: TVL inflow +40% last 7d, emission cliff in 12 days"). Positioned as "DeFiLlama's `predictions` field, but calibrated and continuous."

### Market reality

- **DeFiLlama Yields** already ships a crude `predictedClass` (Stable/Volatile/Down) field, free, ~ceiling baseline.
- **vaults.fyi** = curated vaults + smart-APY weighted averages, no ML.
- **Exponential.fi** = proprietary A-F risk ratings, rule-based, institutional.
- **Gauntlet/Chaos Labs** = enterprise sim, not retail forecasting.
- **Pendle ecosystem** — PT fair-value is a legit underserved niche (serious traders, high willingness-to-pay).
- Nobody ships real multi-horizon probabilistic forecasts with uncertainty. Gap exists — but exists because the signal is weak (see honest verdict).

### ML models / algorithms

- **Time-series (skip Prophet and ARIMA — wrong fit)**. Winners:
  - **LightGBM with lag/rolling features** — boring, ships fast, Kaggle-winning baseline.
  - **DeepAR** (GluonTS) — probabilistic intervals across 15k pools jointly (global model). Best fit for "one model, many pools."
  - **TFT or N-BEATS** via `pytorch-forecasting` — when you want multi-horizon + uncertainty.
- **Features that actually matter**: 7/30d TVL delta, utilization ratio, reward-token emission + decay schedule, reward-token price vol, pool age, chain-gas percentile, vote-escrow gauge weight, bribe $/veToken. Skip audit count (noisy).
- **Risk classifier**: LightGBM multi-class (stable / volatile / mercenary-decay) — beats DeFiLlama if you include emissions schedule + gauge features.
- **Survival analysis**: `lifelines` — Weibull or Cox proportional hazards for "half-life" framing.
- **Portfolio optimizer**: `cvxpy` for mean-variance + CVaR constraints. Skip RL (reward hacking is brutal on 3y data).
- **Anomaly**: `IsolationForest` / PyOD on **residuals from the forecaster**, not raw APY (APY jumps are often legitimate).
- **Calibration flex**: **`mapie` conformal prediction** — the single most portfolio-impressive addition.

### Stack

- **Data**: DeFiLlama `/yields/*` + `/protocols` (free), The Graph, Dune
- **Processing**: Polars + DuckDB
- **ML**: lightgbm, pytorch-forecasting, gluonts, lifelines, mapie, cvxpy
- **Serving**: FastAPI on Modal + scheduled retrain
- **Frontend**: Next.js + Recharts + @tanstack/react-table

### Honest verdict

ML realistically gives **10–20% lift** over a decent heuristic. APY collapses are event-driven (gauge reweights, emission cliffs, governance votes, depegs) — models see 0–3 days ahead at best. **Will not beat the market.** But: (a) clean ML narrative (survival + conformal + global DeepAR), (b) honest public backtest vs DeFiLlama baseline, (c) **Pendle PT fair-value** (alt framing) has real structural inefficiencies that are less arbed. Portfolio upside high; commercial upside modest.

---

## Cross-Cutting: Why NOT Other Obvious Directions

- **LLM eval/observability horizontal** — saturated, already in killed ideas.
- **Code-embedding search / "chat with codebase"** — CodeOnboard killed (2026-04-05); $900M+ competitor funding.
- **Doc staleness detection** — DocDrift killed; 5+ new competitors.
- **Smart contract security/audit ML** — violates Web3-security constraint (day job).
- **Biotech/lab data ML** — violates no-biotech feedback.
- **MEV predictor / front-running detection** — crosses Web3-security line in practice.
- **AI agent evaluation** — already killed as too crowded.

---

## Recommended Sequence

1. **Direction 1 (APIDelta ML layer)** — build first. Compounds an existing product, generates the most portfolio-legit artifact (fine-tuned ModernBERT + distillation + conformal calibration + production serving), zero new market research risk.
2. **Direction 2 (Wallet persona API)** — build second, IF APIDelta ML layer doesn't produce enough signal by the May 15 APIDelta kill-checkpoint. Persona cards are viral and the Web3 moat is strongest here.
3. **Direction 3 (APY Half-Life)** — only if he wants a DeFi-native portfolio piece specifically, OR if ScanAble/APIDelta both fail and a new product slot opens. Revenue upside weakest but ML narrative strong.

---

## Notes / Caveats

- WebSearch was unavailable during research; findings are based on platform knowledge through Jan 2026 + the repo's own killed-ideas log. Before building any direction, verify current competitor state (Nansen API pricing page, DeFiLlama predictions API spec, Langfuse/Braintrust funding numbers, MCP eval tools landscape).
- "Portfolio piece" ≠ "revenue-generating product." These three are weighted for portfolio credentialing first; none are predicted to hit meaningful MRR as solo plays against entrenched competitors.
- All three can be shipped as **OSS core + hosted tier** (mirrors Langfuse / DeFiLlama strategies) — this is also the shape that best converts into portfolio GitHub stars.
