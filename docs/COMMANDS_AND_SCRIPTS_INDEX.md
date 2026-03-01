# Commands and Scripts Index — Organize in Place

**Purpose:** Canonical list of scripts in `scripts/` by category so that **all new commands are organized in place**. After each review, `run-commands-and-architecture-review.sh` checks that every script is listed here (and in NEVER_MISS or ONEWISH_OMNI where applicable); any new script is added to this index and to the appropriate “when to use” doc.

**Governance:** [PRODUCT_THAT_BUILDS_THE_PRODUCT_AND_ARCHITECTURE_TENET.md](PRODUCT_THAT_BUILDS_THE_PRODUCT_AND_ARCHITECTURE_TENET.md); [NEVER_MISS_INSTRUCTIONS.md](NEVER_MISS_INSTRUCTIONS.md); [ONEWISH_OMNI_MAC_DATA_MODEL_AND_COMMANDS.md](ONEWISH_OMNI_MAC_DATA_MODEL_AND_COMMANDS.md).

---

## 1. Entry points (main commands)

| Script | When to use | Doc |
|--------|-------------|-----|
| run-review.sh | Full Review (go + genie loop + comprehensive) in one command | REVIEW_RESPONSE_AND_TOP_SOURCES §0; NEVER_MISS §2 |
| run-go-flow.sh | Route → sync → Full Review only | GAME_CHANGERS; NEVER_MISS |
| run-full-review.sh | Before commit; repo/plan change; quarterly; on demand | NEVER_MISS §2; QUICK_AND_FULL_REVIEW |
| run-comprehensive-eval-and-cleanup.sh | Full Review + 1Password + connections + MERGE/ARCHIVE/DELETE/FIX | run-every-turn; comprehensive-eval |
| run-every-turn.sh | Go → codify → no-fail Comprehensive Review | GAME_CHANGERS “Every turn” |
| run-omni-audit-and-never-miss.sh | Omni inventory; quarterly; before commit when scope includes life/data | ONEWISH_OMNI_MAC_DATA_MODEL_AND_COMMANDS §1; mandatory checklist #9 |
| connect-and-configure-onewishos.sh | One-shot: route + sync + workspace + Full Review | NEVER_MISS §2 |
| run-audit-runbook.sh | Same as connect-and-configure; alternate entry | NEVER_MISS §2 |

---

## 2. Route, sync, propagation

| Script | When to use | Doc |
|--------|-------------|-----|
| route-constitution-to-repos.sh | After constitution/checklist/universal/bootstrap change | NEVER_MISS §2, §3 |
| sync-all-repos-and-review.sh | After doc/config change; weekly; before commit when master changed | NEVER_MISS §2, §3 |
| sync-dev-tools-repos-from-config.sh | After adding repo to config/repos.yaml; Claude Code/Codex same roots | NEVER_MISS §2 |
| sync-canonical-mcp-connectors.py | Immediately after editing canonical-mcp-connectors.yaml | NEVER_MISS §2 |
| push-to-claude-code-and-codex.sh | Sync + optional launch Claude Code or print Codex commands | MASTER_INDEX; CLAUDE.md |

---

## 3. Verify, eval, review

| Script | When to use | Doc |
|--------|-------------|-----|
| run-all-verifications.sh | Phase 1 of Full Review; routing, connections | run-full-review.sh |
| run-post-run-eval-loop.sh | After omni-audit, comprehensive-eval, full-review | EVAL_LOOP_AND_CHAIN_OF_EVENTS |
| run-quick-review.sh | Scope/effects per change; emulation check | QUICK_AND_FULL_REVIEW |
| run-cloud-agent-docs-review-and-copy.sh | Cloud agent review; copy developer/LLM/application docs; save to docs/knowledge, agent, combined | CLOUD_AGENT_DOCS_REVIEW_AND_KNOWLEDGE_COPY |
| verify-all-connections.sh | After adding MCP/connector; optional in Full Review | NEVER_MISS §2 |
| verify-routing.sh | Routing verification | run-all-verifications |
| verify-platform-connections.sh | Platform connections check | verify-all-connections |
| verify-env-example-sync.sh | .env.example sync | run-all-verifications |
| verify-skills.sh | Skills verification | run-all-verifications |
| codify-recommendations-to-scripts.sh | Turn recommendations into Genie-like scripts | GAME_CHANGERS; run-every-turn |
| run_eval.sh | Schema/regression eval vs data/synthetic/gold | evals.md |
| validate_schemas.sh | Schema validation | evals.md |
| validate-taxonomy.sh | Taxonomy validation | evals.md |
| validate-financial-audit-yaml.sh | Financial audit YAML | config/checklists |

---

## 4. 1Password, secrets, vault

