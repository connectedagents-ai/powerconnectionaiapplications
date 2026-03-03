# Commands and Scripts Index — Organize in Place

**Purpose:** Canonical list of scripts in `scripts/` by category so that **all new commands are organized in place**. After each review, `run-commands-and-architecture-review.sh` checks that every script is listed here (and in NEVER_MISS or ONEWISH_OMNI where applicable); any new script is added to this index and to the appropriate “when to use” doc.

**Governance:** [PRODUCT_THAT_BUILDS_THE_PRODUCT_AND_ARCHITECTURE_TENET.md](PRODUCT_THAT_BUILDS_THE_PRODUCT_AND_ARCHITECTURE_TENET.md); [NEVER_MISS_INSTRUCTIONS.md](NEVER_MISS_INSTRUCTIONS.md); [ONEWISH_OMNI_MAC_DATA_MODEL_AND_COMMANDS.md](ONEWISH_OMNI_MAC_DATA_MODEL_AND_COMMANDS.md).

---

## 1. Entry points (main commands)

| Script                                                                      | When to use                                                                                                                                                                                                          | Doc                                                                                                    |
| --------------------------------------------------------------------------- | -------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | ------------------------------------------------------------------------------------------------------ |
| run-review.sh                                                               | Full Review (go + genie loop + comprehensive) in one command                                                                                                                                                         | REVIEW_RESPONSE_AND_TOP_SOURCES §0; NEVER_MISS §2                                                      |
| run-go-flow.sh                                                              | Route → sync → Full Review only                                                                                                                                                                                      | GAME_CHANGERS; NEVER_MISS                                                                              |
| run-full-review.sh                                                          | Before commit; repo/plan change; quarterly; on demand                                                                                                                                                                | NEVER_MISS §2; QUICK_AND_FULL_REVIEW                                                                   |
| run-comprehensive-eval-and-cleanup.sh                                       | Full Review + 1Password + connections + MERGE/ARCHIVE/DELETE/FIX                                                                                                                                                     | run-every-turn; comprehensive-eval                                                                     |
| run-every-turn.sh                                                           | Go → codify → no-fail Comprehensive Review                                                                                                                                                                           | GAME_CHANGERS “Every turn”                                                                             |
| run-omni-audit-and-never-miss.sh                                            | Omni inventory; quarterly; before commit when scope includes life/data                                                                                                                                               | ONEWISH_OMNI_MAC_DATA_MODEL_AND_COMMANDS §1; mandatory checklist #9                                    |
| connect-and-configure-onewishos.sh                                          | One-shot: route + sync + workspace + Full Review                                                                                                                                                                     | NEVER_MISS §2                                                                                          |
| run-audit-runbook.sh                                                        | Same as connect-and-configure; alternate entry                                                                                                                                                                       | NEVER_MISS §2                                                                                          |
| run-onewishos-all.sh                                                        | Sync canonical MCP/connectors then connect-and-configure (route, sync, workspace, Full Review); single command for full OneWish OS sync                                                                              | NEVER_MISS §2; ONEWISHOS_CROSS_TOOL_AND_FULL_INVENTORY §1.2                                            |
| run-onewishos-needful.sh [--all \| --preset \| --step \| --steps \| --list] | **Create/implement/fetch anything needed:** one-shot (--all), multi-step (--steps A,B,C), single-step (--step X); presets onewishos_all, needful_minimal, needful_full. Config: config/onewishos-needful-steps.yaml. | NEVER_MISS §2; config/onewishos-needful-steps.yaml; ONEWISHOS_MASTER_ARCHITECTURE_RULES_AND_SYSTEMS.md |

---

## 2. Route, sync, propagation

