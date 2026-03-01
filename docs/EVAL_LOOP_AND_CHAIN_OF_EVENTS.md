# Eval Loop and Chain of Events — Eval After Each Run

**Purpose:** Define the **eval loop** (evaluate after each run) and the **chain of events** (ordered log of run → eval → outcome) so every omni-audit, comprehensive-eval, or full-review is followed by a consistent evaluation and persisted event.

**Governance:** Constitution §3 (explainability & audit); [evals.md](evals.md); [COMPREHENSIVE_EVAL_RECOMMENDATIONS_SPEC.md](audits/COMPREHENSIVE_EVAL_RECOMMENDATIONS_SPEC.md).

**Eval metrics, flags, and methods:** For canonical definitions of every metric (verify_summary, outcome, merge, archive, delete, fix), all CLI flags (post-run eval, comprehensive eval, every-turn, codify, run_eval, omni-audit), and the exact methods used to compute each metric, see **[docs/audits/EVAL_METRICS_FLAGS_AND_METHODS.md](audits/EVAL_METRICS_FLAGS_AND_METHODS.md)**.

---

## 1. Eval loop (eval after each run)

After **each** of these runs, the **post-run eval** runs automatically:

| Run | Script | Eval runs after |
|-----|--------|------------------|
| **Omni audit** | `./scripts/run-omni-audit-and-never-miss.sh` | Connect-and-configure + comprehensive eval; then `run-post-run-eval-loop.sh` |
| **Comprehensive eval** | `./scripts/run-comprehensive-eval-and-cleanup.sh` | Full Review + 1P + connections + aggregate; then `run-post-run-eval-loop.sh` |
| **Full Review only** | `./scripts/run-full-review.sh` | Verifications + summary; then (optional) `run-post-run-eval-loop.sh --run-type full-review` |

**Post-run eval script:** `./scripts/run-post-run-eval-loop.sh`  
- **Inputs:** Last run outputs (`.full-review-last.log`, `full-review-summary.md`, `comprehensive-eval-and-cleanup-recommendations.md`).  
- **Actions:** Extract metrics (verify pass/fail summary, MERGE/ARCHIVE/DELETE/FIX counts), set outcome (pass/warn), append one JSON line to chain-of-events, write `eval-after-run-latest.json` and `eval-after-run-latest.md`.  
- **Optional:** `--run-type omni-audit|comprehensive-eval|full-review` to tag the event; otherwise auto-detected.

**After each review — commands and architecture:** After Full Review (Phase 3) and after Comprehensive Eval (step 6), the system runs `./scripts/run-commands-and-architecture-review.sh`. This ensures (1) **all new commands are organized in place** (every script in `scripts/` is in [COMMANDS_AND_SCRIPTS_INDEX.md](COMMANDS_AND_SCRIPTS_INDEX.md)); (2) **architecture** is **updated and/or reviewed** (in whole or in part) based on computer-science-based rules, repos, and best practices relevant to any change. See [PRODUCT_THAT_BUILDS_THE_PRODUCT_AND_ARCHITECTURE_TENET.md](PRODUCT_THAT_BUILDS_THE_PRODUCT_AND_ARCHITECTURE_TENET.md). Output: `docs/audits/commands-and-architecture-review-latest.md`.

---

## 2. Chain of events (ordered log)

The **chain of events** is an ordered log of every run and its eval outcome. One **event** = one run + one eval result.

| Artifact | Location | Format |
|----------|----------|--------|
| **Chain log** | `docs/audits/chain-of-events.jsonl` | One JSON object per line: `{"ts":"...","run_type":"...","outcome":"pass|warn|fail","verify_summary":"...","merge":N,"archive":N,"delete":N,"fix":N}` |
| **Latest eval (JSON)** | `docs/audits/eval-after-run-latest.json` | Single JSON object for the most recent run. |
| **Latest eval (summary)** | `docs/audits/eval-after-run-latest.md` | Short markdown summary (timestamp, run_type, outcome, metrics table). |

