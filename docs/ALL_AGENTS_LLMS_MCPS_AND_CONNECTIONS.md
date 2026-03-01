# All Agents, LLMs, MCPs, and Connections — Full Inventory

**Purpose:** Single reference for **every** agent, LLM provider, MCP server, and application/connection used by the OneWish OS / CURSOR CLOUD AGENTS platform. Use this when wiring dev tools (Cursor, Claude Code, Copilot, Codex), verifying env, or auditing capabilities.

**Designated section (top level & downstream):** This doc is the **master list** for the full inventory. It is listed in **docs/MASTER_INDEX.md** §11 (MCP & Connectivity — Master List) and in **AGENTS.md** (Master List — Agents, LLMs, MCPs & Connections). It is **synced to all downstream repos** (LitigationForce.AI, connected-agents-platform, file-management-toolkit, etc.) via `./scripts/sync-all-repos-and-review.sh` §6a so the same list is readily available everywhere.

**Source of truth:** `config/platform-connections.yaml` (applications, mcps, clis, llms, agents). **MCP/LLM routing:** `config/mcp-servers/master-mcp.yaml`. **Canonical MCP registry:** `config/canonical-mcp-connectors.yaml`. **Inference catalog:** `config/inference-models.yaml`. **Blackbox/LLM presets:** `config/blackbox-agents.yaml`.

**Related:** [MASTER_MCP_CONNECTORS_APIS.md](MASTER_MCP_CONNECTORS_APIS.md) (MCP/connector add flow + 1Password), [MCP_SECRETS_REFERENCE.md](MCP_SECRETS_REFERENCE.md), [MARKETING_AND_DESIGN_CONNECTIONS.md](MARKETING_AND_DESIGN_CONNECTIONS.md) (v0, Figma, Framer, Sentry, Canva), [CLAUDE_CODE_AND_CLAUDE_AI_INTEGRATION_BEGINNER.md](CLAUDE_CODE_AND_CLAUDE_AI_INTEGRATION_BEGINNER.md) §11, [DEV_TOOLS_CANONICAL_LIST_AND_AUDIT.md](DEV_TOOLS_CANONICAL_LIST_AND_AUDIT.md), [CONSOLIDATION_AND_REPO_STATUS.md](CONSOLIDATION_AND_REPO_STATUS.md).

---

## 1. Agents (26)

Defined in `config/platform-connections.yaml` under `agents`. Playbooks and roles in `config/playbooks.yaml`, `config/segment-lit-force-lexvault-connected.yaml`, and `.github/agents/my-agent.agent.md`.

| #   | Agent ID                     | Role / use              |
| --- | ---------------------------- | ----------------------- |
| 1   | config-orchestrator-agent    | Config and routing      |
| 2   | master-orchestrator          | Top-level orchestration |
| 3   | platform-architect           | Platform architecture   |
| 4   | linear-buildout-agent        | Linear integration      |
| 5   | platform-notifications-agent | Notifications           |
| 6   | slack-config-agent           | Slack integration       |
| 7   | knowledge-graph-builder      | KG build (Neo4j)        |
| 8   | entity-extractor             | Entity extraction       |
| 9   | cto-auditor                  | CTO/audit checks        |
| 10  | rico-analyzer                | RICO analysis           |
| 11  | case-analyst                 | Case analysis           |
| 12  | damages-modeler              | Damages modeling        |
| 13  | evaluator-swarm              | Evaluation swarm        |
| 14  | privilege-scanner            | Privilege (private LLM) |
| 15  | filing-generator             | Filing generation       |
| 16  | document-classifier          | Document classification |
| 17  | timeline-builder             | Timeline build          |
| 18  | email-analyzer               | Email analysis          |
| 19  | evidence-processor           | Evidence processing     |
| 20  | deposition-planner           | Deposition planning     |
| 21  | contract-analyst             | Contract analysis       |
| 22  | timeline-webapp              | Timeline UI             |
| 23  | reverse-verifier             | Reverse verification    |
| 24  | orchestrator                 | Workflow orchestrator   |
| 25  | master-intelligence          | Master intelligence     |

**Config files:** `config/agents-claude-litigation.yaml`, `config/agents-irs-tax-specialists.yaml`, `config/onewish-connections-prebuilt-agents.yaml`, `config/agent-mcp-function-matrix.yaml`.

---

## 2. LLMs (providers and routing)

### 2.1 Platform-connections (env checks)

From `config/platform-connections.yaml` § `llms`. Each has `env` and `config` (blackbox-agents or inference-models).

| Provider    | Env vars                                             | Config                       |
| ----------- | ---------------------------------------------------- | ---------------------------- |
| anthropic   | ANTHROPIC_API_KEY                                    | config/blackbox-agents.yaml  |
| openai      | OPENAI_API_KEY                                       | config/blackbox-agents.yaml  |
| gemini      | GOOGLE_API_KEY, GEMINI_API_KEY                       | config/blackbox-agents.yaml  |
| vertex_ai   | GOOGLE_APPLICATION_CREDENTIALS, GOOGLE_CLOUD_PROJECT | config/inference-models.yaml |
| google      | GOOGLE_API_KEY                                       | config/blackbox-agents.yaml  |
| blackbox    | BLACKBOX_API_KEY                                     | config/blackbox-agents.yaml  |
| xai         | XAI_API_KEY                                          | config/blackbox-agents.yaml  |
| huggingface | HF_TOKEN                                             | config/inference-models.yaml |

