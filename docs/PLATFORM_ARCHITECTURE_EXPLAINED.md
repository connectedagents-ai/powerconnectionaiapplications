# Platform Architecture Explained — Master Repo, All Repos, Connections & Vocabulary

> **Purpose**: Natural-language explanation of the master repo and every child repo, how they connect, what needs defining/merging/sorting for a perfect consolidated setup, and a clear vocabulary for architecture, structure, workflows, master files, and automations.
>
> **Read this** when you need to onboard, explain the system to others, or plan consolidation work.

---

## Part 1: The Master Repo — CURSOR CLOUD AGENTS

**Location**: `~/.cursor/CURSOR CLOUD AGENTS` (or `CURSOR-CLOUD-AGENTS` on GitHub as `connectedagents-ai/CURSOR-CLOUD-AGENTS`)

**What it is**: The **platform source of truth** and **governance hub** for all Connected Agents.AI repos. It is not a typical application repo—it is a **meta-repository** that holds:

1. **Non-negotiable principles** (constitution) that every agent and output must follow
2. **Reference patterns** (LexVault for evidence, ontology for entities) that child repos emulate
3. **Sync and routing scripts** that propagate governance to child repos
4. **LitigationForce.AI production code** — the replit-app (33 Replit agents), cases (Tesla, Mullins, Winchill), 18 Cursor subagents, 11 Claude Code workers, config for 5-phase pipeline, 8 schemas, intelligence engine, expert marketplace, etc.
5. **Agent specifications** — RICO agent (1,303 lines), playbooks, blackbox agents, MCP servers

**In plain language**: Think of it as the "brain and rulebook" of the whole platform. When someone creates a new tool, agent, or capability, they read the constitution here first. When child repos need updated rules, the master repo pushes them out via sync scripts. The master repo _also_ contains the full LitigationForce.AI application (replit-app, cases, scripts), so it doubles as both governance hub and the primary litigation product repo.

**Key subdirectories**:

- `docs/` — Constitution, UNIVERSAL_INSTRUCTIONS, SUPER_DEVELOPER_PRINCIPLES, architecture, schemas, modules (LexVault, ontology, voice, litigation-swarm-ui)
- `scripts/` — route-constitution-to-repos.sh, sync-all-repos-and-review.sh, verify-routing, blackbox_client, onboard_client, run_pipeline, etc.
- `config/` — production-pipeline.yaml, playbooks.yaml, blackbox-agents.yaml, connectors.yaml, mcp-servers/
- `agents/` — RICO agent, master index, claude-code-build (workers, skills, tools)
- `cases/` — Tesla (primary), Mullins, Winchill
- `replit-app/` — Deployed app (33 agents, intelligence, marketplace, ontology, scrapers)
- `.cursor/rules/` and `.cursor/skills/` — Cursor-specific governance and skills
- `.github/agents/` — GitHub Copilot agent spec (my-agent.agent.md)

---

## Part 2: Child Repos — What Each Is and How It Connects

### 2.1 connected-agents-platform

**Location**: `~/Documents/connected-agents-platform`  
**GitHub**: `connectedagents-ai/connected-agents-platform`  
**Receives from master**: Constitution → `agents/constitution.md`, checklist, universal → `agents/`, bootstrap → `.cursor/rules/platform-bootstrap.mdc`, plus SUPER_DEVELOPER_PRINCIPLES, SOURCES_REVIEWED, modules, REFERENCE_PATTERNS, expert docs, etc.

**What it is**: The **platform core** — the universal operating system for agent-powered businesses. It holds:

- **Shared ontology** (`ontology/core.yaml`, business.yaml) — primitives and business entities used across all verticals
- **Universal modules** — operations, finance, people, sales-crm, marketing, legal-compliance, engineering, data-ai, executive
- **Platform agents** — constitution, personas, evaluators, digital twin architecture
- **Economics** — value tracking, cost comparison, ROI schemas and dashboards
- **Voice framework** — universal commands, personalities, channels (phone, desktop, car)
- **MCP framework** — permission model, server configs, marketplace
- **Marketing** — voice-agent config, Next.js marketing app (voice-app)
- **Verticals** — litigation/ links to CURSOR-CLOUD-AGENTS; energy, real-estate, finance are future
- **Onboarding** — 10-step pipeline, discovery agents

