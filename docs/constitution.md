# Constitution — LitigationForce.AI

> Non-negotiable principles for all AI agents and outputs. Referenced by `.github/agents/my-agent.agent.md`, `.cursor/rules/master-project-rules.mdc`, and platform documentation.

---

## 1. Human-in-the-Loop Checkpoints

High-stakes outputs **must** route through human review:

- Privilege determinations
- Filings and productions
- Expert narratives
- Damages conclusions
- Compliance determinations

Never auto-approve; always prompt for attorney sign-off.

---

## 2. Claim Typing

Every assertion carries a type:

| Type               | Definition                           | Gate Required               |
| ------------------ | ------------------------------------ | --------------------------- |
| `FACT`             | Directly supported by cited evidence | Fact Checker                |
| `INFERENCE`        | Logically derived from facts         | Logic Auditor               |
| `OPINION`          | Expert or analytical judgment        | Ethics Reviewer             |
| `LEGAL_CONCLUSION` | Legal standard application to facts  | Citation Validator + Ethics |

FACT claims require an evidence pointer and quoted excerpt (or UNVERIFIED).

---

## 3. Explainability & Audit

- Preserve prompts, tool calls, parameters, outputs, evaluator results
- Immutable audit trail for every transformation
- Processing history: stage, agent, timestamp, input_hash, output_hash

---

## 4. Bias & Safety

- Evaluate for bias and harmful outputs
- Document mitigations
- Require attorney review for sensitive inferences

---

## 5. Simulation Disclaimer

All litigation outputs are drafts for support only. Not legal advice. Attorney review required before use in legal proceedings.

---

## 6. Actions (Execution)

**Default: agents execute.** Agents must take actions through **terminal, SDKs, IDEs, and/or CLIs** — not the user. The agent executes via terminal or similar methods; do not ask the user to run commands that the agent can run. Do not describe or simulate without executing.

---

## 6.5 Automated Recursive Virtuous Learning; Harnessed Complexity

OneWish OS is **automated**, **recursive**, and **virtuous**: it continuously **learns** (lean learning), **expands**, **spawns**, **integrates**, and **uses tools** in a loop that feeds improvement. This complexity is **harnessed** by **detailed, scientifically founded instructions and rules**, **sequences and connections**, and **MCPs** (and related config) so that behavior is controlled, traceable, and improvable.

At **each stage** (planning, execution, review, handoff, recurring cadence), **always provide**: (1) an **example of outcome** and **derivative outcomes** (what else is impacted); (2) a **chart or graph** (or reference to one) so that evolution is **controlled**, **understood**, and **perfected** at that stage. Derivative outcomes and emulation sources are mandatory per Full Review; diagrams and stage-by-stage artifacts are in the audit and framework docs.

**References:** Stages and required audits/reviews: `docs/FRAMEWORK_AUDITS_REVIEWS_INTEGRATIONS_BY_STAGE.md`. Derivative effects and emulation: `docs/QUICK_AND_FULL_REVIEW.md`. Waterfall and verification diagrams: `docs/audits/artifacts/README.md`. Lifecycle stages: `docs/LIFECYCLE_STAGES_AND_CHECKPOINTS.md`.

---

## 7. New Capabilities (Toolkits, Agents, Skills)

When creating any new tool, toolkit, agent, or platform capability:

1. **Read first**: This constitution, `.github/agents/my-agent.agent.md`, `.cursor/rules/master-project-rules.mdc`
2. **Create skill**: Add `.cursor/skills/{capability-name}/SKILL.md` so agents know when and how to use it
3. **Use ontology skills**: For schemas, lists, entity names — `.cursor/skills/ontology-schema-syntax/`, `lists-todos-projects/`, `names-and-connections/`
4. **Update indexes**: `docs/cross-system-index.md` (new repos), `agents/MASTER_AGENT_INDEX.md` (new agents/skills)
5. **Emulate reference patterns**: For file/evidence systems → `docs/modules/lexvault.md`; for entity schemas → `docs/modules/ontology.md`; for UI/modules → `docs/MODULE_ARCHITECTURE_AND_PLATFORM_STACK.md` and `config/module-selection.yaml`. See `docs/REFERENCE_PATTERNS_AND_EXAMPLE_REPOS.md`.