### 2.2 Master MCP — external and private LLM

From `config/mcp-servers/master-mcp.yaml`:

- **private_llm:** Ollama (e.g. llama-3.1-70b-instruct, mistral-large-2512). Used for: privilege_scan, privilege_determination, attorney_client_analysis, work_product_review, settlement_discussion_analysis. **Never** send privilege-flagged content to external APIs.
- **external_llm providers:** anthropic (claude-opus/sonnet/haiku), openai (gpt-5.2-codex, gpt-5, o3-pro), google (gemini-2.5-pro/flash), blackbox (blackbox-pro), goose (GOOSE_API_KEY). **Routing:** rico/contract → anthropic; privilege → private_llm; damages → openai; document_review → google; deep_research → openai.

---

## 3. MCPs (servers / connectors)

From `config/platform-connections.yaml` § `mcps` and `config/canonical-mcp-connectors.yaml`.

| MCP          | Env / check                               | Description                       |
| ------------ | ----------------------------------------- | --------------------------------- |
| supabase     | (cursor-mcp-enhanced.json)                | Supabase                          |
| notion       | NOTION_API_KEY                            | Notion — wikis, case matrix       |
| linear       | LINEAR_API_KEY                            | Linear — issues, projects         |
| github       | GITHUB_PERSONAL_ACCESS_TOKEN              | GitHub — repos, PRs               |
| slack        | SLACK_BOT_TOKEN                           | Slack                             |
| postgres     | POSTGRES_URL                              | Postgres / Neon                   |
| brave_search | BRAVE_API_KEY                             | Brave Search                      |
| neo4j        | NEO4J_URI, NEO4J_USERNAME, NEO4J_PASSWORD | Knowledge graph                   |
| airtable     | AIRTABLE_API_KEY                          | Airtable                          |
| firebase     | FIREBASE_SERVICE_ACCOUNT                  | Firebase                          |
| apify        | APIFY_API_TOKEN                           | Apify                             |
| huggingface  | HF_TOKEN                                  | Hugging Face                      |
| codacy       | —                                         | Codacy (quality)                  |
| fetch        | —                                         | Fetch                             |
| git          | git rev-parse                             | Git                               |
| MCP_DOCKER   | docker info                               | Docker gateway                    |
| firecrawl    | FIRECRAWL_API_KEY                         | Firecrawl — scrape, search, crawl |
| attio        | ATTIO_API_KEY                             | Attio — CRM                       |
| atlassian    | ATLASSIAN_API_TOKEN, ATLASSIAN_USER_EMAIL | Jira, Confluence                  |
| docker       | —                                         | MCP_DOCKER gateway                |

**Cursor MCP config:** `.cursor/mcp.json` or equivalent; env in `config/mcp-servers/.env.mcp` (see `.env.mcp.example`).

---

## 4. Applications / connections (40+)

From `config/platform-connections.yaml` § `applications`. Each has `env` and optional `check` / `note`.

