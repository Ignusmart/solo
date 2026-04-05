You are auditing the Solo workspace for consistency, staleness, and errors. This command checks that all tracking files, docs, and commands are in sync and flags anything broken.

## Arguments
- `$ARGUMENTS` — parse for `--fix` (auto-fix safe issues), `--deep` (also audit project folders), or both. Default: report only.

---

## AUDIT CHANGELOG — LOOP MEMORY

This command is designed for `/loop`. You have NO memory of previous runs. The changelog IS your memory.

### Changelog file: `research/implementation/audit-changelog.md`

**Execution order (critical for unbiased auditing):**
1. **Run ALL checks FIRST** — produce the full findings list (errors, warnings, passes) WITHOUT reading the changelog. This prevents bias: you must discover issues fresh each time, not skip checks because they "passed last time."
2. **THEN read the changelog** — compare your fresh findings against previous entries.
3. **Classify each finding:**
   - **NEW**: not in any previous changelog entry → report prominently
   - **RECURRING**: same issue appeared in a previous entry and was NOT fixed → flag as recurring with count (e.g., "recurring x3 — first seen 2026-04-05")
   - **REGRESSED**: issue was marked FIXED in a previous entry but is back → flag as regression
   - **FIXED**: issue from a previous entry is no longer found → note as resolved
4. **Append a new entry** to the changelog (even in report-only mode — the changelog tracks findings, not just fixes).

### Changelog format:
```markdown
## Audit #N — YYYY-MM-DD HH:MM

### Findings
| # | Severity | Check | Finding | Status | First Seen |
|---|----------|-------|---------|--------|------------|
| 1 | ERROR | README freshness | DriftWatch listed as "Not started" but TRACKER shows BUILDING | NEW | 2026-04-05 |
| 2 | WARN | Unified leaderboard | File does not exist yet | RECURRING x2 | 2026-04-05 |
| 3 | ERROR | TRACKER consistency | Freight TMS still listed as active in README | FIXED | 2026-04-05 |

### Actions taken
- [if --fix] Fixed README DriftWatch status
- [if report-only] No fixes applied (report-only mode)

### Stats
- Checks: 9 | Errors: 1 | Warnings: 2 | Passed: 6
- New issues: 1 | Recurring: 1 | Regressions: 0 | Fixed since last: 1
```

### Changelog rules:
- **Create the file** if it doesn't exist (first audit run)
- **Append only** — never edit or delete previous entries
- **Keep entries compact** — table format, no prose. The iteration reports have the details.
- **Number audits sequentially** — count existing `## Audit #N` headers to determine next N
- **Include timestamp** (not just date) so multiple audits per day are distinguishable
- **Track "first seen" dates** — when an issue first appeared. Carry forward from previous entries.

### Staleness escalation:
If an issue is RECURRING for 3+ audits:
- Escalate severity: WARN → ERROR
- Add a note: `[STALE x3] This issue has persisted across 3 audits. Needs manual intervention.`

---

## CHECKS TO RUN (in order)

### 1. Command inventory
- Glob `.claude/commands/*.md` — list all commands
- Check that CLAUDE.md and README.md both list ALL commands
- **Flag**: any command missing from CLAUDE.md or README.md

### 2. README.md freshness
- Read README.md
- Read `research/implementation/TRACKER.md` for current idea statuses
- **Flag**: README says an idea is "Not started" or "Planned" but TRACKER shows BUILDING/KILLED/etc.
- **Flag**: README lists projects that don't exist in TRACKER or have been killed
- **Flag**: Commands table doesn't match actual `.claude/commands/` contents
- **Flag**: "Current Priority" section contradicts TRACKER status

### 3. CLAUDE.md freshness
- Read CLAUDE.md
- Compare against actual state:
  - Iteration counts: count `research/reports/*-market-gap-iteration-*.md` and `*-tool-ideas-iteration-*.md`
  - Command list: compare against `.claude/commands/*.md`
  - Revenue strategy: check if it references killed ideas
  - Repo structure tree: check if it lists files/dirs that exist or omits ones that should be listed
- **Flag**: any discrepancy

### 4. TRACKER.md consistency
- Read TRACKER.md
- For each idea listed:
  - Check if `projects/<folder>/` exists (run `ls`)
  - Check if `projects/<folder>/docs/audit-log.md` exists
  - Check if `projects/<folder>/docs/plan.md` exists
  - If status is BUILDING/POLISHING: verify audit-log exists and last iteration matches TRACKER's "Last Iteration"
  - If status is KILLED: verify it's NOT still listed as active or planned in README
- **Flag**: folder missing, audit-log missing for active idea, iteration mismatch, killed idea still advertised

