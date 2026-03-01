# Master Files and Review-Before-Action

**Purpose:** Ensure structure and architecture are **completely, accurately, and efficiently articulated** through best practices and **constantly improved and reviewed**. No high-impact action (rename, consolidation, migration, new capability) proceeds until the relevant master files have been reviewed and are current.

**Rule:** **Review master files before any action.** Use the loop below so master files stay the single source of truth and improve over time.

---

## 1. What are master files?

Master files are the **canonical set of docs and configs** that define:

- **Governance** — Constitution, human-in-loop, claim typing, audit, safety
- **Structure** — Repo map, consolidation status, segment/organization
- **Architecture** — MCP/vendor list, connectors, inference routing, agent roles
- **Secrets and tooling** — 1Password, env, MCP servers, dev-tool setup
- **Plans** — Active multi-phase plans (e.g. GitHub consolidation, rename) that change structure

If a doc or config is the **single place** that describes how something works or what is canonical, it is a master file for that scope.

---

## 2. Master files index (review before action)

Review these **before** executing any phase of a major plan (rename, consolidation, new capability, migration). Keep them in sync with each other and with reality.

### 2.1 Governance (non-negotiable)

| File                                                                                | Scope                                                                                                                                                                                                                                                                                         |
| ----------------------------------------------------------------------------------- | --------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| [docs/ONEWISH_LOGIC.md](ONEWISH_LOGIC.md)                                           | **OneWish OS + OneWish Logic:** OneWish Operating System(s) (full operational dimension); OneWish Logic (protocol, checks, audits); map; core features; OneWish Workflows, Apps, Scripts, Stages, Architecture, Systems of Systems; planned systems (Ollama, Claudebot, Web agents, OpenClaw) |
| [docs/constitution.md](constitution.md)                                             | Human-in-loop, claim typing, audit, bias/safety; OneWish Protocol, rigid review, improvement                                                                                                                                                                                                  |
| [docs/ONEWISH_PROTOCOL.md](ONEWISH_PROTOCOL.md)                                     | Architecture, sync, **never-miss propagation** (§5), rigid review, improvement, **special projects** (§6); downstream repos per OneWish                                                                                                                                                       |
| [docs/SPECIAL_PROJECTS_AND_METHODS.md](SPECIAL_PROJECTS_AND_METHODS.md)             | Methods and related tools per special project type; read when running a special project                                                                                                                                                                                                       |
| [.github/agents/my-agent.agent.md](../.github/agents/my-agent.agent.md)             | Agent spec, vendor inventory, multi-agent roles                                                                                                                                                                                                                                               |
| [.cursor/rules/master-project-rules.mdc](../.cursor/rules/master-project-rules.mdc) | Always-apply Cursor rules                                                                                                                                                                                                                                                                     |

### 2.2 Structure and repo map

| File                                                                                                                  | Scope                                                                                                                                                       |
| --------------------------------------------------------------------------------------------------------------------- | ----------------------------------------------------------------------------------------------------------------------------------------------------------- |
| [docs/MASTER_INDEX.md](MASTER_INDEX.md)                                                                               | Single entry point; links to all canonical docs                                                                                                             |
| [docs/CONSOLIDATION_AND_REPO_STATUS.md](CONSOLIDATION_AND_REPO_STATUS.md)                                             | Canonical repo map, consolidation status, cloud/inference, archives                                                                                         |
| [docs/GITHUB_CONSOLIDATION_AND_DEVTOOLS_OPTIMIZATION_PLAN.md](GITHUB_CONSOLIDATION_AND_DEVTOOLS_OPTIMIZATION_PLAN.md) | Phases: audit → merge/archive → one account → settings                                                                                                      |
| Rename plan (e.g. OneWishAgents-AI)                                                                                   | Org/repo/display renames; path and script updates                                                                                                           |
| [docs/reports/ONEWISH_REPO_ARCHITECTURE_AND_HOW_IT_WORKS.md](reports/ONEWISH_REPO_ARCHITECTURE_AND_HOW_IT_WORKS.md)   | How this repo is architected and works (master files, constitution, automations, bidirectional sync, pushes); onboarding and audits                         |
| [docs/SECOND_LEVEL_REPOS_AND_INTERCONNECTIONS.md](SECOND_LEVEL_REPOS_AND_INTERCONNECTIONS.md)                         | Second-level repos (Financial Audit & Tax, LitigationForce.AI, RobertBaileyFamilyOffice); interconnections; bidirectional sync; OneWish OS strict mirroring |

### 2.2a Narrative / family and third-party

| File                                                                                              | Scope                                                                                          |
| ------------------------------------------------------------------------------------------------- | ---------------------------------------------------------------------------------------------- |
| [docs/TAKE_HOME_ARCHITECTURE_OVERVIEW.md](TAKE_HOME_ARCHITECTURE_OVERVIEW.md)                     | Plain-language architecture for family; OneWishAgents-AI, Connected OneWishMCP, tool ecosystem |
| [docs/ARCHITECTURE_FOR_THIRD_PARTY_PRESENTATION.md](ARCHITECTURE_FOR_THIRD_PARTY_PRESENTATION.md) | Concise architecture for investors/partners/clients; safe to share externally                  |