| Application       | Env (typical)                                                  | Note                                           |
| ----------------- | -------------------------------------------------------------- | ---------------------------------------------- |
| google_cloud      | GOOGLE_APPLICATION_CREDENTIALS, GOOGLE_CLOUD_PROJECT           | GCP, Document AI, BigQuery                     |
| linear            | LINEAR_API_KEY                                                 | + config/linear-project-mappings.yaml          |
| slack             | SLACK_BOT_TOKEN, SLACK_WEBHOOK_URL                             |                                                |
| github            | GITHUB_PERSONAL_ACCESS_TOKEN                                   | gh auth status                                 |
| notion            | NOTION_API_KEY                                                 |                                                |
| supabase          | SUPABASE_URL, SUPABASE_SERVICE_ROLE_KEY                        |                                                |
| postgres          | POSTGRES_URL, DATABASE_URL                                     |                                                |
| neo4j             | NEO4J_URI, NEO4J_USERNAME, NEO4J_PASSWORD                      |                                                |
| 1password         | (op CLI)                                                       | op --version                                   |
| vercel            | VERCEL_TOKEN                                                   |                                                |
| airtable          | AIRTABLE_API_KEY                                               |                                                |
| hubspot           | HUBSPOT_ACCESS_TOKEN                                           |                                                |
| attio             | ATTIO_API_KEY                                                  |                                                |
| stripe            | STRIPE_SECRET_KEY                                              |                                                |
| firebase          | FIREBASE_SERVICE_ACCOUNT                                       |                                                |
| apify             | APIFY_API_TOKEN                                                |                                                |
| brave_search      | BRAVE_API_KEY                                                  |                                                |
| blackbox          | BLACKBOX_API_KEY                                               |                                                |
| microsoft_copilot | MS_GRAPH_CLIENT_ID, MS_GRAPH_CLIENT_SECRET, MS_GRAPH_TENANT_ID | Outlook, Teams, OneDrive                       |
| aws               | AWS_ACCESS_KEY_ID, AWS_SECRET_ACCESS_KEY                       |                                                |
| zoom              | ZOOM_API_KEY, ZOOM_API_SECRET                                  |                                                |
| box               | BOX_CLIENT_ID, BOX_CLIENT_SECRET, BOX_ENTERPRISE_ID            |                                                |
| replit            | REPLIT_API_KEY                                                 | SwarmRICO, Verital-Legal-Tech                  |
| lovable           | LOVABLE_API_KEY                                                |                                                |
| huggingface       | HF_TOKEN                                                       |                                                |
| v0                | V0_API_KEY, VERCEL_TOKEN                                       |                                                |
| framer            | FRAMER_API_KEY                                                 |                                                |
| egnyte            | EGNYTE_ACCESS_TOKEN, …                                         | Legal stack; Power Connection AI               |
| goose             | GOOSE_API_KEY                                                  | AI dev agent                                   |
| canva             | CANVA_ACCESS_TOKEN                                             | Design, presentations                          |
| adobe             | ADOBE_CLIENT_ID, ADOBE_CLIENT_SECRET                           |                                                |
| pipefy            | PIPEFY_API_TOKEN                                               |                                                |
| zendesk           | ZENDESK_ACCESS_TOKEN                                           |                                                |
| zoho              | ZOHO_ACCESS_TOKEN                                              |                                                |
| perplexity        | PERPLEXITY_API_KEY                                             |                                                |
| duckduckgo        | DDG_API_KEY                                                    |                                                |
| atlassian         | ATLASSIAN_API_TOKEN, ATLASSIAN_USER_EMAIL                      | Jira, Confluence                               |
| clay              | CLAY_API_KEY                                                   |                                                |
| todoist           | TODOIST_API_TOKEN                                              |                                                |
| trello            | TRELLO_API_KEY, TRELLO_TOKEN                                   |                                                |
| okta              | OKTA_DOMAIN, OKTA_API_TOKEN                                    |                                                |
| sentry            | SENTRY_DSN, SENTRY_AUTH_TOKEN                                  | Error monitoring; Vercel + Sentry per app      |
| figma             | (URL-based MCP)                                                | Design — MCP; get_design_context, code_connect |

**1Password / Cursor secrets:** v0 → `V0_API_KEY`, `VERCEL_TOKEN` (Vercel / v0); Canva → `CANVA_ACCESS_TOKEN` (Canva); Sentry → `SENTRY_DSN`, `SENTRY_AUTH_TOKEN` (Sentry). See [MCP_SECRETS_REFERENCE.md](MCP_SECRETS_REFERENCE.md) §4 and [MARKETING_AND_DESIGN_CONNECTIONS.md](MARKETING_AND_DESIGN_CONNECTIONS.md).

(Additional entries may exist in `platform-connections.yaml`; always read the file for the current list.)

---

## 5. CLIs (required for checks)

From `config/platform-connections.yaml` § `clis`: op, gh, vercel, docker, npx, python3, jq, curl.

---

## 6. Verification and scripts

| Action                        | Command / script                                                                    |
| ----------------------------- | ----------------------------------------------------------------------------------- |
| Verify platform connections   | `./scripts/verify-platform-connections.sh` or `./scripts/verify-all-connections.sh` |
| MCP sync (canonical → others) | `python3 scripts/sync-canonical-mcp-connectors.py`                                  |
| Env example                   | `config/mcp-servers/.env.mcp.example`                                               |
| 1Password mapping             | docs/PLATFORMS_1PASSWORD_MAPPING.md, docs/MCP_SECRETS_REFERENCE.md                  |

---

## 7. Cross-references

| Doc                                                                                                                  | Purpose                                                    |
| -------------------------------------------------------------------------------------------------------------------- | ---------------------------------------------------------- |
| [CLAUDE_CODE_AND_CLAUDE_AI_INTEGRATION_BEGINNER.md](CLAUDE_CODE_AND_CLAUDE_AI_INTEGRATION_BEGINNER.md)               | Claude + repo integration; §11 summary                     |
| [DEV_TOOLS_CANONICAL_LIST_AND_AUDIT.md](DEV_TOOLS_CANONICAL_LIST_AND_AUDIT.md)                                       | Cursor, Claude Code, Copilot, Codex, v0, etc.              |
| [GITHUB_ORGANIZE_SIMPLIFY_NAMING_ARCHIVE_AND_INTEGRATE.md](GITHUB_ORGANIZE_SIMPLIFY_NAMING_ARCHIVE_AND_INTEGRATE.md) | GitHub instance; naming; archive vs reference vs integrate |
| [CONSOLIDATION_AND_REPO_STATUS.md](CONSOLIDATION_AND_REPO_STATUS.md)                                                 | Canonical repo map; routing; sync                          |

---

_Maintain at: docs/ALL_AGENTS_LLMS_MCPS_AND_CONNECTIONS.md. Update when adding agents, LLMs, MCPs, or applications to config._
