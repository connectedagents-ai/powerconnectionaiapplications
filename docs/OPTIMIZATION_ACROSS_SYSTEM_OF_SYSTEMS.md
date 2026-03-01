# Optimization Across System of Systems — OneWish OS

**Purpose:** Single reference for **optimization levers** that apply across the whole system of systems (master + all downstream repos, dev tools, LLMs, MCPs, agents). Use this to run, share, and iterate on optimization so every node (Cursor, Claude Code, Codex, LitigationForce.AI, connected-agents-platform, file-management-toolkit, etc.) benefits.

**Governance:** [constitution.md](constitution.md); [GAME_CHANGERS.md](GAME_CHANGERS.md) (virtuous loop, eval system of systems); [ONEWISH_PROTOCOL.md](ONEWISH_PROTOCOL.md) §5 never-miss propagation.

---

## 1. What “optimization across SoS” means

| Concept                     | Meaning                                                                                                                                                                     |
| --------------------------- | --------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| **System of systems (SoS)** | Master repo (CURSOR CLOUD AGENTS) + all repos in `config/repos.yaml` (all_repos, ROUTES), all dev tools (Cursor, Claude Code, Codex), all LLMs, MCPs, and agents.           |
| **Optimization**            | Improve velocity, quality, cost, and alignment: sync, verify, improve score, fix connections, consolidate, and propagate so every node sees the same governance and config. |
| **Share**                   | Propagation so every downstream repo and dev tool has the same optimization docs, scripts, and checklist (route constitution, sync-all-repos, workspace, LLM config).       |

---

## 2. One-shot: run optimization across the whole SoS

From **master repo** run:

```bash
./scripts/activate-all-dev-tools-and-docker.sh --full-review
./scripts/run-comprehensive-eval-and-cleanup.sh
./scripts/improvement-score.sh
```

Or use the dedicated optimization runner (runs activate + improvement-score + optional comprehensive; syncs this doc to all repos):

```bash
./scripts/run-optimization-across-sos.sh
./scripts/run-optimization-across-sos.sh --with-comprehensive
```

---

## 3. Optimization levers (what to run and when)

| Lever                  | Script / doc                                                                                                          | Cadence                                | Effect across SoS                                                                             |
| ---------------------- | --------------------------------------------------------------------------------------------------------------------- | -------------------------------------- | --------------------------------------------------------------------------------------------- |
| **Canonical sync**     | `python3 scripts/sync-canonical-mcp-connectors.py`                                                                    | After editing canonical-mcp-connectors | platform-connections, .env.mcp.example, MCP_MAP aligned everywhere.                           |
| **Route constitution** | `./scripts/route-constitution-to-repos.sh`                                                                            | After governance change                | All ROUTES repos get same constitution, checklist, universal instructions, bootstrap.         |
| **Sync all repos**     | `./scripts/sync-all-repos-and-review.sh`                                                                              | Weekly / after doc change              | All §6a/6b/7 docs + LLM practices synced to every repo in all_repos.                          |
| **LLM config sync**    | (inside activate-all step 2c)                                                                                         | With activate-all                      | blackbox-agents, inference-models, platform-connections in every child config/.               |
| **Workspace refresh**  | `./scripts/sync-dev-tools-repos-from-config.sh`                                                                       | After repos.yaml change                | onewish-repos.code-workspace updated; Cursor/Claude Code/Codex see same roots.                |
| **Docker MCP**         | `./scripts/configure-docker-mcp.sh`                                                                                   | After Docker/1P change                 | Cursor connected to gateway; secrets in Docker keychain for catalog servers.                  |
| **Verify routing**     | `./scripts/verify-routing.sh`                                                                                         | With Full Review                       | LLM entry points (AGENTS, CLAUDE, agent manifest) reference constitution.                     |
| **Verify connections** | `./scripts/verify-all-connections.sh`                                                                                 | Advisory / before go-live              | Applications, MCPs, CLIs, LLMs, agents — feedback from each; report in docs/audits.           |
| **Full Review**        | `./scripts/run-full-review.sh`                                                                                        | Before commit, quarterly, on demand    | Verifications + mandatory checklist; summary in docs/audits/full-review-summary.md.           |
| **Comprehensive eval** | `./scripts/run-comprehensive-eval-and-cleanup.sh`                                                                     | With Full Review cadence               | Full Review + 1Password review + connections JSON + MERGE/ARCHIVE/DELETE/FIX recommendations. |
| **Improvement score**  | `./scripts/improvement-score.sh`                                                                                      | Monthly                                | Postmortems, patterns, lessons, rules → single score; virtuous loop velocity.                 |
| **Critical paths**     | [docs/audits/CRITICAL_PATHS.md](audits/CRITICAL_PATHS.md)                                                             | After genie/comprehensive              | P0/P1/P2 priorities (connections, dev-tools alignment, 1P, repo consolidation).               |
| **Dev environment**    | [docs/DEV_ENVIRONMENT_SETUP_AND_OPTIMIZATION.md](DEV_ENVIRONMENT_SETUP_AND_OPTIMIZATION.md)                           | New machine / tuning                   | Docker, MCPs, accounts; one-stop setup.                                                       |
| **GitHub + devtools**  | [docs/GITHUB_CONSOLIDATION_AND_DEVTOOLS_OPTIMIZATION_PLAN.md](GITHUB_CONSOLIDATION_AND_DEVTOOLS_OPTIMIZATION_PLAN.md) | Consolidation phase                    | Repo merge/archive, single account, Cursor/MCP/1Password optimization.                        |