Review these before changing org/repo names or master narrative so the explain-to-family and external story stay aligned with the rename and with Connected OneWishMCP + tool-list recommendations.

### 2.3 Architecture and integrations

| File                                                                                                          | Scope                                                                                                                                 |
| ------------------------------------------------------------------------------------------------------------- | ------------------------------------------------------------------------------------------------------------------------------------- |
| [config/mcp-servers/master-mcp.yaml](../config/mcp-servers/master-mcp.yaml)                                   | MCP servers, vendors, LLM routing, connectors                                                                                         |
| [docs/MODULAR_TOOLS_AND_ENDPOINTS_INVENTORY.md](MODULAR_TOOLS_AND_ENDPOINTS_INVENTORY.md)                     | Modular tools registry; quick reference/command; efficiency review vs goals/repos                                                     |
| [docs/AGENT_MASTER_REPO_INSTRUCTIONS.md](AGENT_MASTER_REPO_INSTRUCTIONS.md)                                   | DevOps, tokens, LLM use cases; keep in sync with master-mcp.yaml                                                                      |
| [docs/MCP_SECRETS_REFERENCE.md](MCP_SECRETS_REFERENCE.md)                                                     | Cursor secrets, env vars, 1Password items                                                                                             |
| [docs/PLATFORMS_1PASSWORD_MAPPING.md](PLATFORMS_1PASSWORD_MAPPING.md)                                         | Platform → env → 1Password                                                                                                            |
| [docs/1PASSWORD_VAULT_ORGANIZATION.md](1PASSWORD_VAULT_ORGANIZATION.md)                                       | Vault taxonomy, team (powerconnection.ai)                                                                                             |
| [docs/BEST_PRACTICES_FROM_TOP_REPOS_TO_ADD_OR_EMULATE.md](BEST_PRACTICES_FROM_TOP_REPOS_TO_ADD_OR_EMULATE.md) | Best practices from top repos (GitHub, MCP, OSS) to add or emulate; review when adding repo-level governance or MCP design; quarterly |
| [docs/LLM_AI_MULTIAGENT_AND_SYSTEMS_BEST_PRACTICES.md](LLM_AI_MULTIAGENT_AND_SYSTEMS_BEST_PRACTICES.md)     | Design, setup, naming, structure for LLM/AI/multi-agent/cloud/private LLMs/dev tools/robotics; **all systems from now on** defined per this doc; review when adding or changing any system, agent, MCP, workflow, or repo structure |
| [docs/SOURCES_AND_EMULATION_INDEX.md](SOURCES_AND_EMULATION_INDEX.md) §11b, [docs/AGENT_FUNCTION_SOURCES_WHITEPAPERS_CONSTITUTIONS_REPOS.md](AGENT_FUNCTION_SOURCES_WHITEPAPERS_CONSTITUTIONS_REPOS.md) | **Top LLMs and applications** — emulation, open source repos, white papers, dev docs. Reference/incorporate where relevant for constitutional, top-level, OneWish OS, Genie desktop, master-synced, never-miss, and Full Review. See constitution §7; NEVER_MISS_INSTRUCTIONS §1. |

### 2.4 Entry points by tool

| File                                                        | Scope                       |
| ----------------------------------------------------------- | --------------------------- |
| [AGENTS.md](../AGENTS.md)                                   | READ FIRST + manifest       |
| [CLAUDE.md](../CLAUDE.md)                                   | READ FIRST + project memory |
| [docs/UNIVERSAL_INSTRUCTIONS.md](UNIVERSAL_INSTRUCTIONS.md) | Tool-agnostic bootstrap     |

---

## 3. Review-before-action rule

**Before any of the following, complete a pass over the relevant master files (at least §2.1 and the rows in §2.2–2.4 that your action touches):**

- Executing a **phase** of the rename plan (e.g. Phase 1 GitHub, Phase 2 replacements)
- Executing a **phase** of GitHub consolidation (audit, transfer, decommission, settings)
- Adding a **new capability** (MCP, connector, agent, repo)
- Changing **org/repo names**, **paths**, or **canonical repo map**
- Changing **governance** (constitution, agent spec, rules)
- Running **destructive or bulk scripts** (transfer, merge, archive, delete)

**Check:**

1. Are the master files that describe this action **current** (names, URLs, paths, status)?
2. Does the action **match** what those files say (e.g. target org, repo list, vault)?
3. After the action, will you **update** those same master files so they stay accurate?
4. **Every review** that touches master files or follows a commit to master includes **commit review and final decision**: retroactive review (Claude Code, Cursor, Codex), gather to `docs/audits/commit-review-gathered/`, rerun, Claude Code final decisions on OneWish OS. See [MASTER_FILE_COMMIT_REVIEW_AND_FINAL_DECISION_SYSTEM.md](MASTER_FILE_COMMIT_REVIEW_AND_FINAL_DECISION_SYSTEM.md); Full Review mandatory checklist item #10.