**Connection**: The master repo (CURSOR CLOUD AGENTS) is the _litigation vertical_ built on top of this platform. The platform provides primitives; the master repo adds litigation-specific agents, schemas, and case data. The platform's `verticals/litigation/` links back to CURSOR-CLOUD-AGENTS.

---

### 2.2 LitigationForce.AI

**Location**: `~/Documents/LitigationForce-Parent/01-Litigation-Core/LitigationForce.AI`  
**GitHub**: Originally `Connected-Energy-AI/LitigationForce.AI`; now under `connectedagents-ai`  
**Receives from master**: Constitution → `docs/constitution.md`, checklist, universal → `docs/`, bootstrap → `.cursor/rules/platform-bootstrap.mdc`, plus all synced docs and rules.

**What it is**: The **ADK-based litigation agent framework** — social media scrapers (Twitter, LinkedIn, Facebook, YouTube, Instagram, websites), Neo4j graph integration, Claude analysis, investigative workflows. Built on Google's Agent Development Kit (ADK). Contains:

- **Scrapers** — Single and multi-platform; profile, posts, connections, search
- **Agents** — ScraperAgent, MultiPlatformScraperAgent, NetworkAnalysisAgent, ContentAnalysisAgent, SentimentAnalysisAgent, SocialEvaluationAgent, RiskAssessmentAgent, InfluenceAnalysisAgent, InvestigationAgent, ClaudeAnalysisAgent
- **Graph analysis** — Neo4j for profile storage, centrality, community detection, path finding, cross-platform identity linking
- **Pydantic models** — litigation entities
- **MCP server** — integration with master repo's mcp-router pattern
- **Ontology** — W3C OWL 2–aligned
- **Large-scale doc processing** — 500k+ page litigation document swarms

**Connection**: This is the _ADK implementation_ of litigation intelligence. The master repo holds the _production_ LitigationForce (replit-app, Blackbox Cloud agents, cases). LitigationForce.AI is the ADK/scraper/graph layer that can feed into or run alongside the master repo's pipeline. There is overlap and potential consolidation—see REPO_SIMILARITY_AND_MERGE_PLAN.

---

### 2.3 file-management-toolkit

**Location**: `~/file-management-toolkit`  
**GitHub**: `connectedagents-ai/file-management-toolkit`  
**Receives from master**: Constitution → `docs/constitution.md`, checklist, universal, bootstrap, plus all synced docs.

**What it is**: A **standalone desktop and cloud file toolkit** — desktop cleanup, cloud deduplication, AI-powered file organization. Scripts **move** files (never delete); use dated folders for undo. Contains:

- **Desktop Janitor** — Organize loose Desktop files by type into `_Cleanup_YYYY-MM-DD/Category/`
- **AI File Clerk** — GPT-4o vision + text; rename to `YYYY-MM-DD_Entity_Type.ext`, move to `~/Documents/01_Projects/Filed`, log to JSON
- **Cloud dedup** — rclone-based; mount remotes, build indexes, find duplicates across Google Drive, Box, OneDrive
- **OneDrive path fix** — Fix deeply nested path errors (run once)
- **Config** — file_clerk_config.yaml

**Connection**: Shared constitution and governance. Used for evidence preparation, client onboarding file discovery, and general file ops. Emulates AI clerk patterns; references constitution for human-in-the-loop on AI outputs.

---

### 2.4 slack-agent-template

**Location**: `~/.cursor/bootstrap-work/slack-agent-template`  
**GitHub**: `connectedagents-ai/slack-agent-template` (merged from slack-agent-template2, slackagent)  
**Receives from master**: Same governance as other child repos; in ALL_REPOS for sync.

