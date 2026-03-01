# Game Changer — Review & Audit (Expanded)

**Purpose:** Single **Game Changer** document that provides **all specs, rules, processes, and features** for our **audit of same** — the expanded definition of **Review** and everything that runs in or after a review. This is the canonical spec for the product-that-builds-the-product’s **review and audit** capability: what “Review” means, what runs, what is produced, and how it aligns to architecture, industry terms, and enterprise best practices.

**Governance:** Constitution §6.5 (outcome, derivative outcomes, chart/graph); [GAME_CHANGERS.md](GAME_CHANGERS.md); [REVIEW_RESPONSE_AND_TOP_SOURCES.md](REVIEW_RESPONSE_AND_TOP_SOURCES.md); [PRODUCT_THAT_BUILDS_THE_PRODUCT_AND_ARCHITECTURE_TENET.md](PRODUCT_THAT_BUILDS_THE_PRODUCT_AND_ARCHITECTURE_TENET.md); [EVAL_LOOP_AND_CHAIN_OF_EVENTS.md](EVAL_LOOP_AND_CHAIN_OF_EVENTS.md).

---

## 1. Defined term: “Review” (expanded)

**In this repo, “Review” or “review” (upper or lower case) means the full set of review types and the additional turn below, together.** One command runs the full set: `./scripts/run-review.sh` (which invokes `run-every-turn.sh`). Every review run includes the **additional turn**: **commands-and-architecture review** (organize in place; architecture updated/reviewed per CS rules, repos, best practices).

### 1.1 Review types (all together = “Review”)

| Type | Script / entry | What it does |
|------|----------------|--------------|
| **Go flow** | `run-go-flow.sh` | Route constitution → sync all repos → Full Review (Phase 1–3). |
| **Full Review** | `run-full-review.sh` | Phase 1: run-all-verifications (--routing --connections --connections-optional). Phase 2: write full-review-summary.md. **Phase 3:** run-commands-and-architecture-review.sh (commands organized in place; architecture per CS/repos/best practices). |
| **Genie loop** | `codify-recommendations-to-scripts.sh` | Turn recommendations into genie-from-recommendations-*.sh; dry-run or --execute. |
| **Comprehensive (eval)** | `run-comprehensive-eval-and-cleanup.sh` | Full Review (or --skip-full-review) + 1Password review + connections verify + aggregate MERGE/ARCHIVE/DELETE/FIX. Step 5: post-run eval. **Step 6:** commands-and-architecture review. |
| **Post-run eval** | `run-post-run-eval-loop.sh` | Extract metrics; append to chain-of-events.jsonl; write eval-after-run-latest.json and .md. |
| **Omni audit** | `run-omni-audit-and-never-miss.sh` | Connect-and-configure + comprehensive eval + post-run eval. |
| **Quick Review** | `run-quick-review.sh` | Scope/effects per change; emulation check; use when applicable. |

### 1.2 Additional turn (every review)

After each **Full Review** (Phase 3) and after each **Comprehensive Eval** (step 6):

- **Commands-and-architecture review** — `./scripts/run-commands-and-architecture-review.sh`
  - Ensures **all new commands are organized in place** (every script in `scripts/` is in [COMMANDS_AND_SCRIPTS_INDEX.md](COMMANDS_AND_SCRIPTS_INDEX.md)).
  - Ensures **architecture** is **updated and/or reviewed** (in whole or in part) based on **computer-science-based rules**, **repos**, and **best practices** relevant to any change.
  - Output: `docs/audits/commands-and-architecture-review-latest.md`.
  - Tenet: [PRODUCT_THAT_BUILDS_THE_PRODUCT_AND_ARCHITECTURE_TENET.md](PRODUCT_THAT_BUILDS_THE_PRODUCT_AND_ARCHITECTURE_TENET.md).

---

## 2. Specs (what every Review must satisfy)

### 2.1 Review response command (mandatory output)

Every Review output **must** include (see [REVIEW_RESPONSE_AND_TOP_SOURCES.md](REVIEW_RESPONSE_AND_TOP_SOURCES.md)):