| Script | When to use | Doc |
|--------|-------------|-----|
| 1password-execute-changes.sh | Execute approved 1P changes (dry-run or --execute) | 1PASSWORD_VAULT_ORGANIZATION |
| 1password-organize-vaults.sh | Organize vaults per taxonomy | ONEWISH_OMNI §2 |
| 1password-review-and-recommend.sh | Generate 1P recommendations JSON | run-comprehensive-eval |
| audit-1password-for-integrations.sh | Audit 1P for integrations | ONEWISH_OMNI §2 |
| agent-1password-index-env.sh | Index 1P into env for agents | platform-connections |
| build-1password-approved-full.sh | Build approved 1P file | 1P scripts |
| generate-1password-archive-by-date.sh | Archive 1P by date | 1P scripts |
| generate-1password-dedup-only-approved.sh | Dedup-only approved | 1P scripts |
| search-1password-for-mcp.sh | Search 1P for MCP | MCP setup |
| add-firecrawl-to-1password-devops.sh | Add Firecrawl to 1P DevOps | One-off |
| add-godaddy-login-to-1password.sh | Add GoDaddy to 1P | One-off |

---

## 5. MCP, Docker, dev tools

| Script | When to use | Doc |
|--------|-------------|-----|
| add-one-wish-agent-mcp.sh | Add One Wish Agent MCP | MCP_CONNECT_ONE_WISH_AGENT_EVERYWHERE |
| configure-docker-mcp.sh | Configure Docker MCP | activate-all-dev-tools |
| setup-mcp-with-1password.sh | Setup MCP with 1Password | MCP setup |
| activate-all-dev-tools-and-docker.sh | Activate all dev tools and Docker | NEVER_MISS; audits |
| setup-dev-environment.sh | Setup dev environment | BEGINNER_SETUP |
| setup-github-code-review.sh | Setup GitHub code review | Repo governance |
| install-git-hooks.sh | Install git hooks | Pre-commit |
| pre-commit-check-no-secrets.sh | Pre-commit no secrets | run-all-verifications |
| launch-ai-with-op.sh | Launch Claude/Codex with 1Password env | push-to-claude-code |

---

## 6. Repos, merge, archive, sync

| Script | When to use | Doc |
|--------|-------------|-----|
| sync-git-repos.sh | Sync git repos | Repo sync |
| merge-repo-into-target.sh | Merge repo into target | CONSOLIDATION |
| archive-repo.sh | Archive repo | CONSOLIDATION |
| delete-duplicate-repos-from-source-orgs.sh | Delete duplicate repos | GitHub cleanup |
| transfer-repos-to-connectedagents-ai.sh | Transfer repos to org | GitHub consolidation |
| add-code-review-to-repos.sh | Add code review to repos | Repo governance |
| sync-graphql-integration.sh | Sync GraphQL | Integrations |
| sync-notion-to-repo.sh | Sync Notion to repo | Integrations |

---

## 7. Evidence, ingestion, workflows

| Script | When to use | Doc |
|--------|-------------|-----|
| run-photo-document-to-evidence-ingestion.sh | Photo/document → evidence | workflows/SOCIAL_POST_AND_PHOTO |
| run-social-post-to-evidence-ingestion.sh | Social post → evidence | workflows |
| run-youtube-to-evidence-ingestion.sh | YouTube → evidence | workflows |
| run-scrape-with-screenshot.sh | Scrape with screenshot | Evidence ingestion |
| export-browser-tabs.sh | Export browser tabs | BROWSER_TABS_AND_1PASSWORD |
| export-and-merge-llm-platform-data.sh | Export/merge LLM platform data | Data ops |

---

## 8. Linear, buildout, optimization

| Script | When to use | Doc |
|--------|-------------|-----|
| run-linear-buildout.sh | Linear buildout | Linear integration |
| run-linear-buildout-scheduled.sh | Linear buildout scheduled | Linear |
| smoke-linear-buildout.sh | Smoke test Linear | Linear |
| run-optimization-across-sos.sh | Optimization across system of systems | OPTIMIZATION_ACROSS_SYSTEM_OF_SYSTEMS |
| run-e2e-devops-preset.sh | E2E DevOps preset | E2E |

---

## 9. Bootstrap, recommend, sources

| Script | When to use | Doc |
|--------|-------------|-----|
| bootstrap-repo-with-constitution.sh | Bootstrap repo with constitution | Repo onboarding |
| bootstrap-child-agents-claude.sh | Bootstrap child agents (Claude) | Agents |
| recommend-agents-and-frameworks.sh | Recommend agents and frameworks | BEGINNERS_GUIDE |
| sources-compare-and-update.sh | Compare and update sources | SOURCES_AND_EMULATION |
| improvement-score.sh | Improvement score | Evals |

---

## 10. Genie (codified), stage, login

| Script | When to use | Doc |
|--------|-------------|-----|
| genie-from-recommendations-*.sh | Generated by codify-recommendations-to-scripts; run with --dry-run or --execute | GAME_CHANGERS; run-every-turn |
| stage-and-commit-onewish-changes.sh | Stage and commit OneWish changes | Commit workflow |
| login-accounts.sh | Login accounts | Accounts |
| check-platform-status.sh | Check platform status | Status |
| archive-credentials-for-fresh-dev.sh | Archive credentials for fresh dev | Dev setup |
| download-tax-forms-for-options.sh | Download tax forms | One-off |

---

**Maintenance:** When adding a new script, add it to the appropriate category above and to NEVER_MISS_INSTRUCTIONS or ONEWISH_OMNI_MAC_DATA_MODEL_AND_COMMANDS if it is an entry point or domain command. Run `./scripts/run-commands-and-architecture-review.sh` after each review to ensure no script is missing from this index.

_Maintain at: docs/COMMANDS_AND_SCRIPTS_INDEX.md._