**What it is**: A **Slack Agent template** — Nitro server, Bolt for JavaScript (TypeScript), Workflow DevKit DurableAgent, AI SDK, Vercel AI Gateway. Features:

- Human-in-the-loop approval workflows (e.g., joining channels)
- Pre-configured tools (read channels, threads, join channels with approval, search)
- Slack Assistant API for threaded conversations, real-time streaming
- Deploy to Vercel

**Connection**: Template for new Slack bots and agent-based Slack apps. Bootstrap on clone; when cloned locally, receives full sync. Used as reference pattern for "new Slack agents."

---

### 2.5 powerconnectionaiapplications

**Location**: `~/Documents/powerconnectionaiapplications`  
**GitHub**: `connectedagents-ai/powerconnectionaiapplications`  
**Receives from master**: Constitution → `docs/constitution.md`, checklist, universal, bootstrap, plus all synced docs. README is minimal (62 chars).

**What it is**: The **PowerConnection AI applications** repo — vertical for powerconnection.ai. Currently sparse: AGENTS.md, CLAUDE.md, docs/, .cursor/, lessons.md, patterns-that-work.md. Pending merges from powerconnectionai, powerconnectionodoo, spark-insight-chooser per REPO_SIMILARITY_AND_MERGE_PLAN.

**Connection**: Receives governance. Will hold PowerConnection-specific apps once merged. Related nextjs-ai-chatbot variants (powerconnection.ai chat) may merge here as config/branch.

---

### 2.6 replit-app (Inside Master Repo)

**Location**: `CURSOR CLOUD AGENTS/replit-app/` (subdirectory of master)  
**Not a separate repo** — lives inside the master repo. Deployed to Replit (SwarmRICO, Verital-Legal-Tech).

**What it is**: The **deployed LitigationForce application** — 33 Replit agents, intelligence engine (8-channel search, persona evaluator, financial modeler), expert marketplace (tri-verified, biometric, bond), ontology (5,351 lines), Neo4j graph client, scrapers, orchestration. Has its own CLAUDE.md, agents/, examples/, src/, tests/.

**Connection**: Receives constitution and docs when master is updated. Not in ROUTES as a separate repo—it _is_ part of the master repo. Sync applies to master; replit-app inherits.

---

## Part 3: How They All Connect

### Data Flow (Conceptual)

```
                    ┌─────────────────────────────────────────┐
                    │     CURSOR CLOUD AGENTS (Master)        │
                    │  Constitution, rules, schemas, replit-app│
                    └─────────────────┬───────────────────────┘
                                      │
         route-constitution-to-repos.sh + sync-all-repos-and-review.sh
                                      │
     ┌────────────────────────────────┼────────────────────────────────┐
     │                                │                                │
     ▼                                ▼                                ▼
┌─────────────┐              ┌──────────────┐              ┌──────────────────────┐
│ connected-  │              │ Litigation   │              │ file-management-     │
│ agents-     │              │ Force.AI     │              │ toolkit              │
│ platform    │              │ (ADK)        │              │                      │
└──────┬──────┘              └──────┬───────┘              └──────────┬───────────┘
       │                            │                                 │
       │  Provides: ontology,       │  Provides: scrapers,             │  Provides:
       │  modules, voice, MCP       │  graph, ADK agents               │  file ops,
       │                            │                                 │  AI clerk
       └────────────────────────────┴─────────────────────────────────┘
                                      │
                                      ▼
                    ┌─────────────────────────────────────────┐
                    │  shared governance: constitution,        │
                    │  claim typing, human-in-loop, audit      │
                    └─────────────────────────────────────────┘
```

### Sync Mechanism