Full checklist: `docs/NEW_CAPABILITY_CHECKLIST.md`. Repo status: `docs/CONSOLIDATION_AND_REPO_STATUS.md`. **Master index**: `docs/MASTER_INDEX.md`. **Accounts login**: `./scripts/login-accounts.sh` — see `docs/ACCOUNTS_LOGIN_PROCESS.md`. **Fundamental strategies**: `docs/FUNDAMENTAL_STRATEGIES_AND_SPECIFICATIONS.md` (agent types, modular dev, design, MCP). **MCP connectivity**: `docs/MCP_MASTER_SERVER_AND_CONNECTIVITY_STRATEGY.md`. **Sources per action**: `docs/SOURCES_AND_EMULATION_INDEX.md`. **Pre-execution checklist**: `docs/SUPER_DEVELOPER_PRE_EXECUTION_CHECKLIST.md`. **Expert prompting**: `docs/EXPERT_PROMPT_ENGINEERING.md`. **Lifecycle checkpoints**: `docs/LIFECYCLE_STAGES_AND_CHECKPOINTS.md`. **Agent orchestration**: `docs/AGENT_ORCHESTRATION_BEST_PRACTICES.md`. **Zero-mistake workflow**: `.cursor/skills/zero-mistake-workflow/SKILL.md`. **Virtuous loop**: failure→postmortem, success→patterns-that-work, session→lessons. **Quarterly sources review**: `./scripts/sources-compare-and-update.sh`.

**Full Review:** Triggered **before commit**, **when changing or merging repos**, quarterly, after integration/onboarding, when plan or docs have drifted, or on demand. Run `./scripts/run-full-review.sh` then **complete the mandatory checklist** in `docs/audits/full-review-summary.md`: derivative effects and emulation sources for every change; Comprehensive Update; refined entry-point instructions (MASTER_INDEX, constitution, QUICK_AND_FULL_REVIEW, COMPREHENSIVE_DEVELOPER_PRINCIPLES, SOURCES_AND_EMULATION_INDEX). Full Review is not complete until all checklist items are done. Future: scoped (by section/repo/codebase) and cross-system Full Review with evals and constant improvement; the faster the better. See `docs/NEXTTECH_OS_INSTRUCTIONS_FOR_ALL_USERS.md` §1.4 and `docs/QUICK_AND_FULL_REVIEW.md` §3.1, §3.1b, §3.3.

**Knowledge, memory, artifacts, and rules cadence (iron curtain):** **All updates are automated all the time, multi-laterally**, after studying the triggers and mechanisms used by **all LLMs and/or agents combined**. This applies to all automated knowledge, memory, instructed memory, automated artifacts, manual artifacts, and rules of any kind. **Iron curtain:** All platforms, systems, sync, and top-level file changes must **follow suit** and **must not disrupt** this cadence. **No limitations:** We are at the beginning of building our knowledge base, tools, and agents; there are **no limitations** on updates, new creations, artifacts, or any features of any trusted or named bidirectional system (Notion, Linear, GitHub, MCPs, sync flows, etc.). The iron curtain protects _how_ we run, not _what_ we may add or update. See `docs/AGENT_SKILLS_KNOWLEDGE_TOOLS_CADENCE.md`.

**Platform vision (exponential learning & pre-built delivery):** We learn **exponentially** from user queries and will deliver **pre-built agents, artifacts, knowledge, and tools** matched to each user (industry, role, status, preferences), identified by **omni-channel Mac review and organization** (apps, content, tiering), merged into **recommended tech stack and/or dev stack**, **connected instantly** via 1Password, CLI, SDK, master MCP, and funneled to private LLMs. **Automatic consolidation** of all LLM data, applications data, email data, and calendar data (scope expanded by function and by class) is based on predefined workflows and processes for NextTech OS. See `docs/EXPONENTIAL_LEARNING_AND_PREBUILT_DELIVERY.md` and `docs/AUTOMATIC_CONSOLIDATION_NEXTTECH_OS.md`; example/demo grind in progress.