| Script                                                              | When to use                                                                                                                                                                                       | Doc                                                                                                    |
| ------------------------------------------------------------------- | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | ------------------------------------------------------------------------------------------------------ |
| route-constitution-to-repos.sh                                      | After constitution/checklist/universal/bootstrap change                                                                                                                                           | NEVER_MISS §2, §3                                                                                      |
| sync-all-repos-and-review.sh                                        | After doc/config change; weekly; before commit when master changed                                                                                                                                | NEVER_MISS §2, §3                                                                                      |
| sync-and-push-all-repos.sh                                          | Real-time sync: route + sync + commit and push in each child. Runs on every push (pre-push hook). Optional: --no-push, --dry-run                                                                  | REALTIME_SYNC_ALL_REPOS.md                                                                             |
| sync-dev-tools-repos-from-config.sh                                 | After adding repo to config/repos.yaml; Claude Code/Codex same roots                                                                                                                              | NEVER_MISS §2                                                                                          |
| sync-handoff-from-master.sh                                         | After editing HANDOFF_MASTER.md; writes docs/HANDOFF_TO_CODEX_CLAUDE_GEMINI.md + data/exports/handoff-latest.md + handoff-for-gemini-YYYYMMDD.md. GitHub Action runs on push.                     | HANDOFF_MASTER.md; PASTE_AND_WHERE_UNIVERSAL.md; .github/workflows/sync-handoff.yml                    |
| sync-canonical-mcp-connectors.py                                    | Immediately after editing canonical-mcp-connectors.yaml                                                                                                                                           | NEVER_MISS §2                                                                                          |
| push-to-claude-code-and-codex.sh                                    | Sync + optional launch Claude Code or print Codex commands                                                                                                                                        | MASTER_INDEX; CLAUDE.md                                                                                |
| one-repo-commit-push-and-align.sh [--dry-run \| --yes \| --no-push] | Beginner: commit key paths, push, sync workspace, copy handoff; prompts unless --yes                                                                                                              | BEGINNER_ONE_REPO_COMMIT_PUSH_AND_DEVTOOLS_ALIGN                                                       |
| check-one-repo-and-credentials-alignment.sh                         | Read-only: verify current folder is one repo; list where to revise APIs/SDKs/credentials/IDEs                                                                                                     | BEGINNER_ONE_REPO_COMMIT_PUSH_AND_DEVTOOLS_ALIGN; ONE_REPO_LOGS_CLEANUP_ORGANIZE_GITHUB_DEVTOOLS_INDEX |
| run-all-align-and-verify.sh [--no-connections]                      | Run sync, alignment check, verify-skills, verify-platform-connections, verify-onewishos-architecture, handoff copy; optional verify-all-connections. Writes data/audits/run-all-inventory-\*.txt. | ONE_REPO; run-full-review                                                                              |
| run-mission.sh [--list \| &lt;mission_id&gt;]                       | Run a named mission: align, verify, commit_push, full_sync, needful_all, credentials_audit, full_review, etc. Config: config/missions.yaml.                                                       | config/missions.yaml; NEVER_MISS                                                                       |

---

## 3. Verify, eval, review

