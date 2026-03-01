# Eval Metrics, Flags, and Methods — Canonical Definitions

**Purpose:** Clearly define **eval metrics** (names, types, meaning, sources), **CLI flags** (all eval- and genie-related scripts), and **methods** (how each metric is computed). Single source of truth for eval semantics and script options.

**Governance:** [EVAL_LOOP_AND_CHAIN_OF_EVENTS.md](../EVAL_LOOP_AND_CHAIN_OF_EVENTS.md); [evals.md](../evals.md); [COMPREHENSIVE_EVAL_RECOMMENDATIONS_SPEC.md](COMPREHENSIVE_EVAL_RECOMMENDATIONS_SPEC.md).

---

## 1. Eval metrics (defined terms)

### 1.1 Post-run eval metrics (chain-of-events and eval-after-run-latest)

| Metric | Type | Source | Meaning |
|--------|------|--------|---------|
| **ts** | string (ISO 8601) | Script runtime | Timestamp of the eval (UTC). |
| **run_type** | enum | CLI `--run-type` or auto-detect | `omni-audit` \| `comprehensive-eval` \| `full-review`. Which run produced the outputs being evaluated. |
| **outcome** | enum | Derived from Full Review log | `pass` — all verifications passed; `warn` — one or more verifications failed (advisory; script still exits 0). |
| **verify_summary** | string | `scripts/.full-review-last.log` | Last line matching `Summary: N/M passed` (e.g. `"Summary: 43/104 passed"`). N = passed checks, M = total; some checks are optional (e.g. connections). |
| **merge** | integer | `docs/audits/comprehensive-eval-and-cleanup-recommendations.md` | Count of **data rows** in the ## MERGE section (repo/1P merge recommendations). Excludes table header and separator. |
| **archive** | integer | Same doc, ## ARCHIVE | Count of data rows (vault moves; archived repos). |
| **delete** | integer | Same doc, ## DELETE | Count of data rows (1P dedup extras; duplicate repos). |
| **fix** | integer | Same doc, ## FIX | Count of data rows (missing env/secrets; connection fixes). |

**Optional / future metrics (not yet in chain):**

| Metric | Type | Source | Meaning |
|--------|------|--------|---------|
| **schema_pass** | boolean | `validate_schemas.sh` | Whether bundle/schemas validation passed. |
| **regression_delta** | number | `run_eval.sh` vs `data/synthetic/gold/` | Delta vs golden set when regression is run. |

### 1.2 Eval layers (evals.md — schema, fact, logic, ethics, regression)

| Layer | What is evaluated | Gate / script |
|-------|-------------------|---------------|
| **Schema** | JSON outputs vs `docs/schemas/` | `validate_schemas.sh` |
| **Fact / citation** | Facts have source + location; citations resolve | Evaluator swarm |
| **Logic** | Claim elements and narrative consistency | Evaluator swarm |
| **Ethics** | No harmful/biased outputs; escalation path | Evaluator swarm |
| **Regression** | Same inputs → acceptable delta vs `data/synthetic/gold/` | `run_eval.sh` |

### 1.3 Thresholds and interpretation (advisory)

- **outcome = pass:** Full Review log contains "All verifications passed." No mandatory threshold on merge/archive/delete/fix counts; they are informational.
- **outcome = warn:** One or more verifications failed; or `verify_summary` shows passed &lt; total. Review `scripts/.full-review-last.log` and `docs/audits/comprehensive-eval-and-cleanup-recommendations.md`.
- **fix &gt; 0:** Indicates connection/env issues; address per FIX section before relying on MCPs/APIs.
- **merge / archive / delete &gt; 0:** Recommendations only; no destructive execution without explicit approval and dry-run first.

---

## 2. Flags (CLI options)

### 2.1 Post-run eval loop — `run-post-run-eval-loop.sh`

| Flag | Values | Default | Effect |
|------|--------|--------|--------|
| `--run-type` | `omni-audit` \| `comprehensive-eval` \| `full-review` | Auto-detect | Tags the chain-of-events entry. Auto-detect: comprehensive-eval if recommendations + full-review-summary exist; else full-review. |

### 2.2 Comprehensive eval — `run-comprehensive-eval-and-cleanup.sh`

| Flag | Default | Effect |
|------|--------|--------|
| `--skip-full-review` | (none) | Skip Full Review step; re-aggregate from existing Full Review log and 1P/connections outputs. |
| `--include-transcripts` | (none) | Emit transcript chunking plan (paths + guidance). |