**Core architecture tenets:** The architecture is **modular** and **omni-channel** for **infinite integration capabilities** across core components (AI graph, RAG, knowledge graph, LexVault, company and multi personal life orchestrations). The system ensures **zero platform lock-in** and **offline privacy** via **private LLMs**; **unlimited functionality** via **separate but integrated OpenClaw instances** coupled with **multi human-like agents**, each area **trained and updated by user content intake** across **all channels** and **related multi-channel daily and/or weekly searches**. **Real-time sync of all repos** is a **fundamental architecture feature**: all repos sync on every push from master (sync, push, and/or GitHub Action) so every dev tool and remote see the same state. **Codex and Claude Code are confirmed:** both see the same state when they pull from GitHub. Explained, definable, and clear: `docs/CORE_ARCHITECTURE_TENETS.md` and `docs/REALTIME_SYNC_ALL_REPOS.md`.

---

## OneWish Protocol, Rigid Review, and Improvement

**Protocol:** All architecture plans, core tenets, tools, practices, memory, integrations, syncs, and downstream repos are governed and expanded per the **OneWish Protocol**: `docs/ONEWISH_PROTOCOL.md`. The protocol defines the **product of products** / **systems of systems**, propagation to downstream repos (ROUTES, all_repos), and self-improvement of the protocol under rigid review. The **operational and functioning dimension** is **OneWish Operating System(s)** (OneWish OS); the **logic** layer within it is **OneWish Logic** (protocol, checks, audits). Both are documented in `docs/ONEWISH_LOGIC.md` and apply to all OneWish products, core features (Connected OneWishMCP, Connected Agents.AI), replicated systems, and (when added) OneWish Ollama, Claudebot, Web agents, OpenClaw instances — which may operate independently or together in parts or whole.

**Rigid review:** Every change that touches the protocol scope (architecture, automations, sync, master files, entry points) must pass **rigid review** for **usability** (findable, understandable, actionable for operators and agents), **operability** (runnable, maintainable, recoverable; scripts and paths correct), and **efficiency** (single source of truth, no duplicate or conflicting definitions, token- and step-efficient). Rigid review is part of Full Review and of the protocol; document the result when merging or propagating such changes.

**Improvement:** The **constant improvement loop** is formally named **improvement**. Improvement is the recurring process of review (before/after phases, quarterly, when integrating from other repos), capture (postmortem on failure, patterns-that-work on success, lessons at session end), update (master files, constitution, protocol, entry-point instructions), and propagate (sync to all repos, route governance). Improvement is informed by top LLM repos, dev docs, and tools (`docs/SOURCES_AND_EMULATION_INDEX.md`, `docs/SOURCES_REVIEWED.md`, `docs/BEST_PRACTICES_FROM_TOP_REPOS_TO_ADD_OR_EMULATE.md`). Each Full Review and each change to the protocol scope should reference at least one emulation source. Triggers and cadence are defined in `docs/ONEWISH_PROTOCOL.md` §3.

**Continuous expand, improve, review, audit (at each turn):** Top-level (OneWish OS) and downstream (waterfall) — all systems, repos, logic, workflows, MCPs, core features — are **continuously expanded upon, improved, reviewed, and audited at each turn**. Each turn (phase, commit, sync, new capability, or audit cycle) is an opportunity to expand, improve, review, and audit; no turn is skipped for the scope that changed.

**Downstream repos:** Downstream repos are defined and expanded per the protocol (listed in `config/repos.yaml` ROUTES and all_repos; canonical status in `docs/CONSOLIDATION_AND_REPO_STATUS.md`). When adding or changing downstream repos, follow master-files review-before-action and rigid review (usability, operability, efficiency).

**Never-miss propagation:** Protocol data and master files must flow to all dev tools, MCPs, APIs, workflows, downstream and adjacent repos, agents, and (when added) OneWish Ollama, Claudebot, Web agents, OpenClaw instances — with no target missed. Every **sub-repo**, **agent**, **orchestrated repo**, **orchestrated agent**, **workflow logic**, and **orchestrated workflow logic entity** runs and is governed by **full OneWish OS** (all logic, functionality, components, systems, architecture, best practices, edge cases as expanded). The **never-miss method** (protocol §5) — checklist, triggers, verification — ensures OneWish OS is applied everywhere and no such target is skipped. Run route-constitution and sync-all-repos-and-review per triggers; complete Full Review mandatory checklist so entry points and tools stay aligned.