---

## 4. Sharing optimization across SoS

- **This doc** is synced to all repos in `all_repos` when you run `./scripts/run-optimization-across-sos.sh` or when `OPTIMIZATION_ACROSS_SYSTEM_OF_SYSTEMS.md` is included in the sync list in `sync-all-repos-and-review.sh`.
- **Master files** (constitution, MASTER_INDEX, ALL_AGENTS_LLMS_MCPS_AND_CONNECTIONS, CRITICAL_PATHS, full-review-summary, comprehensive-eval-and-cleanup-recommendations) are already synced via sync-all-repos and activate-all; downstream repos and any dev tool opening them see the same state.
- **Single source of truth:** `config/repos.yaml`, `config/platform-connections.yaml`, `config/canonical-mcp-connectors.yaml`. Change there → run the scripts above → whole SoS stays optimized and aligned.

---

## 5. Checklist: optimization applied across SoS

- [ ] Run `./scripts/activate-all-dev-tools-and-docker.sh --full-review` (or `run-optimization-across-sos.sh`).
- [ ] Run `./scripts/improvement-score.sh` (monthly).
- [ ] Run `./scripts/run-comprehensive-eval-and-cleanup.sh` with Full Review cadence.
- [ ] Address P0/P1 from [CRITICAL_PATHS.md](audits/CRITICAL_PATHS.md) (connections, dev-tools alignment).
- [ ] Complete mandatory checklist in [full-review-summary.md](audits/full-review-summary.md).
- [ ] Apply MERGE/ARCHIVE/DELETE/FIX from [comprehensive-eval-and-cleanup-recommendations.md](audits/comprehensive-eval-and-cleanup-recommendations.md) per policy.
- [ ] Open `onewish-repos.code-workspace` in Cursor/Claude Code/Codex so all dev tools see the same roots.

---

## 6. References

| Doc                                                                                      | Purpose                                                          |
| ---------------------------------------------------------------------------------------- | ---------------------------------------------------------------- |
| [MASTER_INDEX.md](MASTER_INDEX.md)                                                       | Entry point; links to all optimization-related docs and scripts. |
| [audits/CRITICAL_PATHS.md](audits/CRITICAL_PATHS.md)                                     | P0/P1/P2 after genie run; SoS/agents/devtools what to run.       |
| [DEV_ENVIRONMENT_SETUP_AND_OPTIMIZATION.md](DEV_ENVIRONMENT_SETUP_AND_OPTIMIZATION.md)   | Docker, MCPs, accounts; full dev setup.                          |
| [ONEWISHOS_CROSS_TOOL_AND_FULL_INVENTORY.md](ONEWISHOS_CROSS_TOOL_AND_FULL_INVENTORY.md) | Cross-tool execution; scripts that connect/configure all.        |
| [GAME_CHANGERS.md](GAME_CHANGERS.md)                                                     | Virtuous loop; Master Agent evals system of systems.             |