### 5. Leaderboard consistency
- Read SaaS leaderboard (`research/reports/2026-04-04-idea-leaderboard.md`)
- Read Tool leaderboard (`research/reports/tool-ideas-leaderboard.md`)
- Check: does `research/implementation/unified-leaderboard.md` exist? If not, flag it.
- If unified leaderboard exists: verify it includes all non-killed ideas above threshold from both sources
- **Flag**: scoring system mismatch (e.g., header says /30 but table uses /25 columns), missing ideas, stale unified leaderboard

### 6. Strategy docs check
- Glob `research/strategy/*.md`
- Verify the numbered series is complete (00-07 expected)
- Check that 06-KILLED-IDEAS.md and 07-KILLED-TOOL-IDEAS.md exist
- **Flag**: missing strategy docs, gaps in numbering

### 7. Cross-reference killed ideas
- For each idea in TRACKER.md with status KILLED:
  - Grep `research/strategy/06-KILLED-IDEAS.md` for the idea name
  - Grep `research/strategy/07-KILLED-TOOL-IDEAS.md` for the idea name
  - **Flag**: killed in TRACKER but not recorded in killed-ideas registry

### 8. `/implement` command internal consistency (only with `--deep`)
- Read `.claude/commands/implement.md`
- **Flag**: step numbering out of order
- **Flag**: duplicate section labels
- **Flag**: references to files that don't exist
- **Flag**: tech stack or scoring thresholds that contradict research commands
- **Flag**: prompt length (warn if >500 lines — context pressure risk)

### 9. Project folder health (only with `--deep`)
- For each active (non-KILLED) idea in TRACKER:
  - Check `projects/<name>/.git` exists
  - Check `projects/<name>/CLAUDE.md` exists
  - Check `projects/<name>/README.md` exists
  - Check `projects/<name>/.env.example` exists (if past PLANNING phase)
  - Check `projects/<name>/docs/audit-log.md` — verify iteration count matches TRACKER
  - Run `git -C projects/<name>/ status` — check for uncommitted changes
  - **Flag**: missing git, missing docs, uncommitted work, iteration drift

---

## OUTPUT FORMAT

```
# Auto-Audit #N — YYYY-MM-DD HH:MM

## Summary
- Checks run: N | Passed: N | Warnings: N | Errors: N
- vs last audit: N new | N recurring | N regressions | N fixed

## Errors (must fix)
1. [ERROR] [check name] — [description] [NEW/RECURRING xN/REGRESSED]
   - Expected: ...
   - Actual: ...
   - Fix: [what to do]
   - First seen: YYYY-MM-DD

## Warnings (should fix)
1. [WARN] [check name] — [description] [NEW/RECURRING xN]
   - Fix: [what to do]
   - First seen: YYYY-MM-DD

## Fixed since last audit
- [✓] [description] — was [ERROR/WARN], first seen YYYY-MM-DD, fixed after N audits

## Passed
- [✓] Command inventory: N commands found, all listed
- [✓] README freshness: all statuses match TRACKER
- ...
```

### Severity rules:
- **ERROR**: Data contradicts reality (README says active, TRACKER says killed). Misleads future conversations.
- **WARN**: Something is missing or stale but doesn't cause wrong behavior (e.g., unified leaderboard not yet created).
- **PASS**: Check passes, state is consistent.
- **Escalation**: WARN issues recurring 3+ times auto-escalate to ERROR.

---

## IF `--fix` IS PASSED

After reporting, auto-fix SAFE issues only:
- Update README.md: sync project statuses from TRACKER, sync commands table from `.claude/commands/`, update "Current Priority" section
- Update CLAUDE.md: sync iteration counts, sync commands list, update revenue strategy to remove killed ideas, update repo structure tree
- Create `research/implementation/unified-leaderboard.md` if missing (build from both source leaderboards)
- Add missing killed ideas to killed-ideas registries
- **Do NOT auto-fix**: project folder issues, scoring mismatches, `/implement` structural issues (these need human judgment)

After fixing, re-run checks 1-7 to confirm fixes resolved the issues. Record results in the changelog entry under "Actions taken" with pass/fail for each fix.

---

## IMPORTANT
- This command is designed to be run periodically (e.g., `/loop 1h /auto-audit`) or before any `/implement` run.
- **Always append to the changelog** — even in report-only mode. The changelog tracks what was found, not just what was fixed.
- Keep output concise — errors and warnings only in the default view. `--deep` adds the project-level checks.
- If everything passes, say so in one line: "All N checks passed. System is consistent. No new issues since audit #N-1."
- **Do NOT read the changelog before running checks.** Findings must be unbiased. Compare only after.