**Special projects:** Commands or queries designated as special projects must read the protocol first and use the protocol’s methods/tools list and best practices (top repos, standards, emulated projects); see `docs/ONEWISH_PROTOCOL.md` §6 and `docs/SPECIAL_PROJECTS_AND_METHODS.md`.

---

## 8. Integration of OneWish OS into all dev tools and component repositories

OneWish OS is **code through architecture** and a **system of systems**. All instructions, governance, and sync flows must integrate into **every dev tool** and propagate **down to all component repositories**, **NextTech OS**, **agents**, **systems**, and **Connected Agents.AI**. Integration, syncing, updating, and pushing of all related activities follow the rules below.

### 8.1 Dev tools (where instructions live)

**Same level:** Every dev tool in the canonical list is **on the same level**. There is no hierarchy or “first-class vs optional” for governance: each receives the **same** constitution and governance, the **same** entry-point and audit treatment, and the **same** ability to run any OneWish OS script from its terminal (see §8.5). When a tool is “not in use,” it is still in the list and still verified on every audit (document “Not in use”); when in use, it gets the same integration (constitution ref, entry point, sync path) as every other tool. Canonical list: `docs/DEV_TOOLS_CANONICAL_LIST_AND_AUDIT.md` §1 — all 9 tools; never omit one.

| Dev tool                 | Entry points                                                            | How OneWish OS instructions apply                                                                          |
| ------------------------ | ----------------------------------------------------------------------- | ---------------------------------------------------------------------------------------------------------- |
| **Cursor**               | AGENTS.md, .cursor/rules/\*.mdc                                         | Read first; master-project-rules and path-scoped rules reference constitution, MASTER_INDEX, protocol.     |
| **Claude Code**          | CLAUDE.md, .claude/                                                     | Project and user memory; references constitution, MASTER_INDEX, sync flows.                                |
| **GitHub / Copilot**     | AGENTS.md, .github/agents/my-agent.agent.md                             | Agent spec references constitution, protocol, vendor inventory.                                            |
| **Codex**                | .codex/config.toml; project CLAUDE.md/AGENTS.md when present            | Same instructions via synced entry points; run from canonical repo (see docs/DEV_TOOLS_REPO_ALIGNMENT.md). |
| **v0 (Vercel)**          | docs/V0_SETUP_AND_INSTRUCTIONS.md                                       | Custom Instructions and rules for litigation UI (2000 char max).                                           |
| **VS Code / Extensions** | .vscode/extensions.json; docs/VSCODE_EXTENSIONS\*, DEVELOPER_FOUNDATION | Same governance; extensions and recommendations per docs.                                                  |
| **Windsurf**             | docs/archives/.../windsurf.md (when in use)                             | When in use: config and entry point documented; constitution ref; same level as above.                     |
| **Warp**                 | docs/archives/.../warp.md (when in use)                                 | When in use: config and entry point documented; constitution ref; same level as above.                     |
| **Goose**                | docs/GOOSE_SETUP_AND_INTEGRATION.md; platform-connections               | When in use: GOOSE_API_KEY, verify-all-connections; constitution ref; same level as above.                 |

**Rule:** Every dev tool in the canonical list (see `docs/DEV_TOOLS_CANONICAL_LIST_AND_AUDIT.md`) receives the same governance and entry-point instructions via **route-constitution** (ROUTES) and **sync-all-repos-and-review** (all_repos). Refined instructions (AGENTS.md, CLAUDE.md, UNIVERSAL_INSTRUCTIONS, my-agent.agent.md, .cursor/rules) are updated in Full Review so they reference and require reading MASTER_INDEX, constitution, QUICK_AND_FULL_REVIEW, and SOURCES_AND_EMULATION_INDEX.

### 8.2 Component repositories (propagation down)

