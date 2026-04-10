You are showing Jobelo a consolidated status dashboard of ALL ideas across both research tracks (SaaS and Tools) and the implementation pipeline. This is a read-only command — it does NOT modify any files.

## What to do

Read the following files and output a single, unified status report:

### Files to read (all required):
1. `research/reports/2026-04-04-idea-leaderboard.md` — SaaS ideas from `/research-ideas`
2. `research/reports/tool-ideas-leaderboard.md` — utility tool ideas from `/research-tool-ideas`
3. `research/implementation/TRACKER.md` — implementation pipeline status
4. `research/implementation/unified-leaderboard.md` — unified leaderboard (if it exists)

### Files to count (for stats, don't read fully):
- Count `research/reports/*-market-gap-iteration-*.md` files → SaaS iteration count
- Count `research/reports/*-tool-ideas-iteration-*.md` files → Tool iteration count

### Optional per-idea detail (only if `$ARGUMENTS` contains `--detail` or a specific idea name):
- Read `projects/<idea>/docs/audit-log.md` — latest iteration details
- Read `projects/<idea>/docs/plan.md` — phase progress

---

## Output format

Output this dashboard as markdown. Keep it concise — this is a quick status check, not a deep dive.

```
# Ideas Status — YYYY-MM-DD

## Research Pipeline

| Track | Command | Iterations | Ideas Scored | Ideas Killed | Best Surviving | Score | Threshold |
|-------|---------|:----------:|:------------:|:------------:|----------------|:-----:|:---------:|
| SaaS  | /research-ideas | N | N | N | [name] | X/30 | 22/30 |
| Tools | /research-tool-ideas | N | N | N | [name] | X/25 | 16/25 |

## Implementation Pipeline

| # | Idea | Type | Score | Status | Phase | Iteration | MVP Progress | Next | Blocker |
|---|------|------|:-----:|--------|-------|:---------:|:------------:|------|---------|
| 1 | ... | SaaS/Tool | X/N (Y%) | ... | ... | ... | X/10 | ... | ... |

## Unified Leaderboard (available for /implement backfill)

| Rank | Idea | Type | Raw Score | Normalized | Status |
|------|------|------|:---------:|:----------:|--------|
| 1 | ... | ... | ... | ... | IN_TRACKER / AVAILABLE / KILLED |

## Launch Progress (for LAUNCHING/LAUNCHED/GROWING ideas)

### [Idea Name]
| Date | Action | Status | Notes |
|------|--------|--------|-------|
| ... | ... | ✅/❌/🔄 | ... |

(Include ad campaign configs, pending blockers with unblock steps, and review dates)

## Summary
- **Active builds**: N idea(s) in implementation
- **Available for backfill**: N idea(s) above threshold, not yet started
- **Research exhaustion**: [assessment — e.g., "SaaS track exhausted after 14 iterations, Tool track early with 2 iterations"]
- **Recommendation**: [one line — what should happen next: more research, start building, kill something, etc.]
```

### Status derivation rules:
- **IN_TRACKER**: Idea appears in TRACKER.md (any status except KILLED)
- **AVAILABLE**: Idea is above its threshold AND not in TRACKER → can be picked by `/implement`
- **BELOW_THRESHOLD**: Scored but below threshold (22/30 SaaS, 16/25 Tools)
- **KILLED**: Explicitly killed in leaderboard, TRACKER, or killed-ideas registry
- **BUILDING/POLISHING/LAUNCHING/etc.**: Use exact status from TRACKER.md

### Score normalization (for unified ranking):
- SaaS: `score / 30 * 100` → percentage
- Tools: `score / 25 * 100` → percentage
- Sort by normalized % descending

### Launch progress (always show for LAUNCHING/LAUNCHED/GROWING ideas):
- Read the "Launch Progress Logs" section of TRACKER.md
- Display the launch log table for each active launch idea
- Highlight pending (❌) items and upcoming review dates

### If `--detail [idea-name]` is passed:
Also read and display:
- Latest audit-log entry for that idea
- Current plan.md phase and remaining deliverables
- MVP checklist progress
- Git log (last 3 commits) from `projects/<idea>/`

### If no arguments:
Show the dashboard + launch logs for any LAUNCHING/LAUNCHED/GROWING ideas.

---

## IMPORTANT
- This is READ-ONLY. Do NOT modify any files.
- Keep output under 100 lines for the default view.
- If a file doesn't exist, note "not found" in the relevant section and continue.
- For killed ideas in the leaderboard, only show the top 5 most recently killed (with kill reason) to keep the output manageable. Add a count: "and N more killed".