| Script                                                    | When to use                                                                                                                                           | Doc                                                                                           |
| --------------------------------------------------------- | ----------------------------------------------------------------------------------------------------------------------------------------------------- | --------------------------------------------------------------------------------------------- |
| verify-onewishos-architecture-and-systems.sh [--json]     | Verify all paths in config/onewishos-master-architecture-systems.yaml (rules, architecture, repos, tools, agents, systems, multi-agent)               | ONEWISHOS_MASTER_ARCHITECTURE_RULES_AND_SYSTEMS.md                                            |
| run-all-verifications.sh                                  | Phase 1 of Full Review; routing, connections                                                                                                          | run-full-review.sh                                                                            |
| run-post-run-eval-loop.sh                                 | After omni-audit, comprehensive-eval, full-review                                                                                                     | EVAL_LOOP_AND_CHAIN_OF_EVENTS                                                                 |
| run-quick-review.sh                                       | Scope/effects per change; emulation check                                                                                                             | QUICK_AND_FULL_REVIEW                                                                         |
| verify-all-connections.sh                                 | After adding MCP/connector; optional in Full Review                                                                                                   | NEVER_MISS §2                                                                                 |
| verify-ai-llm-tools.sh [--json]                           | Env check for each tool in config/ai-llm-tools-canonical.yaml                                                                                         | AI_LLM_TOOLS_DEV_DOCS_REVIEW_AND_CANONICAL_LIST.md                                            |
| sync-ai-llm-tools-from-canonical.py [--dry-run]           | Add missing api-type tools from canonical to platform-connections llms                                                                                | AI_LLM_TOOLS_DEV_DOCS_REVIEW_AND_CANONICAL_LIST.md                                            |
| run-ai-llm-tools-verify-flow.sh [--full-review]           | Multi-flow: sync canonical → platform-connections, verify AI/LLM tools; optional Full Review                                                          | AI_LLM_TOOLS_DEV_DOCS_REVIEW_AND_CANONICAL_LIST.md; workflows-ai-llm-tools-verify.yaml        |
| run-super-agent-ask-and-gather.sh                         | Emit canonical ask (Codex, Cursor, Claude Code) and create placeholder gathered file; Claude Code compiles and memorializes                           | SUPER_AGENT_ASK_AND_COMPILATION.md; MASTER_FILE_COMMIT_REVIEW_AND_FINAL_DECISION_SYSTEM.md §7 |
| run-super-agent-review-with-references.sh [--full-review] | Optional Full Review, then emit ask (top references); create placeholder; next steps for manual gather/compile (manual optional when using full-auto) | SUPER_AGENT_ASK_AND_COMPILATION.md §2a, §4                                                    |
| run-super-agent-cursor-leg.sh                             | Fill Cursor section of latest super-agent-eval gathered file automatically (no manual step)                                                           | SUPER_AGENT_ASK_AND_COMPILATION.md                                                            |
| run-super-agent-compile-and-approve.sh [--commit]         | Compile latest gathered file into memorialized doc; optional git add + commit of memorialized and gathered                                            | SUPER_AGENT_ASK_AND_COMPILATION.md §4                                                         |
| run-super-agent-full-auto.sh [--full-review] [--commit]   | **No manual required:** ask+gather → Cursor leg → compile-and-approve; optional Full Review first and optional commit                                 | SUPER_AGENT_ASK_AND_COMPILATION.md §4; memorialized doc §4 Integration instructions           |
| run-apis-credentials-audit.sh                             | APIs/tokens/credentials audit step-by-step (baseline + op run, write result); --json                                                                  | audits/APIS_TOKENS_CREDENTIALS_SETUP_AND_TEST_AUDIT.md                                        |
| run-apis-credentials-self-improvement.sh [--vault VAULT]  | Run audit + integrate dry-run + 1P check; append last-run to self-improvement report                                                                  | audits/SELF_IMPROVEMENT_REPORT_APIS_CREDENTIALS_AND_1PASSWORD.md                              |
| run-github-deep-audit.sh [--with-env]                     | Phase Zero: read-only GitHub security/settings audit (repos, collaborators, branch protection, 2FA); report to data/audits/github-deep-audit          | GITHUB_DEEP_AUDIT_PHASE_ZERO.md                                                               |
| verify-routing.sh                                         | Routing verification                                                                                                                                  | run-all-verifications                                                                         |
| verify-platform-connections.sh                            | Platform connections check                                                                                                                            | verify-all-connections                                                                        |
| verify-env-example-sync.sh                                | .env.example sync                                                                                                                                     | run-all-verifications                                                                         |
| verify-skills.sh                                          | Skills verification                                                                                                                                   | run-all-verifications                                                                         |
| codify-recommendations-to-scripts.sh                      | Turn recommendations into Genie-like scripts                                                                                                          | GAME_CHANGERS; run-every-turn                                                                 |
| run_eval.sh                                               | Schema/regression eval vs data/synthetic/gold                                                                                                         | evals.md                                                                                      |
| validate_schemas.sh                                       | Schema validation                                                                                                                                     | evals.md                                                                                      |
| validate-taxonomy.sh                                      | Taxonomy validation                                                                                                                                   | evals.md                                                                                      |
| validate-financial-audit-yaml.sh                          | Financial audit YAML                                                                                                                                  | config/checklists                                                                             |

---

## 4. 1Password, secrets, vault

