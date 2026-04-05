# CI/CD & DevOps MCP Servers — Landscape Analysis (April 2026)

## Executive Summary

The DevOps MCP server ecosystem has exploded: 11,000+ MCP servers exist overall, but **less than 5% are monetized**. Most CI/CD and DevOps servers are free/open-source, community-built, and demo-quality. The few enterprise-backed ones (GitHub, AWS, HashiCorp, Microsoft) focus on CRUD operations — triggering builds, reading logs, managing resources. **Deep intelligence layers (failure analysis, cost correlation, multi-pipeline orchestration) are either missing or extremely early-stage.** This is the gap.

---

## 1. What CI/CD MCP Servers Exist

### Official / Vendor-Backed (Free)

| Server | Maintainer | Stars | What It Does |
|--------|-----------|-------|-------------|
| [github/github-mcp-server](https://github.com/github/github-mcp-server) | GitHub (Official) | 28,500+ | Repos, issues, PRs, code search, trigger GitHub Actions workflows. Lockdown mode for public repos. |
| [GitLab MCP Server](https://docs.gitlab.com/user/gitlab_duo/model_context_protocol/mcp_server/) | GitLab (Official) | — | Issues, merge requests, pipelines, commits, cross-project search. Requires GitLab 18.6+. |
| [microsoft/azure-devops-mcp](https://github.com/microsoft/azure-devops-mcp) | Microsoft (Official) | — | Repos, work items, pipelines, boards. Remote MCP server in public preview. CVE-2026-32211 disclosed (CVSS 9.1 — missing auth). |
| [CircleCI MCP Server](https://circleci.com/blog/resolve-ci-test-failures-with-ai/) | CircleCI | — | Identifies, understands, and resolves failing tests in CI/CD builds directly in the editor. |
| Argo CD MCP | Akuity (Official) | — | Natural language GitOps: sync, rollback, query app status. Built by Argo CD creators. |

### Community-Built (Free, Open Source)

| Server | Stars | Notes |
|--------|-------|-------|
| [ko1ynnky/github-actions-mcp-server](https://github.com/ko1ynnky/github-actions-mcp-server) | 40 | GitHub Actions-specific. |
| [Jordan-Jarvis/jenkins-mcp-enterprise](https://github.com/Jordan-Jarvis/jenkins-mcp-enterprise) | 22 | **Most advanced Jenkins MCP.** AI-powered failure analysis, vector search, multi-instance, 10GB+ log handling. Free/OSS. |
| [Daghis/teamcity-mcp](https://github.com/Daghis/teamcity-mcp) | 22 | JetBrains TeamCity: builds, tests, agents, configs. |
| [Alosies/gitlab-mcp-server](https://github.com/Alosies/gitlab-mcp-server) | 9 | Fully-typed TypeScript. Projects, issues, MRs, CI/CD pipelines, job logs. |
| [stefanoamorelli/codemagic-mcp](https://github.com/stefanoamorelli/codemagic-mcp) | 7 | Codemagic CI/CD (mobile-focused). |
| [shalwin04/GitLab-CICD-Agent](https://github.com/shalwin04/GitLab-CICD-Agent) | 13 | Multi-agent system for GitLab CI/CD using LangGraphJS. |
| [mcncl/zed-mcp-server-buildkite](https://github.com/mcncl/zed-mcp-server-buildkite) | 3 | Buildkite integration for Zed editor. |
| [kud/mcp-jenkins](https://github.com/kud/mcp-jenkins) | 3 | 25+ tools for Jenkins jobs, builds, workflows. |
| Jenkins MCP Plugin (Official) | — | Server-side Jenkins plugin implementing MCP spec. |

### Key Observation
Most CI/CD MCP servers are **thin wrappers over existing APIs** — they let you trigger builds and read logs, but don't analyze, correlate, or reason about failures. The Jenkins Enterprise server is the one notable exception, but it has only 22 stars and is a single-maintainer project.

---

## 2. DevOps / Infrastructure MCP Servers

### Infrastructure as Code

| Server | Maintainer | Status |
|--------|-----------|--------|
| [hashicorp/terraform-mcp-server](https://github.com/hashicorp/terraform-mcp-server) | HashiCorp (Official) | Beta. Registry search, workspace mgmt, plan/apply, state inspection. On Docker Hub. |
| [pulumi/mcp-server](https://github.com/pulumi/mcp-server) | Pulumi (Official) | Stack queries, resource search. Remote endpoint available. |
| [opentofu/opentofu-mcp-server](https://github.com/opentofu/opentofu-mcp-server) | OpenTofu (Official) | Registry search, provider/module docs. Remote endpoint: mcp.opentofu.org |
| [hashicorp/vault-mcp-server](https://github.com/hashicorp/vault-mcp-server) | HashiCorp (Official) | Beta. Secrets management. Warning: secrets exposure risk. |

### Kubernetes & Containers

| Server | Focus |
|--------|-------|
| [containers/kubernetes-mcp-server](https://github.com/containers/kubernetes-mcp-server) | Native Go, no kubectl dependency, multi-cluster. |
| [Azure/mcp-kubernetes](https://github.com/Azure/mcp-kubernetes) | Microsoft. Unified kubectl interface, minimal context consumption. |
| [Flux159/mcp-server-kubernetes](https://github.com/Flux159/mcp-server-kubernetes) | Non-destructive mode, secrets masking. Popular community pick. |
| [alexei-led/k8s-mcp-server](https://github.com/alexei-led/k8s-mcp-server) | Multi-tool: kubectl + helm + istioctl + argocd in one server. |
| Docker MCP | Container image ops, registry mgmt, local builds. |

### Cloud Platforms

| Server | Maintainer |
|--------|-----------|
| [awslabs/mcp](https://github.com/awslabs/mcp) | AWS (Official). 8,600+ stars. Multiple sub-servers for different AWS services. |
| [Azure DevOps MCP](https://github.com/microsoft/azure-devops-mcp) | Microsoft (Official). |
| GCP MCP | Google Cloud Platform interactions via MCP. |

### Monitoring & Observability

| Server | What It Does |
|--------|-------------|
| Datadog MCP | Bridge between Datadog observability data and AI agents. Query metrics, logs, traces. |
| [grafana/mcp-grafana](https://github.com/grafana/mcp-grafana) | Dashboard searches, datasource queries, incident management. |
| PagerDuty MCP | On-call management, incident response, escalation. Cloud-hosted, integrates with Azure SRE Agent. |
| Mezmo AI SRE | Agentic SRE for root cause analysis. Claims 80% MTTR improvement. |

### Security Scanning

| Server | What It Does |
|--------|-------------|
| [jmstar85/DevSecOps-MCP](https://github.com/jmstar85/DevSecOps-MCP) | Integrates Semgrep, Bandit, OWASP ZAP, Trivy, npm audit, OSV Scanner. SAST+DAST+IAST+SCA. 100% OSS. |
| [armyknife-social/kryptonclaw](https://github.com/armyknife-social/kryptonclaw) | GitHub Actions security scanner. 30+ attack patterns. CLI + MCP + SARIF. |
| [duriantaco/skylos](https://github.com/duriantaco/skylos) | Python/TS/Go SAST. Dead code detection, secret detection. 362 stars. |
| [affaan-m/agentshield](https://github.com/affaan-m/agentshield) | AI agent security scanner. MCP server config vulnerability detection. 308 stars. |

### Cost Analysis

| Server | What It Does |
|--------|-------------|
| AWS Billing & Cost Management MCP | Official AWS. Natural language cost queries, savings recommendations, FinOps audits. |
| AWS Cost Explorer MCP | Community. Break down costs by service, region, usage tier. |
| Vantage Cloud Cost Management MCP | **Multi-cloud** (AWS, Azure, etc.). Spending patterns, budget tracking, anomaly detection. |

---

## 3. What's Missing — Gap Analysis

### 3.1 CI/CD Failure Analysis (Intelligence Layer)

**Current state:** Most servers just surface raw logs. Only two projects attempt intelligent analysis:
- **jenkins-mcp-enterprise** (22 stars) — vector search over logs, pattern matching, but Jenkins-only and single maintainer.
- **CircleCI MCP** — identifies failing tests but locked to CircleCI ecosystem.
- **LogSage** (academic paper) — first end-to-end LLM framework for CI/CD failure RCA and remediation.

**Gap:** No **CI-platform-agnostic** failure analysis MCP server exists. Nothing that works across GitHub Actions + GitLab CI + Jenkins + CircleCI and:
- Classifies failure types (flaky test, dependency issue, infra timeout, config drift, OOM)
- Correlates failures across branches/PRs
- Suggests specific fixes (not just "check the logs")
- Tracks failure patterns over time (regression detection)
- Estimates time-to-fix based on historical data

### 3.2 Multi-Pipeline Orchestration

**Current state:** Each CI/CD MCP server is a **silo**. You can trigger a GitHub Actions workflow OR query a Jenkins build, but nothing coordinates across them.

**Gap:** No MCP server handles:
- Cross-platform pipeline visualization (e.g., GitHub Actions triggers Jenkins which deploys via Argo CD)
- Dependency-aware deployment ordering across services
- Unified status dashboard across CI providers
- "What's blocking this deployment?" queries that span multiple systems

### 3.3 Infrastructure Cost Analysis

**Current state:** AWS has strong coverage with official Billing MCP + Cost Explorer MCP. Vantage offers multi-cloud.

**Gap:** 
- No Terraform/Pulumi cost estimation BEFORE apply (pre-deploy cost prediction)
- No "what would this PR cost in infra changes?" integration
- No FinOps MCP that ties CI/CD costs (build minutes) + infra costs (cloud spend) + developer time into a unified view
- GCP and Azure cost analysis MCP servers lag behind AWS

### 3.4 Security Scanning Integration

**Current state:** DevSecOps-MCP exists but is low-traction. Individual tools exist (Skylos, AgentShield, Kryptonclaw).

**Gap:**
- No unified "security gate" MCP that integrates into CI/CD and aggregates findings from SAST + DAST + SCA + secrets scanning + container scanning into a single risk score
- No MCP server that maps vulnerabilities to deployment risk ("this CVE is in a service that handles PII and is deployed to prod")
- No automated PR-blocking based on security policy thresholds via MCP

### 3.5 Deployment Rollback Automation

**Current state:** Argo CD MCP supports rollback commands. Kubernetes MCP servers can scale/restart pods.

**Gap:**
- No intelligent rollback MCP that monitors post-deploy metrics and auto-triggers rollback based on error rate spikes, latency increases, or health check failures
- No cross-service rollback coordination ("service A depends on service B, rollback both")
- No rollback with blast radius analysis ("what will break if we rollback this service?")

---

## 4. Developer Complaints

### Security Concerns (Critical)
- **CVE-2026-32211**: Azure MCP Server missing authentication entirely (CVSS 9.1). No patch as of April 2026.
- Scan of 8,000 servers: **36.7% had SSRF vulnerabilities**, **43% had unsafe command execution paths**.
- 30 CVEs filed against MCP servers in the first 60 days of 2026.
- Vault MCP server beta explicitly warns about secrets exposure risk.

### Context Window Bloat
- MCP tool schemas consume massive token counts. One team burned **143,000 of 200,000 tokens (72%)** just on tool definitions.
- DevOps servers with many tools (Kubernetes, Terraform) are the worst offenders.

### Authentication is Painful
- OAuth flow requires browser — breaks in CI/CD and headless environments.
- No standardized service account / API key approach across MCP servers.
- Each server rolls its own auth, creating config sprawl.

### Quality Gap
- **5,000+ MCP servers on GitHub, most are demos.** Finding production-ready ones requires curation.
- Community servers are frequently abandoned (last commit months ago).
- Inconsistent error handling, poor documentation, no tests.

### Platform Lock-in
- Each CI/CD server only works with one platform. Teams running GitHub Actions + Jenkins (common) need two separate MCP servers with different configs.

---

## 5. Paid MCP Servers — What Exists

### DevOps-Adjacent Paid Servers
The paid MCP market is nascent. The few paid ones are data/enterprise focused, not DevOps:

| Server | Price | Focus |
|--------|-------|-------|
| Atlan MCP | $1,200-5,000/mo | Data governance |
| MindsDB MCP | $750-3,000+/mo | AI/ML databases |
| K2view MCP | ~$5,000/mo | Data integration |
| Vectara MCP | $1,000-4,500/mo | RAG/search |
| Snowflake MCP | $2,000-6,000/mo | Data warehouse |

### DevOps Specifically
- **No paid DevOps-specific MCP servers found.** Everything is free/OSS or bundled into existing platform pricing (Datadog, PagerDuty, etc. charge for their platform, the MCP server is free).
- Wagner (trywagner.dev) appears to be building an "AI DevOps teammate" product and curates the awesome-devops-mcp list — potential competitor, but no pricing visible yet.
- StackGen offers governance-enabled self-service infrastructure with MCP — enterprise sales model.

### Market Signal
- 8 million MCP downloads with 85% MoM growth.
- Less than 5% of servers are monetized.
- MCP server development costs: $25-50K for MVP, $60-120K for production SaaS.

---

## 6. What "10x Better" Looks Like

A winning CI/CD MCP server would combine what's currently spread across 5-10 separate tools into one **intelligence layer**:

### The "CI/CD Brain" Concept

**Core thesis:** Don't just read CI/CD data — **reason about it.**

1. **Universal Pipeline Adapter** — Single MCP server that connects to GitHub Actions, GitLab CI, Jenkins, CircleCI, Argo CD, Buildkite. One config, all platforms. (Nobody does this today.)

2. **Failure Intelligence Engine** — Not "here are your logs" but:
   - Auto-classifies failures (flaky test, dependency, OOM, config, timeout, permissions)
   - Shows similar past failures and what fixed them
   - Suggests specific code changes or config fixes
   - Detects flaky test patterns and quarantines them
   - Estimates fix time based on historical data

3. **Cross-Pipeline Visibility** — "What's blocking the deploy of service-X?" Answer spans GitHub Actions build -> security scan -> staging deploy -> integration tests -> prod deploy. One query, full picture.

4. **Pre-Deploy Risk Score** — Before merging a PR, answer:
   - What will this cost in infra? (Terraform cost estimation)
   - What security findings exist? (aggregate SAST/DAST/SCA)
   - What's the blast radius? (dependency graph analysis)
   - How confident is the test coverage?

5. **Smart Rollback** — Monitor post-deploy metrics (error rate, latency, 5xx) and either alert or auto-rollback. Know the dependency graph so rollbacks are coordinated.

6. **FinOps Integration** — Tie CI/CD build minutes ($) + infra changes ($) + developer time per failure into a cost-of-change metric.

### Why This Doesn't Exist Yet
- **Complexity**: Connecting to 5+ CI platforms is hard API work.
- **State**: You need to store historical data (failures, patterns, costs) — most MCP servers are stateless.
- **Security**: Teams are wary of giving AI agents access to CI/CD systems (43% have unsafe command execution).
- **Business model unclear**: Nobody has proven you can charge for a DevOps MCP server yet.

### Monetization Angles
- **Freemium**: Free for 1 CI platform + basic log reading. Paid for multi-platform, failure intelligence, cost analysis.
- **Per-seat or per-pipeline pricing**: $29-99/developer/month or $99-299/pipeline/month.
- **Enterprise**: Self-hosted, SSO, audit logs, $1,000-5,000/month.
- The Jenkins Enterprise MCP (free, 22 stars) proves there's demand for advanced failure analysis — a commercial multi-platform version could capture that market.

---

## Key Takeaway

The DevOps MCP space is wide but shallow. Lots of thin API wrappers, no intelligence layer. The opportunity is a **multi-platform CI/CD intelligence server** that does for build failures what Datadog did for infrastructure monitoring — aggregate, correlate, and surface actionable insights. Nobody is charging for this yet, and the tooling bar (just reading logs from 3+ CI platforms) is high enough to be defensible.
