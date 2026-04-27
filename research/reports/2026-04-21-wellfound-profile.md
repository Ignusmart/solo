# Wellfound Profile — Audit and Proposed Rewrites

**Date:** 2026-04-21
**Target profile:** Jobelo Andrés Quintero Rodríguez on Wellfound
**Positioning alignment:** Matches ignusmart.com + CV (`projects/cv/resume.pdf`) versatile Principal Engineer framing — AI · Full-Stack · Web3.

---

## Top issues (ranked by impact)

1. **"Eight years" → 10+ years** — stale; recruiter filters will auto-reject.
2. **Webacy title: "Software Engineer"** should be **Principal Software Engineer** — affects salary calibration and search ranking.
3. **Miroculus shows "Present"** but left in 2022.
4. **Integra Biosciences missing entirely** (2023–Present).
5. **Achievements paragraph is generic** — no stats, no AI/agent story, dated phrasing ("passion for delivering service").
6. **Skills missing ~15 high-value tags**: MCP, Claude, Foundry, ethers.js, AWS, Terraform, Docker, React Native, CrewAI, LangGraph, etc.
7. **Webacy tech tags have Redux** (dead) and no TypeScript/Solidity/AI.
8. **Education missing** Udacity Blockchain Developer cert + DataCamp Data Science track.
9. **Desired Role: "Software Engineer"** — wrong grade for $170K+ Principal market.
10. **"Quiet office" want** contradicts "Remote Preferred".

---

## Proposed rewrites (copy-paste ready)

### "Looking for" (short field)

```
Principal-level role building AI agent systems, Web3 tooling, or full-stack SaaS. I design across the stack, ship with AI-augmented workflows, and thrive in async remote teams. Builder-track, not manager-track.
```

### "Achievements" (narrative field)

```
Principal Software Engineer with 10+ years shipping production systems across three domains: AI & Agentic Systems, Blockchain & Web3, and Full-Stack Engineering. 45+ production systems shipped, 20+ smart contract protocols audited, and 10+ AI agent systems deployed — including multi-agent orchestration with CrewAI, LangGraph, and the Model Context Protocol (MCP).

At Webacy I architect a Web3 risk intelligence platform spanning 8+ EVM chains — TypeScript APIs, React/Next.js dApp frontends, ML risk classifiers, and data pipelines processing millions of on-chain transactions. In parallel I build agentic tooling that my team uses to ship at ~3x velocity without accruing technical debt.

I don't just use AI — I build the agent systems AND use them in the dev loop. My stack spans Solidity smart contract security (Foundry, Slither, Aderyn), full-stack TypeScript (React, Next.js, Node.js), Python data pipelines, and cloud infra (AWS, Terraform, Docker).

I work async-first, prefer IC tracks over management, and lead through architecture and mentorship — not org charts.
```

---

## Experience — per entry

### Webacy

- **Title** → `Principal Software Engineer`
- **Tech tags** → `TypeScript, React, Next.js, Node.js, Solidity, AI Agents, PostgreSQL, AWS`
- **Description:**

```
Principal Engineer on a Web3 risk intelligence platform across 8+ EVM (Ethereum Virtual Machine) chains. Architect TypeScript APIs, Node.js services, and React/Next.js dApp frontends, backed by ML risk classifiers and data pipelines processing millions of on-chain transactions. Apply smart contract security tooling (Foundry, Slither, Aderyn) across 20+ audited protocols. Build multi-agent orchestration with Claude, MCP, and CrewAI that cuts feature delivery time by ~50% without sacrificing production quality. Lead cross-stack architecture decisions spanning smart contracts, backend APIs, frontend UX, and AI-augmented engineering loops.
```

> **Open decision:** current description mentions older product features (Backup Wallet, Panic Button, Wallet Notifications). Recommendation is to drop those and lead with risk-intelligence framing (matches CV, LinkedIn, ignusmart.com). If those features still feel important, add one short trailing sentence.

### Toptal

- **Title** → `Freelance Principal Engineer — AI, Full-Stack & Blockchain` (or closest Wellfound grade)
- **Tech tags** → `React, Next.js, Node.js, Solidity, Python, AI Agents`
- **Description (replace boilerplate):**