- **Source of truth:** `config/repos.yaml` — **ROUTES** (receive constitution, checklist, universal, bootstrap via `route-constitution-to-repos.sh`) and **all_repos** (receive full sync via `sync-all-repos-and-review.sh`).
- **Canonical map:** `docs/CONSOLIDATION_AND_REPO_STATUS.md` — which repos are canonical, merged, archived.
- **Flow:** Master → ROUTES (governance only) and Master → all_repos (full sync: SUPER_DEVELOPER_PRINCIPLES, MASTER_INDEX, agent spec, skills, config, docs). Child repos and **Connected Agents.AI** modules (LitigationForce.AI, file-management-toolkit, powerconnectionaiapplications, slack-agent-template, etc.) receive the same OneWish OS instructions and updates.
- **Bidirectional:** When a component repo contributes back (common code, improvements), document in CONSOLIDATION_AND_REPO_STATUS; merge to master; then run route + sync so updated master flows to all targets.

### 8.3 NextTech OS, agents, systems, Connected Agents.AI

- **NextTech OS** is the user-facing instance of this repo; it runs the same Full Review, sync, and never-miss propagation as the master.
- **Agents** (orchestrator, specialists, workflow agents) are governed by full OneWish OS; they receive protocol data and master files via entry points and sync. Agent spec: `.github/agents/my-agent.agent.md`.
- **Systems** (Connected OneWishMCP, LitigationForce.AI, Power Connecting, LexVault, knowledge graph; planned: OneWish Ollama, Claudebot, Web agents, OpenClaw) operate as part of the **system of systems**; each is in propagation targets when it has a repo or config entry.
- **Connected Agents.AI** is the product identity; all its modules and repos are in ROUTES or all_repos and receive integration, sync, update, and push per never-miss (§5 in protocol).

### 8.4 Syncing, updating, pushing (related activities)

| Activity                | Script / trigger                                | Targets                                                     |
| ----------------------- | ----------------------------------------------- | ----------------------------------------------------------- |
| **Route governance**    | `./scripts/route-constitution-to-repos.sh`      | ROUTES (constitution, checklist, universal, bootstrap)      |
| **Full sync**           | `./scripts/sync-all-repos-and-review.sh`        | all_repos (master files, agent spec, skills, docs)          |
| **Full Review**         | `./scripts/run-full-review.sh`                  | Mandatory checklist; refined entry-point instructions       |
| **Dev-tools workspace** | `./scripts/sync-dev-tools-repos-from-config.sh` | onewish-repos.code-workspace; Claude Code / Codex alignment |
| **Never-miss**          | Protocol §5 checklist                           | All dev tools, ROUTES, all_repos, MCPs, agents, workflows   |

Triggers: governance change → route; master files or repo list change → sync; before commit → Full Review + checklist; quarterly → full pass. See `docs/ONEWISH_PROTOCOL.md` §5 and `docs/reports/ONEWISH_REPO_ARCHITECTURE_AND_HOW_IT_WORKS.md`.

### 8.5 Cross-tool execution and full inventory (dev tools, APIs, SDKs, IDEs, repos, agents, connectors, MCPs)

**Cross-tool execution:** Every **dev tool** connected to OneWish OS may **run any other connected dev tool or OneWish OS script** from within that tool. There is no hierarchy that blocks one IDE from invoking another or from running the same scripts (route-constitution, sync-all-repos, Full Review, comprehensive eval, audit runbook). Execution is via **terminal, CLI, or script** from the currently active dev tool (Cursor, Claude Code, Codex, etc.); the master repo path and workspace are the same, so any connected tool can run `./scripts/run-audit-runbook.sh`, `./scripts/run-comprehensive-eval-and-cleanup.sh`, or any other script. **Rule:** From any connected dev tool, open the master repo (or `onewish-repos.code-workspace`), then run the desired script in the terminal; no tool is “only” runnable from one other tool.

**Full inventory:** All **dev tools**, **APIs**, **SDKs**, **IDEs**, **repos**, **agents**, **connectors**, and **MCPs** that are part of OneWish OS must be **listed** in the canonical sources and **connected and configured** per OneWish OS. Single reference: `docs/ONEWISHOS_CROSS_TOOL_AND_FULL_INVENTORY.md`.