### 2.3 Every turn (genie run) — `run-every-turn.sh`

| Flag | Default | Effect |
|------|--------|--------|
| `--skip-codify` | (none) | Skip codify step; run Go flow + Comprehensive Review only. |
| `--execute-codify` | dry-run | Run codify **and execute** the generated genie script (default: dry-run). |

### 2.4 Codify (Genie Magic) — `codify-recommendations-to-scripts.sh`

| Flag | Default | Effect |
|------|--------|--------|
| `--dry-run` | **dry-run** | Generate genie script and run it in dry-run mode (echo only). |
| `--execute` | (none) | Generate and **execute** the genie script. |
| `--no-pre-check` | (none) | Skip pre-flight verifications before codify. |
| `--no-post-eval` | (none) | Skip post-run verifications and eval harness after executing genie script. |
| `--strict` | (none) | Pre-flight and post-run failures cause script to exit 1; include schema and taxonomy validation in pre-flight when set. |

### 2.5 Eval harness — `run_eval.sh`

| Flag | Default | Effect |
|------|--------|--------|
| `--regression` | (none) | Run regression comparison vs `data/synthetic/gold/` when gold labels exist. |

### 2.6 Omni audit — `run-omni-audit-and-never-miss.sh`

| Flag | Default | Effect |
|------|--------|--------|
| `--connections-optional` | (none) | Run connect-and-configure with connection verification in advisory mode. |

---

## 3. Methods (how metrics are computed)

### 3.1 verify_summary

- **Source file:** `scripts/.full-review-last.log`
- **Method:** `grep -E "Summary: [0-9]+/[0-9]+" .full-review-last.log | tail -1`
- **Output:** Raw string, e.g. `"Summary: 43/104 passed"`. Stored as-is in chain and eval-after-run-latest.

### 3.2 outcome

- **Source:** Same log as above.
- **Method:**  
  - If log contains literal "All verifications passed" → **pass**.  
  - Else if `verify_summary` was parsed and (total − passed) &gt; 0 → **warn**.  
  - Default → **pass** (eval is non-blocking).

### 3.3 merge, archive, delete, fix (recommendation counts)

- **Source file:** `docs/audits/comprehensive-eval-and-cleanup-recommendations.md`
- **Method:** For each section `## MERGE`, `## ARCHIVE`, `## DELETE`, `## FIX`, count lines that:
  - Lie between that section header and the next `## ` section,
  - Start with `|`,
  - Do **not** match the table separator `|---`,
  - Do **not** match the header row pattern `| Item |` (so only data rows are counted).
- **Implementation:** AWK one-liner per section (see `run-post-run-eval-loop.sh`).

### 3.4 run_type (auto-detect)

- **Method:** If `comprehensive-eval-and-cleanup-recommendations.md` and `full-review-summary.md` both exist → `comprehensive-eval`; else `full-review`. Overridden by `--run-type` when provided.

---

## 4. Chain-of-events JSONL schema (one line per run)

Each line is a single JSON object with no trailing comma. Example:

```json
{"ts":"2026-02-28T20:36:09Z","run_type":"comprehensive-eval","outcome":"pass","verify_summary":"Summary: 43/104 passed","merge":2,"archive":2,"delete":2,"fix":17}
```

| Field | Type | Required |
|-------|------|----------|
| ts | string | yes |
| run_type | string | yes |
| outcome | string | yes |
| verify_summary | string | yes (may be empty) |
| merge | number | yes |
| archive | number | yes |
| delete | number | yes |
| fix | number | yes |

---

## 5. References

| Doc | Purpose |
|-----|--------|
| [EVAL_LOOP_AND_CHAIN_OF_EVENTS.md](../EVAL_LOOP_AND_CHAIN_OF_EVENTS.md) | Eval loop, chain of events, wiring, best practices (genie) |
| [evals.md](../evals.md) | Evaluation layers, schema/regression, run_eval.sh |
| [COMPREHENSIVE_EVAL_RECOMMENDATIONS_SPEC.md](COMPREHENSIVE_EVAL_RECOMMENDATIONS_SPEC.md) | MERGE/ARCHIVE/DELETE/FIX spec and aggregation |

_Maintain at: docs/audits/EVAL_METRICS_FLAGS_AND_METHODS.md. Update when adding metrics, flags, or methods._