```
Member of Toptal's top-3% freelance network. Deliver full-stack TypeScript and Python applications for fintech, blockchain, and healthcare clients — architecture through production deployment. Consult on AI-augmented engineering adoption and smart contract security reviews; agentic workflow rollouts cut delivery cycles by ~30% for client teams. Mentor senior engineers on systems design and modern stack selection.
```

### Integra Biosciences — ADD (missing)

- **Title:** Consulting Software Engineer
- **Dates:** 2023 – Present
- **Tech:** React, Node.js, Python
- **Description:**

```
Architect modular React and Node.js software for laboratory automation — drag-and-drop experiment design, scientific data pipelines, and real-time instrument telemetry across heterogeneous hardware.
```

### Miroculus

- **Fix dates:** `Feb 2018 – Dec 2022` (not Present)
- **Tech tags:** React, TypeScript, Python
- Description is fine as-is.

### Youse / Volaires / Twnel / Codetag

- Descriptions are acceptable.
- Minor cleanup: drop "triple constraints of time, scope, and budget" cliché from Youse.

---

## Skills

### Remove (stale / low-signal)

- `Play` (framework unclear, likely dead)
- `Security` (too vague → replace with `Smart Contract Security`)
- `Automation` (too vague)
- `Infrastructure` (too vague → replace with specific tools)
- `HTML`, `CSS` (implicit in any frontend role, crowd the tag list)

### Add (prioritized by differentiation value)

1. Solidity (already there)
2. EVM
3. Foundry
4. Hardhat
5. ethers.js
6. Smart Contract Security
7. Slither / Aderyn
8. TypeScript (already there)
9. React / React Native
10. Next.js (already there)
11. Node.js (already there)
12. Python (already there)
13. Claude / MCP (Model Context Protocol)
14. CrewAI / LangGraph
15. Agentic AI
16. AWS
17. Terraform
18. Docker
19. PostgreSQL
20. CI/CD

### Final ordered skills list (first 12–15 are most visible on Wellfound)

```
Solidity, EVM, Foundry, Smart Contract Security, ethers.js, TypeScript,
React, Next.js, Node.js, React Native, Python, Claude, MCP, CrewAI,
LangGraph, Agentic AI, AWS, Terraform, Docker, PostgreSQL, Django,
TailwindCSS, Git
```

---

## Education — ADD

- **Blockchain Developer** (2022) — Udacity, ID# D7GGFQYG
- **Data Science with Python** (2021) — DataCamp

---

## Ideal next opportunity

- **Desired Role** → `Principal Engineer` or `Staff Engineer` (fall back to `Full-Stack Engineer` if dropdown limits).
- **Desired Salary** → $170K is low for US-remote Principal. Consider **$200–220K** if targeting US-pay markets; keep $170K for LATAM-remote bands. Decision pending.
- **Desired Tech Stack** → add **Solidity** (missing despite being in skills), **MCP**, **Agentic AI**.
- **Company Focus** → keep AI/ML + Blockchain; **drop Games** (doesn't match portfolio); add **Developer Tools** / **SaaS** if available.
- **Wants** → **remove "Quiet office"** (contradicts remote preference).

---

## Checklist before publishing

- [ ] Bump experience from 8 to 10+ years everywhere
- [ ] Update Webacy title to Principal Software Engineer
- [ ] Rewrite Webacy description (risk intelligence framing)
- [ ] Fix Miroculus end date (Dec 2022)
- [ ] Add Integra Biosciences entry
- [ ] Replace Achievements paragraph
- [ ] Replace Looking for paragraph
- [ ] Remove stale skills (Play, Security, Automation, Infrastructure, HTML, CSS)
- [ ] Add missing skills (AI stack, blockchain tooling, infra)
- [ ] Add Udacity + DataCamp under Education
- [ ] Update Desired Role → Principal/Staff
- [ ] Revise Desired Tech Stack (add Solidity, MCP)
- [ ] Drop Games from Company Focus; add Dev Tools / SaaS
- [ ] Remove "Quiet office" from Wants
- [ ] Decide on salary ($170K vs $200–220K)