**Constitution for connectors/MCPs:** Only tools in the **canonical registry** (`config/canonical-mcp-connectors.yaml`) are approved; no tool is added to platform-connections, MCP configs, or prebuilt-agent lists unless it is in the canonical registry. When adding a tool: add to canonical only → run sync → set up and configure across all relevant tools via OneWish OS (`connect-and-configure-onewishos.sh`) → **never miss** every target → **always review** (Full Review checklist). See `docs/MCP_CONNECTOR_SYNC_AND_TRIGGER.md`. **Game changers** (platform-defining features, including OneWish OS and full ingestion + one-button orchestration): `docs/GAME_CHANGERS.md`. — which lists where each category lives (config/repos.yaml, config/platform-connections.yaml, config/connectors.yaml, config/canonical-mcp-connectors.yaml, docs/DEV_TOOLS_CANONICAL_LIST_AND_AUDIT.md, docs/MASTER_MCP_CONNECTORS_APIS.md) and which scripts connect and configure them. Nothing is “implicit”; new additions are added to the appropriate config or doc and then sync/connect scripts are run.

**Connect and configure:** Scripts that connect and configure all listed entities to OneWish OS are documented in `docs/ONEWISHOS_CROSS_TOOL_AND_FULL_INVENTORY.md` and in `./scripts/connect-and-configure-onewishos.sh` (runs route-constitution, sync-all-repos, sync-dev-tools, verify-all-connections optional, run-full-review). Run after adding a new repo, dev tool, MCP, or connector so the system stays fully integrated.

**Architecture and methods:** Whether OneWish OS uses the best architecture, sorting, and organizational methods—and what set of best practices, computer science, LLMs, dev tools, systems-of-systems, and architecture-as-code we align to—is clarified in **`docs/ONEWISHOS_ARCHITECTURE_AND_METHODS.md`**. In short: we align to leading methods (12-Factor, Production-Grade Agentic AI, MCP best practices, TRiSM, ABA/EDRM/Sedona, etc.); we use best-practical architecture and single-source-of-truth, canonical lists, route/sync, no-fail audit; we iterate on a set cadence and document gaps. “Best” here means best **practical** and explicitly traceable to those sources.

---

## Cloud & Inference (Google Cloud / Gemini / Vertex AI)

Inference and cloud operations default to **Google Cloud**, **Gemini API**, and **Vertex AI** where applicable:

- **Gemini API**: `GOOGLE_API_KEY` — direct LLM calls (ai.google.dev)
- **Vertex AI**: `GOOGLE_APPLICATION_CREDENTIALS` + `GOOGLE_CLOUD_PROJECT` — enterprise Gemini, embeddings, document processing
- **Google Cloud**: Storage, Document AI, BigQuery — governed by `config/connectors.yaml`

See `config/connectors.yaml`, `docs/PLATFORMS_1PASSWORD_MAPPING.md`, `docs/LAUNCH_AI_TOOLS_WITH_1PASSWORD.md`.

**Platform audit**: Run `./scripts/audit-1password-for-integrations.sh` and consult `docs/PLATFORM_INTEGRATION_AUDIT.md` for 1Password items, subscriptions, and integration targets.

**Master MCP, connectors & APIs**: See `docs/MASTER_MCP_CONNECTORS_APIS.md` for the complete inventory of Claude, Claude Code, ChatGPT, Perplexity, Genspark, Zoom, Neo4j, Docker, Attio, Airtable, Brave, DuckDuckGo, and all MCP servers and connectors.

**Vault organization**: DevOps-first taxonomy, rules, and sync — `docs/1PASSWORD_VAULT_ORGANIZATION.md`, `./scripts/1password-organize-vaults.sh`.

---

## Entity-Specific Operational Knowledge

**Tejas Environmental** (environmental services, SWD, oil recovery optimization):

- **Workbook breakout**: Master Excel split into 5 workbooks for context-window optimization. Location: `~/Desktop/Tejas Environmental Workbooks/`. Skill: `~/.cursor/skills/tejas-environmental-workbooks/SKILL.md`. Cross-links: CRM VLOOKUPs → Revenue (Consolidated); Valuation pulls JV-BL from JV & Growth.
- **Roadmap**: `docs/archives/projects-archives/docs/roadmaps/tejas-environmental.md`
- **Datasite**: `~/Desktop/1TEJAS.TRISUN.Datasite_*/` — CRM SORT.xlsx, financials, customers
- **Entity cluster**: Tejas Environmental Solutions Inc. (TES), Nexus Envirotech, Breakwater Environmental; Brand Davis (operations)