1. **route-constitution-to-repos.sh** — Copies constitution.md, NEW_CAPABILITY_CHECKLIST, UNIVERSAL_INSTRUCTIONS, platform-bootstrap.mdc to ROUTES (4 repos with local paths).
2. **sync-all-repos-and-review.sh** — Does all of the above plus: SUPER_DEVELOPER_PRINCIPLES, SOURCES_REVIEWED, docs/modules/, REFERENCE_PATTERNS, SOURCES_AND_EMULATION_INDEX, PRE_EXECUTION_CHECKLIST, expert docs, AGENT_ORCHESTRATION_BEST_PRACTICES, my-agent.agent.md, master-orchestrator.md, bootstrap (developer-enhancement, agent-efficiency), AGENTS.md/CLAUDE.md bootstrap. Runs on ALL_REPOS (master + 5 child repos).
3. **Pre-push hook** — When constitution, routing config, modules, SOURCES, PRE_EXECUTION_CHECKLIST change, prompts running full sync.
4. **GitHub Actions** — verify-routing.yml, verify-connections.yml on PR.

---

## Part 4: What Needs to Be Defined, Merged, Sorted for a Perfect Repo

### 4.1 Definition Gaps

| Gap                                          | Current State                                | Needed                                                                                                                                                        |
| -------------------------------------------- | -------------------------------------------- | ------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| **PowerConnection README**                   | 62 chars, no structure                       | Full README: purpose, structure, how it connects, deploy steps                                                                                                |
| **LitigationForce.AI vs Master**             | Both have litigation; overlap unclear        | Single source of truth: ADK (LF.AI) vs production (master replit-app). Define: "LitigationForce.AI = ADK/scrapers; master replit-app = deployed app" or merge |
| **nextjs-ai-chatbot**                        | GitHub-only, not in ROUTES                   | Add to REFERENCE_PATTERNS; define when to clone; optionally add to sync when cloned                                                                           |
| **adk-python**                               | GitHub-only                                  | Document as reference for agent patterns; no local clone needed                                                                                               |
| **connected-agent-ai, Connectedagentsrepo1** | Pending merge into connected-agents-platform | Define: merge or archive; update CONSOLIDATION                                                                                                                |

### 4.2 Merge Actions (from REPO_SIMILARITY_AND_MERGE_PLAN)

| Cluster                    | Repos   | Action                                                                                                                                                                                                        | Status  |
| -------------------------- | ------- | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | ------- |
| **LitigationForce family** | 9 repos | Merge litforce-ai-gateway, litigationagentsmultimodalchat into LitigationForce.AI; archive litigatioinagents.ai, LITIGATION-AGENTS---7-26-2025, Litigation-Force-Interactive-Presentation, case-commander-pro | Pending |
| **Next.js AI chatbot**     | 5 repos | Merge into nextjs-ai-chatbot with env configs (POWERCONNECTION, LITIGATIONFORCE)                                                                                                                              | Pending |
| **PowerConnection**        | 5 repos | Merge powerconnectionai, powerconnectionodoo, spark-insight-chooser into powerconnectionaiapplications                                                                                                        | Pending |
| **Slack agents**           | 3       | Merged (template2, slackagent → slack-agent-template)                                                                                                                                                         | Done    |
| **Vercel AI demos**        | 8 repos | Create vercel-ai-demos monorepo or archive                                                                                                                                                                    | Pending |
| **connected-agent**        | 3       | Merge connected-agent-ai, Connectedagentsrepo1 into connected-agents-platform                                                                                                                                 | Pending |
| **AI SDK starters**        | 3       | Merge litforce/deepinfra variants into ai-sdk-starter-xai                                                                                                                                                     | Pending |
| **Powermed**               | 2       | Merge design variant into Powermed-Marketing                                                                                                                                                                  | Pending |
| **InfraNodus**             | 2       | Delete 2infranodus-obsidian-plugin (duplicate)                                                                                                                                                                | Pending |
| **Low-value**              | ~15     | Archive demo-repository, ubiquitous-octo-dollop, skills-introduction-to-github, Cursor-Project-1, etc.                                                                                                        | Pending |

### 4.3 Sorting and Organization