| Element | Required | Where it appears |
|--------|----------|-------------------|
| **Reference to top repos** | Yes | SOURCES_AND_EMULATION_INDEX, BEST_PRACTICES_FROM_TOP_REPOS, REFERENCE_PATTERNS_AND_EXAMPLE_REPOS; or “Top repos & whitepapers (this run)” in full-review-summary.md. |
| **Reference to whitepapers / standards** | Yes | ABA/EDRM/Sedona, Production-Grade Agentic AI, 12-Factor Agents, MCP Best Practice, OWASP LLM, ISO/IEC 42001. |
| **Real-world context** | Yes | One sentence: what this run means in practice. |
| **Average-person summary** | Yes | Plain-language summary in full-review-summary.md and comprehensive-eval artifacts. |
| **Technical summary** | Yes | full-review-summary.md “Technical summary”; verification result; MERGE/ARCHIVE/DELETE/FIX counts; eval-after-run metrics. |
| **Visual summary** | Yes | Charts, graphs, tables: Architecture graphs/charts, waterfall, verification result, recommendations tables, docs/audits/artifacts/README.md. |

### 2.2 Mandatory checklist (Full Review not complete until all done)

Per full-review-summary.md, the mandatory completion checklist includes:

- Derivative effects documented; emulation sources present; Comprehensive Update run; refined instructions (AGENTS.md, CLAUDE.md, my-agent.agent.md, etc.); architecture review and efficiency review; iron curtain (updates automated); optional quality gate (three pillars); agent menu and harnesses; **omni inventory and dedupe** (run-omni-audit-and-never-miss when scope includes life/data domains).

### 2.3 Eval metrics (post-run)