If any answer is no, update the master files first, then proceed.

---

## 4. The review loop (constant improvement)

Structure and architecture stay articulated and improve only if review is **repeated**.

### 4.1 When to run the loop

| Trigger                                       | What to review                                                                                                                                                                                                   |
| --------------------------------------------- | ---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| **Before each phase** of a multi-phase plan   | §2.1 + §2.2 (and §2.3 if phase touches MCP/secrets)                                                                                                                                                              |
| **After each phase**                          | Update CONSOLIDATION_AND_REPO_STATUS, plan doc, and any changed paths/names in master files                                                                                                                      |
| **Quarterly**                                 | Full pass: constitution, agent spec, MASTER_INDEX, CONSOLIDATION_AND_REPO_STATUS, master-mcp.yaml, secrets/vault docs                                                                                            |
| **When reviewing tool/vendor list**           | Run `scripts/recommend-tools-from-list.py` on the list; update MODULAR_TOOLS_AND_ENDPOINTS_INVENTORY, canonical, matrix; see [TOOL_LIST_UPLOAD_AND_RECOMMENDATIONS.md](TOOL_LIST_UPLOAD_AND_RECOMMENDATIONS.md). |
| **When integrating from starred/other repos** | See §5 below; then update master files if you adopt new structure or patterns                                                                                                                                    |

### 4.2 How to review (best practices)

- **Completeness** — Every canonical repo, org, vault, and connector is named and has a single source of truth in a master file.
- **Accuracy** — Names, URLs, paths, and status match the current state (GitHub, 1Password, local paths).
- **Efficiency** — No duplicate or conflicting definitions; one place per concept; links from MASTER_INDEX to details.
- **Improvement** — Each pass: fix one inconsistency, clarify one section, or add one missing link. Document the change in the file or in a short audit note.

### 4.3 Who does the review

- **Human** — Attorney or operator confirms governance and high-impact changes.
- **Agent** — Can propose edits to master files; human approves before merge or before running scripts that depend on them.

---

## 5. Starred and other repos: review and integrate

Various **repos and starred repos** should be reviewed and, where applicable, **integrated in parts** to:

- **Optimize** — Better patterns, fewer steps, clearer structure
- **Professionalize** — Naming, docs, and checklists that match industry practice
- **Upgrade** — New patterns (MCP, agents, security, CI) that improve the platform
- **Modify** — Adjust working repos and **master files** so they reflect adopted patterns

**Process:**

1. **List** — Maintain a short list in [docs/STARRED_AND_REFERENCE_REPOS.md](STARRED_AND_REFERENCE_REPOS.md) of starred/reference repos and what each is used for (e.g. “MCP patterns”, “agent layout”, “security baseline”).
2. **Review** — Periodically open a reference repo and note: one pattern, one doc structure, or one config approach that could apply to this workspace.
3. **Integrate in parts** — Propose a **small** change (one doc, one section, one script pattern) and update the **relevant master file** so the change is articulated in the canonical structure.
4. **Gate** — Before applying the change at scale, review the affected master files per §3 and §4.

This keeps master files and working repos improving without big, untracked imports.

---

## 6. Summary

- **Master files** = governance + structure + architecture + secrets/plans (§2).
- **Review before action** = no rename/consolidation/capability/migration phase without checking and, if needed, updating the relevant master files (§3).
- **Loop** = before/after each phase, quarterly, and when integrating from other repos; aim for complete, accurate, efficient articulation and constant improvement (§4).
- **Starred/other repos** = review and selectively integrate into working repos and master files, in parts, with master-file updates and review-before-action (§5).

Keeping this discipline ensures structure and architecture stay clearly articulated and improve over time.

---

**Cross-references**

| Doc                                                                                                              | Purpose                                |
| ---------------------------------------------------------------------------------------------------------------- | -------------------------------------- |
| [MASTER_INDEX.md](MASTER_INDEX.md)                                                                               | Entry point; includes link to this doc |
| [CONSOLIDATION_AND_REPO_STATUS.md](CONSOLIDATION_AND_REPO_STATUS.md)                                             | Repo map; consolidation status         |
| [GITHUB_CONSOLIDATION_AND_DEVTOOLS_OPTIMIZATION_PLAN.md](GITHUB_CONSOLIDATION_AND_DEVTOOLS_OPTIMIZATION_PLAN.md) | Multi-account consolidation            |
| [NEW_CAPABILITY_CHECKLIST.md](NEW_CAPABILITY_CHECKLIST.md)                                                       | New tool/agent/skill flow              |
| [QUICK_AND_FULL_REVIEW.md](QUICK_AND_FULL_REVIEW.md)                                                             | Review triggers and checklist          |

_Maintain at: docs/MASTER_FILES_AND_REVIEW_BEFORE_ACTION.md._