| Item                          | Action                                                                                                                               |
| ----------------------------- | ------------------------------------------------------------------------------------------------------------------------------------ |
| **connectedenergyai**         | Transfer blocked (GitHub Enterprise). Manual: clone → push to connectedagents-ai → delete source                                     |
| **ROUTES vs ALL_REPOS**       | Keep in sync. Add powerconnectionaiapplications to both when cloned (already in both). Add nextjs-ai-chatbot when cloned.            |
| **replit-app**                | Clearly document: subdirectory of master, not separate repo. Receives via master sync.                                               |
| **Document Reference Matrix** | Ensure all new expert docs (EXPERT_PROMPT_ENGINEERING, LIFECYCLE_STAGES, AGENT_ORCHESTRATION_BEST_PRACTICES) are in CONSOLIDATION §8 |

### 4.4 Vocabulary Standardization

See Part 5.

---

## Part 5: Clear Vocabulary — Architecture, Structure, Workflows, Master Files, Automations

### 5.1 Architecture Terms

| Term                  | Definition                                                                                                           | Example                                                                      |
| --------------------- | -------------------------------------------------------------------------------------------------------------------- | ---------------------------------------------------------------------------- |
| **Master repo**       | CURSOR CLOUD AGENTS. Governance hub + LitigationForce production. Source of constitution, rules, reference patterns. | `~/.cursor/CURSOR CLOUD AGENTS`                                              |
| **Child repo**        | Repo that receives governance via route-constitution and sync-all-repos.                                             | connected-agents-platform, LitigationForce.AI, file-management-toolkit, etc. |
| **Platform core**     | connected-agents-platform. Universal ontology, modules, voice, MCP, economics.                                       | Shared across all verticals                                                  |
| **Vertical**          | Product-specific layer (litigation, energy, real-estate). Built on platform core.                                    | LitigationForce, PowerConnection, (future) EnergyForce                       |
| **Route target**      | Repo in ROUTES (route-constitution-to-repos.sh). Receives constitution, checklist, universal, bootstrap.             | 4 repos with local paths                                                     |
| **ALL_REPOS**         | List in sync-all-repos-and-review.sh. Receives full sync (principles, modules, agent instructions, bootstrap).       | Master + 5 child repos                                                       |
| **Reference pattern** | Module spec (LexVault, ontology, voice, litigation-swarm-ui) or example repo that new repos emulate.                 | docs/modules/lexvault.md                                                     |
| **Schema-first**      | Data contracts defined in docs/schemas/ before implementation.                                                       | Evidence, Claim, Timeline, Bundle                                            |
| **Router-first MCP**  | Progressive discovery: small router tool set → fetch schema on demand → execute.                                     | docs/mcp-router.md                                                           |
| **One evidence base** | Single corpus feeds all litigation tracks (CA, TX, Federal RICO).                                                    | cases/Tesla                                                                  |
| **replit-app**        | Deployed LitigationForce app. Subdirectory of master. Not a separate repo.                                           | CURSOR CLOUD AGENTS/replit-app/                                              |

### 5.2 Structure Terms