**Event sequence:**  
`[Run]` → `[Eval after run]` → `[Persist to chain-of-events.jsonl]` → `[Write eval-after-run-latest.*]` → optional report or next trigger.

---

## 3. Metrics captured per run

| Metric | Type | Source | Meaning |
|--------|------|--------|---------|
| **ts** | string (ISO 8601) | Script runtime | Eval timestamp (UTC). |
| **run_type** | enum | `--run-type` or auto-detect | `omni-audit` \| `comprehensive-eval` \| `full-review`. |
| **outcome** | enum | Derived from Full Review log | `pass` — all verifications passed; `warn` — one or more failed (advisory; script exits 0). |
| **verify_summary** | string | `scripts/.full-review-last.log` | Last "Summary: N/M passed" line (e.g. 43/104). |
| **merge** | integer | Data rows in ## MERGE (recommendations doc) | Repo/1P merge recommendations count. |
| **archive** | integer | Data rows in ## ARCHIVE | Vault moves; archived repos count. |
| **delete** | integer | Data rows in ## DELETE | 1P dedup extras; duplicate repos count. |
| **fix** | integer | Data rows in ## FIX | Missing env/secrets; connection fixes count. |

**Full definitions, thresholds, and computation methods:** [audits/EVAL_METRICS_FLAGS_AND_METHODS.md](audits/EVAL_METRICS_FLAGS_AND_METHODS.md).

---

## 4. Wiring (where eval is invoked)

| Script | Invocation |
|--------|------------|
| `run-comprehensive-eval-and-cleanup.sh` | At end: `"$SCRIPT_DIR/run-post-run-eval-loop.sh" --run-type comprehensive-eval` |
| `run-omni-audit-and-never-miss.sh` | At end: `"$SCRIPT_DIR/run-post-run-eval-loop.sh" --run-type omni-audit` |
| `run-full-review.sh` | Optional: call `run-post-run-eval-loop.sh --run-type full-review` from a wrapper or after manual run. |

Eval is **non-blocking**: it always exits 0 so it does not fail the main run.

---

## 5. Using the chain for reporting and triggers

- **History:** `tail -n 20 docs/audits/chain-of-events.jsonl` for the last 20 runs.  
- **Latest outcome:** `docs/audits/eval-after-run-latest.md` or `eval-after-run-latest.json`.  
- **Automation:** A cron or CI job can run omni-audit or comprehensive-eval, then read `eval-after-run-latest.json` to trigger alerts (e.g. outcome=warn, fix>10) or post to Slack.  
- **Regression:** Compare `outcome` and metrics across events (e.g. fix count increasing) to spot drift.

---

## 6. Best practices: running genie

**Genie run** = full “every turn” flow: Go flow → codify recommendations into Genie-like scripts → no-fail Comprehensive Review. Interchangeable with “comprehensive review” (Constitution §6.5). Below are the recommended practices.

### 6.1 When to run genie

| Trigger | Action |
|---------|--------|
| **After a cycle of work** | Run → then Go run or Genie run so route/sync/Full Review and recommendations are current. |
| **Before commit (governance/connector scope)** | Run Full Review or Genie run so checklist and MERGE/ARCHIVE/DELETE/FIX are up to date. |
| **Quarterly** | Run omni-audit and/or Genie run; complete mandatory checklist and apply recommendations per policy. |
| **After adding repos/MCPs/connectors** | Run connect-and-configure and Full Review; then comprehensive eval so recommendations and post-run eval reflect new state. |

### 6.2 Sequence (genie run)

1. **Go flow** — `run-go-flow.sh`: route constitution → sync all repos → Full Review (writes full-review-summary.md and .full-review-last.log).
2. **Codify** — `codify-recommendations-to-scripts.sh`: read comprehensive-eval-and-cleanup-recommendations.md → generate genie-from-recommendations-YYYYMMDD-HHMM.sh → run it (dry-run by default).
3. **Comprehensive Review** — `run-comprehensive-eval-and-cleanup.sh`: Full Review (or skip with --skip-full-review) + 1Password review + connections verify + aggregate MERGE/ARCHIVE/DELETE/FIX → then **post-run eval** (chain-of-events + eval-after-run-latest).