---

## Ontology, Lists & Connections

When creating ontology schemas, lists, to-dos, projects, or entity names and connections, follow the Cursor skills:

- **Ontology / schema / syntax**: `.cursor/skills/ontology-schema-syntax/SKILL.md`
- **Lists / to-dos / projects**: `.cursor/skills/lists-todos-projects/SKILL.md`
- **Names and connections**: `.cursor/skills/names-and-connections/SKILL.md`

---

## 9. Changelog (Constitution Versions)

| Version | Date    | Summary                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                 |
| ------- | ------- | --------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| 1.0     | 2026-02 | Initial constitution: human-in-loop, claim typing, audit, bias/safety, simulation disclaimer, new capability flow                                                                                                                                                                                                                                                                                                                                                                                                                                                                       |
| 1.1     | 2026-02 | Added §7 changelog; expert docs references; virtuous loop; quarterly sources review                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                     |
| 1.2     | 2026-02 | Added Tejas Environmental operational knowledge (§ Entity-Specific)                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                     |
| 1.3     | 2026-02 | Added OneWish Protocol, rigid review (usability, operability, efficiency), and improvement (constant improvement loop); downstream repos per protocol                                                                                                                                                                                                                                                                                                                                                                                                                                   |
| 1.4     | 2026-02 | Never-miss propagation of protocol and master files to all dev tools, MCPs, APIs, workflows, repos, agents (§5); Special projects (§6) with methods/tools list and best practices                                                                                                                                                                                                                                                                                                                                                                                                       |
| 1.5     | 2026-02 | §6 Actions (Execution): always take actions through SDKs, IDEs, CLIs, and/or terminal; renumbered New Capabilities to §7, Changelog to §8                                                                                                                                                                                                                                                                                                                                                                                                                                               |
| 1.6     | 2026-02 | §6: default = agents execute (terminal/SDKs/IDEs/CLIs), not user. §8 Integration of OneWish OS into all dev tools and component repos (dev tools, component repos, NextTech OS/agents/systems/Connected Agents.AI, sync/update/push). Changelog → §9                                                                                                                                                                                                                                                                                                                                    |
| 1.7     | 2026-02 | §8.5 Cross-tool execution (any connected dev tool may run any other / any OneWish OS script); full inventory (dev tools, APIs, SDKs, IDEs, repos, agents, connectors, MCPs) listed and connect/configure scripts; ONEWISHOS_CROSS_TOOL_AND_FULL_INVENTORY.md; connect-and-configure-onewishos.sh                                                                                                                                                                                                                                                                                        |
| 1.8     | 2026-02 | §8.1 Same level: all 9 dev tools on the same level (no hierarchy); table expanded to Cursor, Claude Code, Copilot, Codex, v0, VS Code/Extensions, Windsurf, Warp, Goose; DEV_TOOLS_CANONICAL §2 and DEV_TOOLS_RULES_SETUP updated with same-level principle and all 9.                                                                                                                                                                                                                                                                                                                  |
| 1.9     | 2026-02 | §8 Architecture and methods: pointer to ONEWISHOS_ARCHITECTURE_AND_METHODS.md — clarifies best architecture/sorting/organization and leading methods we align to (best-practical, iterate, document gaps).                                                                                                                                                                                                                                                                                                                                                                              |
| 1.10    | 2026-02 | §6.5 Automated recursive virtuous learning; harnessed complexity: system is automated, recursive, virtuous (lean learning, expanding, spawning, integrating, learning, tools use); complexity harnessed by detailed scientifically founded instructions, rules, sequences, connections, MCPs; at each stage always provide example of outcome and derivative outcomes and chart or graph so evolution is controlled, understood, and perfected. Refs: FRAMEWORK_AUDITS_REVIEWS_INTEGRATIONS_BY_STAGE, QUICK_AND_FULL_REVIEW, audits/artifacts/README, LIFECYCLE_STAGES_AND_CHECKPOINTS. |

---

_Referenced by: AGENTS.md, CLAUDE.md, .github/agents/my-agent.agent.md_