| Script                                                                                            | When to use                                                                                                                               | Doc                                                                                      |
| ------------------------------------------------------------------------------------------------- | ----------------------------------------------------------------------------------------------------------------------------------------- | ---------------------------------------------------------------------------------------- |
| 1password-execute-changes.sh                                                                      | Execute approved 1P changes (dry-run or --execute)                                                                                        | 1PASSWORD_VAULT_ORGANIZATION                                                             |
| 1password-organize-vaults.sh                                                                      | Organize vaults per taxonomy                                                                                                              | ONEWISH_OMNI §2                                                                          |
| 1password-review-and-recommend.sh                                                                 | Generate 1P recommendations JSON                                                                                                          | run-comprehensive-eval                                                                   |
| audit-1password-for-integrations.sh                                                               | Audit 1P for integrations                                                                                                                 | ONEWISH_OMNI §2                                                                          |
| agent-1password-index-env.sh                                                                      | Index 1P into env for agents                                                                                                              | platform-connections                                                                     |
| integrate-apis-1password.py [--inject] [--check] [--vault VAULT]                                  | Add all platform-connections env vars to .env.mcp.example (op://); optional op inject, 1P item check                                      | PLATFORMS_1PASSWORD_MAPPING; APIS_TOKENS_CREDENTIALS_SETUP_AND_TEST_AUDIT                |
| create-missing-credentials-and-integrate-1password.py [--vault] [--check-only] [--integrate-only] | Create missing API keys/accounts/MCP via CLI/API/manual; create 1P items in Developer Operations (or DevOps) vault; wire .env.mcp.example | CREATE_AND_INTEGRATE_APIS_CREDENTIALS_DESIGN.md; connector-creation-methods.yaml         |
| build-1password-approved-full.sh                                                                  | Build approved 1P file                                                                                                                    | 1P scripts                                                                               |
| generate-1password-archive-by-date.sh                                                             | Archive 1P by date                                                                                                                        | 1P scripts                                                                               |
| generate-1password-dedup-only-approved.sh                                                         | Dedup-only approved                                                                                                                       | 1P scripts                                                                               |
| search-1password-for-mcp.sh                                                                       | Search 1P for MCP                                                                                                                         | MCP setup                                                                                |
| add-firecrawl-to-1password-devops.sh                                                              | Add Firecrawl to 1P DevOps                                                                                                                | One-off                                                                                  |
| add-godaddy-login-to-1password.sh                                                                 | Add GoDaddy to 1P                                                                                                                         | One-off                                                                                  |
| push-and-copy-handoff-to-dev-tools.sh [--push]                                                    | Check access (gh, op); sync workspace; copy handoff to data/exports for Gemini; optional git commit and push                              | WHAT_TO_PUSH_AND_COPY; PASTE_AND_WHERE_UNIVERSAL.md (what to paste and where, all tools) |
| run-zoom-remove-note-takers.sh [--visible \| --headless]                                          | Remove Zoom note takers (Clapp AI, Read.ai); login from 1Password; archive to data/archives/zoom-account-archives                         | ZOOM_NOTE_TAKERS_REMOVAL.md                                                              |
| run-omni-token-discovery.sh [--with-env]                                                          | Find all dev/AI accounts and API keys (HF, GCP, Figma, Replit, Lovable, etc.); report to data/audits/omni-token-discovery                 | OMNI_TOKEN_DISCOVERY_AND_SSOT.md                                                         |

---

## 5. MCP, Docker, dev tools

| Script                               | When to use                                                                                                          | Doc                                   |
| ------------------------------------ | -------------------------------------------------------------------------------------------------------------------- | ------------------------------------- |
| add-one-wish-agent-mcp.sh            | Add One Wish Agent MCP                                                                                               | MCP_CONNECT_ONE_WISH_AGENT_EVERYWHERE |
| configure-docker-mcp.sh              | Configure Docker MCP                                                                                                 | activate-all-dev-tools                |
| setup-mcp-with-1password.sh          | Setup MCP with 1Password                                                                                             | MCP setup                             |
| activate-all-dev-tools-and-docker.sh | Activate all dev tools and Docker                                                                                    | NEVER_MISS; audits                    |
| setup-dev-environment.sh             | Setup dev environment                                                                                                | BEGINNER_SETUP                        |
| setup-github-code-review.sh          | Setup GitHub code review                                                                                             | Repo governance                       |
| install-git-hooks.sh                 | Install git hooks                                                                                                    | Pre-commit                            |
| pre-commit-check-no-secrets.sh       | Pre-commit no secrets                                                                                                | run-all-verifications                 |
| launch-ai-with-op.sh                 | Launch Claude/Codex with 1Password env                                                                               | push-to-claude-code                   |
| run-connector-signup-agent.sh        | HTTP/browser agent to sign up for a connector (config: config/connector-signup-agent.yaml; env: CONNECTOR*SIGNUP*\*) | connector-signup-agent.yaml           |

---

## 6. Repos, merge, archive, sync

| Script                                      | When to use                                                                  | Doc                                     |
| ------------------------------------------- | ---------------------------------------------------------------------------- | --------------------------------------- |
| sync-git-repos.sh                           | Sync git repos                                                               | Repo sync                               |
| merge-repo-into-target.sh                   | Merge repo into target                                                       | CONSOLIDATION                           |
| archive-repo.sh                             | Archive repo                                                                 | CONSOLIDATION                           |
| delete-duplicate-repos-from-source-orgs.sh  | Delete duplicate repos                                                       | GitHub cleanup                          |
| transfer-repos-to-connectedagents-ai.sh     | Transfer repos to org                                                        | GitHub consolidation                    |
| add-code-review-to-repos.sh                 | Add code review to repos                                                     | Repo governance                         |
| sync-graphql-integration.sh                 | Sync GraphQL                                                                 | Integrations                            |
| sync-notion-to-repo.sh                      | Sync Notion to repo                                                          | Integrations                            |
| generate-fleet-inventory.sh                 | Generate \_scan/out/FLEET_INVENTORY.md from config/repos.yaml and GitHub API | FLEET_INVENTORY_AND_SCAN_OUT; WHAT_ELSE |
| compare-onewishos-with-connectedagents.sh   | Diff key files/dirs between this repo and Connectedagentsrepo1; report       | ONEWISHOS_REPO_INTEGRATION_PLAN         |
| integrate-onewishos-from-connectedagents.sh | Copy onewishos/, CodeAppDocs-style content, tools→scripts, workflows         | ONEWISHOS_REPO_INTEGRATION_PLAN         |

---

## 7. Evidence, ingestion, workflows

| Script                                      | When to use                    | Doc                             |
| ------------------------------------------- | ------------------------------ | ------------------------------- |
| run-photo-document-to-evidence-ingestion.sh | Photo/document → evidence      | workflows/SOCIAL_POST_AND_PHOTO |
| run-social-post-to-evidence-ingestion.sh    | Social post → evidence         | workflows                       |
| run-youtube-to-evidence-ingestion.sh        | YouTube → evidence             | workflows                       |
| run-scrape-with-screenshot.sh               | Scrape with screenshot         | Evidence ingestion              |
| export-browser-tabs.sh                      | Export browser tabs            | BROWSER_TABS_AND_1PASSWORD      |
| export-and-merge-llm-platform-data.sh       | Export/merge LLM platform data | Data ops                        |

---

## 8. Linear, buildout, optimization

| Script                           | When to use                           | Doc                                   |
| -------------------------------- | ------------------------------------- | ------------------------------------- |
| run-linear-buildout.sh           | Linear buildout                       | Linear integration                    |
| run-linear-buildout-scheduled.sh | Linear buildout scheduled             | Linear                                |
| smoke-linear-buildout.sh         | Smoke test Linear                     | Linear                                |
| run-optimization-across-sos.sh   | Optimization across system of systems | OPTIMIZATION_ACROSS_SYSTEM_OF_SYSTEMS |
| run-e2e-devops-preset.sh         | E2E DevOps preset                     | E2E                                   |

---

## 9. Bootstrap, recommend, sources

| Script                                  | When to use                                                                                         | Doc                                        |
| --------------------------------------- | --------------------------------------------------------------------------------------------------- | ------------------------------------------ |
| bootstrap-repo-with-constitution.sh     | Bootstrap repo with constitution                                                                    | Repo onboarding                            |
| bootstrap-child-agents-claude.sh        | Bootstrap child agents (Claude)                                                                     | Agents                                     |
| recommend-agents-and-frameworks.sh      | Recommend agents and frameworks                                                                     | BEGINNERS_GUIDE                            |
| sources-compare-and-update.sh           | Compare and update sources                                                                          | SOURCES_AND_EMULATION                      |
| improvement-score.sh                    | Improvement score                                                                                   | Evals                                      |
| run-cloud-agent-docs-review-and-copy.sh | Cloud agent docs review + copy developer/LLM/app docs to knowledge; optional --copy-only, --dry-run | CLOUD_AGENT_DOCS_REVIEW_AND_KNOWLEDGE_COPY |

---

## 10. Genie (codified), stage, login

| Script                               | When to use                                                                     | Doc                           |
| ------------------------------------ | ------------------------------------------------------------------------------- | ----------------------------- |
| genie-from-recommendations-\*.sh     | Generated by codify-recommendations-to-scripts; run with --dry-run or --execute | GAME_CHANGERS; run-every-turn |
| stage-and-commit-onewish-changes.sh  | Stage and commit OneWish changes                                                | Commit workflow               |
| login-accounts.sh                    | Login accounts                                                                  | Accounts                      |
| check-platform-status.sh             | Check platform status                                                           | Status                        |
| archive-credentials-for-fresh-dev.sh | Archive credentials for fresh dev                                               | Dev setup                     |
| download-tax-forms-for-options.sh    | Download tax forms                                                              | One-off                       |

---

## 11. Calendar Unified (Google, Microsoft, Apple, CRM/agents)

| Script                                      | When to use                                                                | Doc                                        |
| ------------------------------------------- | -------------------------------------------------------------------------- | ------------------------------------------ |
| calendar-unified/scripts/setup-all.sh       | One-time install for Option 1, 2, 3; create config from examples           | calendar-unified/README.md                 |
| calendar-unified/scripts/run-option-1.sh    | Start unified calendar API (single REST API for Google/Microsoft/CalDAV)   | calendar-unified/docs/ARCHITECTURE.md      |
| calendar-unified/scripts/run-option-2.sh    | Run calendar sync once (sources → one destination); use cron for recurring | calendar-unified/docs/WHEN_TO_USE_WHICH.md |
| calendar-unified/scripts/run-option-3.sh    | Start webhook hub (receive webhooks, normalize, forward to CRM/automation) | calendar-unified/docs/ARCHITECTURE.md      |
| calendar-unified/scripts/config-from-env.sh | Refresh config from .env.calendar or 1Password (op run)                    | calendar-unified/README.md                 |
| calendar-unified/scripts/validate-config.sh | Validate YAML configs and env for all three options                        | calendar-unified/README.md                 |

---

## 12. OneDrive / path length

| Script                                              | When to use                                                                                               | Doc                                 |
| --------------------------------------------------- | --------------------------------------------------------------------------------------------------------- | ----------------------------------- |
| scripts/onedrive-path-fix/find-long-paths.sh        | Find files/folders with path length over limit (default 200); pass OneDrive root, optional --max-length N | ONEWISHOS_ONEDRIVE_PATH_FIX_PLAN.md |
| scripts/onedrive-path-fix/shorten-onedrive-paths.py | Shorten folder names (hex truncation + abbreviations); --dry-run (default), --execute to apply            | ONEWISHOS_ONEDRIVE_PATH_FIX_PLAN.md |
| scripts/onedrive-path-fix/run-ongoing-check.sh      | Weekly/cron: run find-long-paths, optional --report DIR to save timestamped report                        | ONEWISHOS_ONEDRIVE_PATH_FIX_PLAN.md |

---

**Maintenance:** When adding a new script, add it to the appropriate category above and to NEVER_MISS_INSTRUCTIONS or ONEWISH_OMNI_MAC_DATA_MODEL_AND_COMMANDS if it is an entry point or domain command. Run `./scripts/run-commands-and-architecture-review.sh` after each review to ensure no script is missing from this index.

_Maintain at: docs/COMMANDS_AND_SCRIPTS_INDEX.md._