Single command: `./scripts/run-every-turn.sh` (optionally `--skip-codify` or `--execute-codify`).

### 6.3 Pre-flight and post-run (Genie Magic)

| Phase | Best practice |
|-------|----------------|
| **Pre-flight** | Run before codify: `run-all-verifications.sh --quick`. With `--strict`: also run validate_schemas.sh and validate-taxonomy.sh; fail script on any failure. |
| **Codify** | Default **dry-run**: generate and run genie script in echo-only mode. Use `--execute` only after reviewing the generated script and approving destructive steps. |
| **Post-run** | After executing genie script: re-run quick verifications and `run_eval.sh` (schema/regression). Use `--no-post-eval` only when intentionally skipping. |
| **Destructive actions** | 1Password execute, delete repos, etc.: genie script runs them with dry-run first; execute only via explicit `--execute` and human approval. |

### 6.4 Flags (quick reference)

| Script | Key flags |
|--------|-----------|
| `run-every-turn.sh` | `--skip-codify`, `--execute-codify` |
| `codify-recommendations-to-scripts.sh` | `--dry-run`, `--execute`, `--no-pre-check`, `--no-post-eval`, `--strict` |
| `run-comprehensive-eval-and-cleanup.sh` | `--skip-full-review`, `--include-transcripts` |
| `run-post-run-eval-loop.sh` | `--run-type omni-audit \| comprehensive-eval \| full-review` |

Full flag semantics: [audits/EVAL_METRICS_FLAGS_AND_METHODS.md](audits/EVAL_METRICS_FLAGS_AND_METHODS.md) §2.

### 6.5 Charts and graphs (Constitution §6.5)

Every genie run / comprehensive review must produce:

- **Technical summary** — full-review-summary.md (waterfall, verification result, mandatory checklist).
- **Recommendations** — comprehensive-eval-and-cleanup-recommendations.md (MERGE/ARCHIVE/DELETE/FIX).
- **Eval result** — eval-after-run-latest.md and chain-of-events.jsonl (metrics, outcome).
- **Normal-person summary** — full-review-summary.md “Average-person summary” and, when produced, any Genie Magic checksum/pre-post check summary.

### 6.6 No destructive execution without approval

- Apply MERGE/ARCHIVE/DELETE/FIX per policy; do not execute destructive actions without approval.
- Dry-run first; then execute only with explicit flags and after reviewing the generated genie script and 1password-approved.json (or equivalent).

---

## 7. References

| Doc | Purpose |
|-----|--------|
| [audits/EVAL_METRICS_FLAGS_AND_METHODS.md](audits/EVAL_METRICS_FLAGS_AND_METHODS.md) | **Canonical** metrics, flags, methods |
| [evals.md](evals.md) | Schema/regression eval harness; run_eval.sh |
| [audits/COMPREHENSIVE_EVAL_RECOMMENDATIONS_SPEC.md](audits/COMPREHENSIVE_EVAL_RECOMMENDATIONS_SPEC.md) | Comprehensive eval spec |
| [audits/full-review-summary.md](audits/full-review-summary.md) | Full Review output (mandatory checklist) |
| [audits/comprehensive-eval-and-cleanup-recommendations.md](audits/comprehensive-eval-and-cleanup-recommendations.md) | MERGE/ARCHIVE/DELETE/FIX artifact |
| [COMPONENT_BREAKDOWN_SYNC_AND_RUN.md](COMPONENT_BREAKDOWN_SYNC_AND_RUN.md) | Run → Go run → Genie run sequence |

_Maintain at: docs/EVAL_LOOP_AND_CHAIN_OF_EVENTS.md. Update when adding metrics, wiring new runs, or changing genie best practices._