| Term                       | Definition                                                                                                              | Example                                                       |
| -------------------------- | ----------------------------------------------------------------------------------------------------------------------- | ------------------------------------------------------------- |
| **Constitution**           | Non-negotiable principles: human-in-loop, claim typing, audit, bias/safety, simulation disclaimer, new capability flow. | docs/constitution.md                                          |
| **UNIVERSAL_INSTRUCTIONS** | Tool-agnostic entry point for all AI agents. Points to constitution, checklists, repo status.                           | docs/UNIVERSAL_INSTRUCTIONS.md                                |
| **Master rules**           | .cursor/rules/master-project-rules.mdc. Always-apply Cursor rules.                                                      | Identity, simulation disclaimer, claim typing, evaluator gate |
| **Agent spec**             | .github/agents/my-agent.agent.md. GitHub Copilot + multi-agent roles, vendor inventory.                                 | Standards, provenance, Evaluator Swarm                        |
| **AGENTS.md**              | READ FIRST + manifest for Cursor, Copilot, Claude. In every repo root.                                                  | READ FIRST block, constitution ref                            |
| **CLAUDE.md**              | READ FIRST + guide for Claude Code. In every repo root.                                                                 | Project memory, reference patterns                            |
| **docs/modules/**          | LexVault, ontology, voice-agents, litigation-swarm-ui. Reference specs synced to child repos.                           | File/evidence, entity schemas                                 |
| **config/playbooks.yaml**  | Per-agent prompt templates. Externalized prompt management.                                                             | 12 agent playbooks                                            |
| **config/connectors.yaml** | MCP servers, cloud connectors, API configs.                                                                             | Google Cloud, Gemini, Vertex, Copilot, AWS, Zoom, Box         |
| **Bootstrap**              | platform-bootstrap.mdc. Initial setup rules for new repos.                                                              | .cursor/rules/platform-bootstrap.mdc                          |

### 5.3 Workflow Terms

| Term                        | Definition                                                                                  | Example                                         |
| --------------------------- | ------------------------------------------------------------------------------------------- | ----------------------------------------------- |
| **Sync**                    | Propagate governance and reference artifacts from master to child repos.                    | sync-all-repos-and-review.sh                    |
| **Route**                   | Copy constitution, checklist, universal, bootstrap to ROUTES.                               | route-constitution-to-repos.sh                  |
| **Bootstrap (verb)**        | Create AGENTS.md, CLAUDE.md in repos missing them. Run at start of sync.                    | bootstrap-child-agents-claude.sh                |
| **All-repo review**         | Protocol: run sync --review; check architecture, workflows, constitution, MCP, principles.  | docs/ALL_REPO_REVIEW.md                         |
| **Virtuous loop**           | Failure→postmortem; Success→patterns-that-work; Session→lessons; New waste→anti-pattern.    | SOURCES_AND_EMULATION_INDEX                     |
| **Pre-execution checklist** | 22 categories, 110+ checks before acting.                                                   | docs/SUPER_DEVELOPER_PRE_EXECUTION_CHECKLIST.md |
| **Evaluator Swarm**         | 4-gate QA: Fact Checker, Citation Validator, Logic Auditor, Ethics Reviewer. All must pass. | constitution §2                                 |
| **Human checkpoint**        | Mandatory attorney review for high-stakes outputs.                                          | Privilege, filings, productions, damages        |

### 5.4 Master Files (Canonical Sources)

| File                                            | Purpose                             | Propagates To          |
| ----------------------------------------------- | ----------------------------------- | ---------------------- |
| docs/constitution.md                            | Non-negotiable principles           | All repos via route    |
| docs/UNIVERSAL_INSTRUCTIONS.md                  | Tool-agnostic bootstrap             | All repos via route    |
| docs/NEW_CAPABILITY_CHECKLIST.md                | New tool/agent/skill flow           | All repos via route    |
| .cursor/rules/platform-bootstrap.mdc            | Bootstrap rules                     | All repos via route    |
| docs/SUPER_DEVELOPER_PRINCIPLES.md              | Super developer principles          | All repos via sync     |
| docs/SOURCES_REVIEWED.md                        | LLM/repo best practices             | All repos via sync     |
| docs/SOURCES_AND_EMULATION_INDEX.md             | Top sources per action              | All repos via sync     |
| docs/SUPER_DEVELOPER_PRE_EXECUTION_CHECKLIST.md | Pre-exec checks                     | All repos via sync     |
| docs/modules/\*.md                              | LexVault, ontology, voice, swarm-ui | All repos via sync     |
| docs/REFERENCE_PATTERNS_AND_EXAMPLE_REPOS.md    | What to emulate                     | All repos via sync     |
| .github/agents/my-agent.agent.md                | Agent spec                          | All repos via sync     |
| .cursor/agents/master-orchestrator.md           | Orchestrator instructions           | All repos via sync     |
| docs/EXPERT_PROMPT_ENGINEERING.md               | Claude/OpenAI/GOLDEN                | All repos via sync     |
| docs/LIFECYCLE_STAGES_AND_CHECKPOINTS.md        | When to run checklist               | All repos via sync     |
| docs/AGENT_ORCHESTRATION_BEST_PRACTICES.md      | Multi-agent patterns                | All repos via sync     |
| docs/CONSOLIDATION_AND_REPO_STATUS.md           | Repo map, merge status              | Reference (not synced) |

### 5.5 Automation Terms

| Term                                 | Definition                                                                      | Trigger                     |
| ------------------------------------ | ------------------------------------------------------------------------------- | --------------------------- |
| **route-constitution-to-repos.sh**   | Copy constitution, checklist, universal, bootstrap to ROUTES                    | Manual; sync script step 1  |
| **sync-all-repos-and-review.sh**     | Full sync: bootstrap agents, route, principles, modules, agent instructions     | Manual; pre-push can prompt |
| **bootstrap-child-agents-claude.sh** | Create AGENTS.md, CLAUDE.md in child repos                                      | Start of sync               |
| **verify-routing.sh**                | Check constitution refs in AGENTS.md, CLAUDE.md, my-agent, master-project-rules | Manual; CI                  |
| **verify-skills.sh**                 | Check referenced skills exist                                                   | run-all-verifications       |
| **run-all-verifications.sh**         | Platform, secrets, env, schema, routing, connections                            | Manual                      |
| **sources-compare-and-update.sh**    | Compare vs external LLM best practices; suggest updates                         | Quarterly                   |
| **pre-push hook**                    | On constitution/routing/modules/SOURCES/PRE_EXECUTION change → prompt full sync | Git pre-push                |
| **verify-routing.yml**               | PR check on constitution, rules                                                 | GitHub Actions              |
| **verify-connections.yml**           | Platform inventory                                                              | GitHub Actions              |

---

## Part 6: Repo-by-Repo Summary (Quick Reference)

| Repo                              | Location                                                                 | Purpose                                                                     | Receives   | Status                            |
| --------------------------------- | ------------------------------------------------------------------------ | --------------------------------------------------------------------------- | ---------- | --------------------------------- |
| **CURSOR CLOUD AGENTS**           | ~/.cursor/CURSOR CLOUD AGENTS                                            | Master: governance + LitigationForce production (replit-app, cases, agents) | — (source) | Canonical                         |
| **connected-agents-platform**     | ~/Documents/connected-agents-platform                                    | Platform core: ontology, modules, voice, MCP, economics                     | Full sync  | Canonical                         |
| **LitigationForce.AI**            | ~/Documents/LitigationForce-Parent/01-Litigation-Core/LitigationForce.AI | ADK litigation: scrapers, Neo4j, Claude agents                              | Full sync  | Canonical; merge variants pending |
| **file-management-toolkit**       | ~/file-management-toolkit                                                | Desktop/cloud file ops, AI clerk, dedup                                     | Full sync  | Canonical                         |
| **slack-agent-template**          | ~/.cursor/bootstrap-work/slack-agent-template                            | Slack agent template (Nitro, Bolt, AI SDK)                                  | Full sync  | Canonical; merged                 |
| **powerconnectionaiapplications** | ~/Documents/powerconnectionaiapplications                                | PowerConnection AI apps                                                     | Full sync  | Canonical; merge pending          |
| **replit-app**                    | Inside master                                                            | Deployed LitigationForce (33 agents, intelligence, marketplace)             | Via master | Subdirectory                      |
| **nextjs-ai-chatbot**             | GitHub only                                                              | AI chat UI template                                                         | —          | Clone when needed                 |
| **adk-python**                    | GitHub only                                                              | Google ADK reference                                                        | —          | Document only                     |

---

_Maintain at: docs/PLATFORM_ARCHITECTURE_EXPLAINED.md. Update when repos change, merges complete, or vocabulary evolves._