| Metric | Type | Meaning |
|--------|------|---------|
| **ts** | ISO 8601 | Eval timestamp (UTC). |
| **run_type** | omni-audit \| comprehensive-eval \| full-review | Which run produced the outputs. |
| **outcome** | pass \| warn | pass = all verifications passed; warn = one or more failed (advisory). |
| **verify_summary** | string | e.g. "Summary: N/M passed". |
| **merge, archive, delete, fix** | integer | Data-row counts in comprehensive-eval-and-cleanup-recommendations.md (## MERGE, ## ARCHIVE, ## DELETE, ## FIX). |

Full definitions and methods: [audits/EVAL_METRICS_FLAGS_AND_METHODS.md](audits/EVAL_METRICS_FLAGS_AND_METHODS.md).

### 2.4 Chain of events (ordered log)

- **Artifact:** `docs/audits/chain-of-events.jsonl` — one JSON object per run (ts, run_type, outcome, verify_summary, merge, archive, delete, fix).
- **Latest:** `docs/audits/eval-after-run-latest.json`, `eval-after-run-latest.md`.

---

## 3. Rules (governing every Review)

| Rule | What it means |
|------|----------------|
| **Never skip a target** | Route and sync reach every ROUTE and every repo in all_repos; no target omitted. NEVER_MISS_INSTRUCTIONS. |
| **No-fail Comprehensive Review** | After every turn (Go → codify), run-comprehensive-eval-and-cleanup.sh must complete or be explicitly deferred with a documented reason. |
| **Human checkpoint** | Privilege, productions, filings, damages conclusions, compliance determinations require human sign-off. Constitution §1. |
| **No destructive execution without approval** | 1Password execute, delete repos, etc.: dry-run first; --execute only with explicit approval. Genie script defaults to dry-run. |
| **Single source of truth** | Master repo = GitHub; canonical lists (repos, MCPs, dev tools, scripts); add to canonical only, then sync. |
| **Commands organized in place** | Every script in scripts/ is in COMMANDS_AND_SCRIPTS_INDEX; new scripts added there and to NEVER_MISS or ONEWISH_OMNI as applicable. |
| **Architecture reviewed per change** | After each review, architecture docs are confirmed or updated (in whole or in part) per CS rules, repos, best practices. PRODUCT_THAT_BUILDS_THE_PRODUCT_AND_ARCHITECTURE_TENET. |
| **Eval non-blocking** | Post-run eval and commands-and-architecture review exit 0 so they do not fail the main run; findings are reported. |

---

## 4. Processes (exact sequences)

### 4.1 Go flow

1. Route constitution — `route-constitution-to-repos.sh` — constitution, checklist, universal, bootstrap → all 4 ROUTES.
2. Sync all repos — `sync-all-repos-and-review.sh` — §6a docs, modules, config → all_repos.
3. Full Review — `run-full-review.sh` — Phase 1 (verifications), Phase 2 (summary), **Phase 3 (commands-and-architecture review)**.

**Script:** `./scripts/run-go-flow.sh`.

### 4.2 Full Review (three phases)

1. **Phase 1:** run-all-verifications.sh --routing --connections --connections-optional → log to .full-review-last.log.
2. **Phase 2:** Write full-review-summary.md (technical summary, average-person summary, top repos & whitepapers, architecture graphs, waterfall, mandatory checklist, evaluation pillars, log tail).
3. **Phase 3:** run-commands-and-architecture-review.sh → commands-and-architecture-review-latest.md.

**Script:** `./scripts/run-full-review.sh`.

### 4.3 Comprehensive Eval (six steps)

1. Full Review (or --skip-full-review).
2. 1Password review → 1password-recommendations.json.
3. Connections verify → connections-report.json.
4. Aggregate recommendations → comprehensive-eval-and-cleanup-recommendations.md (MERGE, ARCHIVE, DELETE, FIX).
5. Post-run eval → chain-of-events.jsonl, eval-after-run-latest.*.
6. **Commands-and-architecture review** → commands-and-architecture-review-latest.md.

**Script:** `./scripts/run-comprehensive-eval-and-cleanup.sh`.

### 4.4 Every turn (Genie run)

1. Go flow — run-go-flow.sh.
2. Codify — codify-recommendations-to-scripts.sh (dry-run or --execute-codify).
3. No-fail Comprehensive Review — run-comprehensive-eval-and-cleanup.sh.

**Script:** `./scripts/run-every-turn.sh`. **Single entry for full Review:** `./scripts/run-review.sh` (invokes run-every-turn.sh).

### 4.5 Omni audit

1. Connect-and-configure — route, sync, workspace, optional verify, Full Review.
2. Comprehensive eval — run-comprehensive-eval-and-cleanup.sh --skip-full-review.
3. Post-run eval — run-post-run-eval-loop.sh --run-type omni-audit.

**Script:** `./scripts/run-omni-audit-and-never-miss.sh`.

---

## 5. Features (expanded)

| Feature | Description | Doc / artifact |
|---------|-------------|----------------|
| **Eval loop** | Eval after each run; metrics extracted; chain-of-events appended; eval-after-run-latest written. | EVAL_LOOP_AND_CHAIN_OF_EVENTS.md; run-post-run-eval-loop.sh |
| **Commands-and-architecture review** | After each Full Review and Comprehensive Eval; commands organized in place; architecture reviewed per CS/repos/best practices. | PRODUCT_THAT_BUILDS_THE_PRODUCT_AND_ARCHITECTURE_TENET.md; run-commands-and-architecture-review.sh; commands-and-architecture-review-latest.md |
| **Industry terms mapping** | Review (and its parts) mapped to industry terms (quality gate, audit, stage gate, etc.) by specialization, core, game changers, principles, DevOps. | REVIEW_INDUSTRY_TERMS_BY_SPECIALIZATION_AND_DEVOPS.md |
| **Enterprise IAM/secrets alignment** | Okta, JumpCloud, Vault, Teleport, 1Password principles and best practices we adopt for architecture, naming, ontology (entity/multi-entity). | ENTERPRISE_IAM_SECRETS_ORCHESTRATION_TOOLS_AND_OUR_PRINCIPLES.md |
| **Product-that-builds-the-product tenet** | Architecture as core tenet; after each review, commands organized and architecture updated/reviewed. | PRODUCT_THAT_BUILDS_THE_PRODUCT_AND_ARCHITECTURE_TENET.md |
| **P/D/A/W classification** | Every audited section/function as probabilistic, deterministic, automated, workflow; industry vernacular. | full-review-summary.md; audits/artifacts/AUDITED_SECTIONS_CLASSIFICATION.md |
| **Three-pillar evaluation** | Success/quality, process/trajectory, safety. | REVIEW_AND_AUDIT_STAGES_IMPROVED.md; full-review-summary.md |
| **Waterfall scope (layers 1–7)** | OneWish OS → systems → repos → logic → workflows → MCPs → core features. | full-review-summary.md; audits/artifacts/README.md |
| **Mandatory checklist** | Derivative effects, emulation sources, Comprehensive Update, refined instructions, architecture/efficiency review, iron curtain, quality gate, agent menu, omni inventory. | full-review-summary.md; QUICK_AND_FULL_REVIEW.md |

---

## 6. Scripts and artifacts (index)

| Script | Role |
|--------|------|
| run-review.sh | Single entry for full Review (run-every-turn). |
| run-every-turn.sh | Go flow → codify → no-fail Comprehensive Review. |
| run-go-flow.sh | Route → sync → Full Review. |
| run-full-review.sh | Phase 1 verifications + Phase 2 summary + Phase 3 commands-and-architecture review. |
| run-comprehensive-eval-and-cleanup.sh | Full Review + 1P + connections + aggregate + post-run eval + commands-and-architecture review. |
| run-post-run-eval-loop.sh | Eval after run; chain-of-events; eval-after-run-latest. |
| run-commands-and-architecture-review.sh | Commands organized in place; architecture review; commands-and-architecture-review-latest.md. |
| run-omni-audit-and-never-miss.sh | Connect-and-configure + comprehensive + post-run eval. |
| run-quick-review.sh | Scope/effects per change. |
| codify-recommendations-to-scripts.sh | Recommendations → genie-from-recommendations-*.sh. |

| Artifact | Location |
|----------|----------|
| full-review-summary.md | docs/audits/full-review-summary.md |
| comprehensive-eval-and-cleanup-recommendations.md | docs/audits/ |
| chain-of-events.jsonl | docs/audits/chain-of-events.jsonl |
| eval-after-run-latest.json, .md | docs/audits/ |
| commands-and-architecture-review-latest.md | docs/audits/ |
| .full-review-last.log | scripts/.full-review-last.log |
| 1password-recommendations.json | config/mcp-servers/ |
| connections-report.json | docs/audits/ |

---

## 7. Flags and options (canonical)

| Script | Flag | Effect |
|--------|------|--------|
| run-post-run-eval-loop.sh | --run-type omni-audit \| comprehensive-eval \| full-review | Tag chain-of-events entry. |
| run-comprehensive-eval-and-cleanup.sh | --skip-full-review | Skip Full Review step; re-aggregate from existing outputs. |
| run-every-turn.sh | --skip-codify | Skip codify; Go flow + Comprehensive only. |
| run-every-turn.sh | --execute-codify | Run codify and execute generated genie script (default: dry-run). |
| run-full-review.sh | --skip-regenerate | Verifications only; no Phase 2 regenerate guidance. |
| codify-recommendations-to-scripts.sh | --dry-run \| --execute | Default dry-run; --execute runs generated script. |

Full list: [audits/EVAL_METRICS_FLAGS_AND_METHODS.md](audits/EVAL_METRICS_FLAGS_AND_METHODS.md).

---

## 8. References (master list)

| Doc | Purpose |
|-----|---------|
| [GAME_CHANGERS.md](GAME_CHANGERS.md) | Parent game changers list; Genie Magic; every turn. |
| [REVIEW_RESPONSE_AND_TOP_SOURCES.md](REVIEW_RESPONSE_AND_TOP_SOURCES.md) | Review response command; top repos/whitepapers; third-party tools. |
| [PRODUCT_THAT_BUILDS_THE_PRODUCT_AND_ARCHITECTURE_TENET.md](PRODUCT_THAT_BUILDS_THE_PRODUCT_AND_ARCHITECTURE_TENET.md) | Architecture as core tenet; commands-and-architecture review after each review. |
| [EVAL_LOOP_AND_CHAIN_OF_EVENTS.md](EVAL_LOOP_AND_CHAIN_OF_EVENTS.md) | Eval after each run; chain of events; best practices genie. |
| [audits/EVAL_METRICS_FLAGS_AND_METHODS.md](audits/EVAL_METRICS_FLAGS_AND_METHODS.md) | Eval metrics, flags, methods; chain JSONL schema. |
| [REVIEW_INDUSTRY_TERMS_BY_SPECIALIZATION_AND_DEVOPS.md](REVIEW_INDUSTRY_TERMS_BY_SPECIALIZATION_AND_DEVOPS.md) | Industry terms by specialization, core, game changers, principles, DevOps. |
| [ENTERPRISE_IAM_SECRETS_ORCHESTRATION_TOOLS_AND_OUR_PRINCIPLES.md](ENTERPRISE_IAM_SECRETS_ORCHESTRATION_TOOLS_AND_OUR_PRINCIPLES.md) | Enterprise IAM/secrets tools; how their principles mirror ours; best practices we adopt. |
| [COMMANDS_AND_SCRIPTS_INDEX.md](COMMANDS_AND_SCRIPTS_INDEX.md) | Canonical list of scripts; organize in place. |
| [NEVER_MISS_INSTRUCTIONS.md](NEVER_MISS_INSTRUCTIONS.md) | Sequence; when to use each script; single point of truth. |
| [QUICK_AND_FULL_REVIEW.md](QUICK_AND_FULL_REVIEW.md) | Full Review definition; triggers; mandatory checklist. |

---

_Maintain at: docs/GAME_CHANGER_REVIEW_AND_AUDIT_EXPANDED.md. Update when adding review types, steps, rules, or artifacts._
