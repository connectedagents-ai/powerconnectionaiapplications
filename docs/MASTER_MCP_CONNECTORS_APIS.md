# Master MCP, Connectors & APIs List

> **Single source of truth** for all AI tools, MCP servers, connectors, and APIs used by the **One Wish Agent / NextTech OS MCP server** (master MCP router in this repo). Referenced by constitution, my-agent.agent.md, and platform documentation.

**Sync trigger:** Add new MCP/connectors only to **config/canonical-mcp-connectors.yaml**, then run **`python3 scripts/sync-canonical-mcp-connectors.py`** so they propagate to platform-connections, .env.mcp.example, MCP_MAP, and (where applicable) connectors and master-mcp. See **docs/MCP_CONNECTOR_SYNC_AND_TRIGGER.md**.

**Completeness:** This list and **docs/MCP_SECRETS_REFERENCE.md** are kept complete against 1Password vault items (`config/mcp-servers/1password-*.json`, `docs/1PASSWORD_VAULT_ORGANIZATION.md`) and **docs/MAC_APP_INTEGRATION_AUDIT.md**. Constitution §6 (new capabilities), Cloud & Inference refs, and **.github/agents/my-agent.agent.md** (master inventory) apply. After adding integrations: run `./scripts/agent-1password-index-env.sh`; update **PLATFORMS_1PASSWORD_MAPPING.md** and this doc.

---

## 1. LLM & AI Chat Tools (Accounts, APIs, Agents)

**Cursor secrets:** See **docs/MCP_SECRETS_REFERENCE.md** §2 (LLM & AI APIs). Map each secret to the env var below.

| Tool                   | 1Password Item       | Env Var                          | Cursor Secret Name(s)                               | Config                      | Notes                              |
| ---------------------- | -------------------- | -------------------------------- | --------------------------------------------------- | --------------------------- | ---------------------------------- |
| **Claude (Anthropic)** | Anthropic, Claude    | `ANTHROPIC_API_KEY`              | `anthropic.secret.ces.com`, `claude.secret.ces.com` | master-mcp, connectors      | Claude API, Claude bot             |
| **Claude Code**        | (uses Anthropic)     | `ANTHROPIC_API_KEY`              | Same                                                | ~/.claude.json, CLAUDE.md   | IDE; reads CLAUDE.md               |
| **Claude Co-worker**   | (uses Anthropic)     | `ANTHROPIC_API_KEY`              | Same                                                | Same as Claude Code         | Co-worker mode                     |
| **ChatGPT (OpenAI)**   | OpenAI, ChatGPT      | `OPENAI_API_KEY`                 | `openai.secret.ces.com`, `chatgpt.secret.ces.com`   | master-mcp external_llm     | GPT-5, o3-pro, etc.                |
| **Perplexity**         | Perplexity           | `PERPLEXITY_API_KEY`             | `perplexity.secret.ces.com`                         | connectors                  | Search-augmented LLM               |
| **Genspark**           | Genspark             | `GENSPARK_API_KEY` (if API)      | `genspark.secret.ces.com`                           | TBD                         | AI workspace; API availability TBD |
| **Gemini / Google AI** | Gemini, Google AI    | `GOOGLE_API_KEY`                 | `google.api_key.ces.com`, `gemini.secret.ces.com`   | master-mcp, connectors      | Primary inference                  |
| **Vertex AI**          | Vertex, Google Cloud | `GOOGLE_APPLICATION_CREDENTIALS` | `google.credentials.ces.com`                        | connectors                  | Enterprise Gemini                  |
| **Blackbox**           | Blackbox             | `BLACKBOX_API_KEY`               | `blackbox.secret.ces.com`                           | master-mcp, blackbox-agents | Multi-model                        |
| **xAI (Grok)**         | Grok, xAI            | `XAI_API_KEY`                    | `xai.secret.ces.com`, `grok.secret.ces.com`         | connectors                  |                                    |

---

## 2. Search APIs

| Tool                     | 1Password Item | Env Var                            | MCP/Config       | Notes                        |
| ------------------------ | -------------- | ---------------------------------- | ---------------- | ---------------------------- |
| **Brave Search**         | Brave          | `BRAVE_API_KEY`                    | brave_search MCP | Primary search API           |
| **DuckDuckGo**           | DuckDuckGo     | `DDG_API_KEY` (Instant Answer)     | —                | Limited API; Brave preferred |
| **Google Custom Search** | Google         | `GOOGLE_API_KEY` + `GOOGLE_CSE_ID` | —                | Alternative search           |

---

## 3. MCP Servers (cursor-mcp-enhanced.json)

**Cursor secrets:** For each secret-requiring MCP, use the Cursor (team) secret name in **docs/MCP_SECRETS_REFERENCE.md**; map secret value to the env var(s) below.

| MCP Server       | Env Vars                                                            | Cursor Secret(s)                                                               | Purpose                                                                                                |
| ---------------- | ------------------------------------------------------------------- | ------------------------------------------------------------------------------ | ------------------------------------------------------------------------------------------------------ |
| **supabase**     | (URL-based)                                                         | —                                                                              | DB, auth, storage                                                                                      |
| **codacy**       | —                                                                   | —                                                                              | Code quality; run `codacy_cli_analyze` after edits; Trivy for deps. Cursor: `.cursor/rules/codacy.mdc` |
| **Auth0**        | (URL-based)                                                         | —                                                                              | Auth                                                                                                   |
| **MCP_DOCKER**   | —                                                                   | —                                                                              | Docker gateway                                                                                         |
| **Agent Skills** | (URL-based)                                                         | —                                                                              | agentskills.io                                                                                         |
| **notion**       | `NOTION_API_KEY`                                                    | `notion.secret.ces.com`                                                        | Wiki, case notes                                                                                       |
| **linear**       | `LINEAR_API_KEY`                                                    | `linear.secret.ces.com`                                                        | Project tracking                                                                                       |
| **github**       | `GITHUB_PERSONAL_ACCESS_TOKEN`                                      | `github.secret.ces.com`                                                        | Repos, PRs                                                                                             |
| **slack**        | `SLACK_BOT_TOKEN`                                                   | `slack.secret.ces.com`                                                         | Comms                                                                                                  |
| **postgres**     | `POSTGRES_URL`                                                      | `postgres.secret.ces.com`                                                      | Database                                                                                               |
| **brave_search** | `BRAVE_API_KEY`                                                     | `brave.secret.ces.com`                                                         | Web search                                                                                             |
| **firecrawl**    | `FIRECRAWL_API_KEY`                                                 | `firecrawl.secret.ces.com`                                                     | Scrape, Search, Crawl, Agent — LLM-ready web data; see docs/FIRECRAWL_API_AND_INTEGRATIONS.md          |
| **fetch**        | —                                                                   | —                                                                              | URL fetch                                                                                              |
| **git**          | —                                                                   | —                                                                              | Git ops                                                                                                |
| **neo4j**        | `NEO4J_URI`, `NEO4J_USER`, `NEO4J_PASSWORD`                         | `neo4j.uri.ces.com`, `neo4j.user.ces.com`, `neo4j.password.ces.com`            | Knowledge graph                                                                                        |
| **attio**        | `ATTIO_API_KEY` (when used with API key)                            | `attio.secret.ces.com`                                                         | CRM; MCP can be URL-based or use API key                                                               |
| **hubspot**      | (URL-based)                                                         | —                                                                              | CRM                                                                                                    |
| **stripe**       | (URL-based)                                                         | —                                                                              | Payments                                                                                               |
| **airtable**     | `AIRTABLE_API_KEY`                                                  | `airtable.secret.ces.com`                                                      | DB, CRM; see §9a and docs/AIRTABLE_SECRET_SETUP.md                                                     |
| **figma**        | (URL-based)                                                         | —                                                                              | Design                                                                                                 |
| **firebase**     | `FIREBASE_SERVICE_ACCOUNT`                                          | `firebase.secret.ces.com`                                                      | Backend                                                                                                |
| **greptile**     | (URL-based)                                                         | —                                                                              | Code intelligence; PR code review                                                                      |
| **apify**        | `APIFY_API_TOKEN`                                                   | `apify.secret.ces.com`                                                         | Scraping, automation                                                                                   |
| **huggingface**  | `HF_TOKEN`                                                          | `huggingface.secret.ces.com`                                                   | Models, Spaces                                                                                         |
| **atlassian**    | `ATLASSIAN_API_TOKEN`, `ATLASSIAN_USER_EMAIL`, `ATLASSIAN_SITE_URL` | `atlassian.token.ces.com`, `atlassian.email.ces.com`, `atlassian.site.ces.com` | Jira, Confluence (Docker MCP)                                                                          |
| **mcp-graphql**  | `ENDPOINT`, `HEADERS` (JSON)                                        | (per endpoint)                                                                 | Generic GraphQL APIs (Linear, HubSpot, custom)                                                         |

---

## 3b. GraphQL Integration

| Tool            | GraphQL? | Notes                                                                      |
| --------------- | -------- | -------------------------------------------------------------------------- |
| **Supabase**    | Yes      | `search_docs` requires GraphQL query string                                |
| **Linear**      | Yes      | Full API at `api.linear.app/graphql`                                       |
| **HubSpot**     | Yes      | CRM objects via GraphQL                                                    |
| **mcp-graphql** | Yes      | Generic server for any GraphQL endpoint; see `docs/GRAPHQL_INTEGRATION.md` |

---

## 4. Connectors (config/connectors.yaml)

**Cursor secrets for connectors:** See **docs/MCP_SECRETS_REFERENCE.md** §2 (LLM), §3 (CRM, Zoom, Google, Microsoft, Docker), §4 (Dev apps). Examples: Replit `replit.secret.ces.com`, Lovable `lovable.secret.ces.com`, Vercel/v0 `vercel.secret.ces.com`, Goose `goose.secret.ces.com`.

| Connector                                                    | Env Vars                                                 | Category         |
| ------------------------------------------------------------ | -------------------------------------------------------- | ---------------- |
| google_cloud                                                 | `GOOGLE_APPLICATION_CREDENTIALS`, `GOOGLE_CLOUD_PROJECT` | Cloud            |
| gemini_api                                                   | `GOOGLE_API_KEY`                                         | LLM              |
| vertex_ai                                                    | `GOOGLE_APPLICATION_CREDENTIALS`, `GOOGLE_CLOUD_PROJECT` | LLM              |
| google_developer                                             | `GOOGLE_CLIENT_ID`, `GOOGLE_CLIENT_SECRET`               | OAuth            |
| microsoft_copilot                                            | `MS_GRAPH_*`                                             | Microsoft        |
| aws                                                          | `AWS_*`                                                  | Cloud            |
| zoom                                                         | `ZOOM_API_KEY`, `ZOOM_API_SECRET`                        | Comms            |
| egnyte                                                       | `EGNYTE_*`                                               | Storage          |
| box                                                          | `BOX_*`                                                  | Storage          |
| replit, lovable, huggingface, vercel, v0, framer             | (per tool)                                               | Vibe code        |
| canva, adobe                                                 | `CANVA_*`, `ADOBE_*`                                     | Design           |
| pipefy, zendesk, zoho                                        | `PIPEFY_*`, etc.                                         | Workflow         |
| atlassian                                                    | `ATLASSIAN_API_TOKEN`, `ATLASSIAN_USER_EMAIL`            | Jira, Confluence |
| clay, todoist, trello, okta                                  | `CLAY_*`, `TODOIST_*`, `TRELLO_*`, `OKTA_*`              | CRM, tasks, auth |
| goose                                                        | `GOOSE_API_KEY`                                          | AI dev           |
| relativity, everlaw, clio, spellbook, briefpoint, lexisnexis | (per tool)                                               | Legal            |

---

## 5. Master MCP Router (config/mcp-servers/master-mcp.yaml)

### External LLM Providers

| Provider  | Key Env             | Models / notes                                           |
| --------- | ------------------- | -------------------------------------------------------- |
| anthropic | `ANTHROPIC_API_KEY` | claude-opus/sonnet/haiku                                 |
| openai    | `OPENAI_API_KEY`    | gpt-5, o3-pro                                            |
| google    | `GOOGLE_API_KEY`    | gemini-2.5-\*                                            |
| blackbox  | `BLACKBOX_API_KEY`  | blackbox-pro                                             |
| goose     | `GOOSE_API_KEY`     | api.goose.ai engines (AI dev); mirrors Docker/connectors |

### Vendors (API)

**Cursor secrets:** Microsoft: `microsoft.client_id.ces.com`, `microsoft.client_secret.ces.com`, `microsoft.tenant_id.ces.com`. Zoom: `zoom.api_key.ces.com`, `zoom.api_secret.ces.com`. See docs/MCP_SECRETS_REFERENCE.md §3.

| Vendor                                                                           | Key Envs                          | Cursor Secret Name(s) (see MCP_SECRETS_REFERENCE) | Tools                                                   |
| -------------------------------------------------------------------------------- | --------------------------------- | ------------------------------------------------- | ------------------------------------------------------- |
| microsoft_copilot                                                                | `MS_GRAPH_*`                      | microsoft.client_id/secret/tenant_id.ces.com      | copilot_graph_query, copilot_plugin_invoke              |
| aws                                                                              | `AWS_*`                           | (per env)                                         | aws_s3_upload, aws_textract_analyze, aws_bedrock_invoke |
| zoom                                                                             | `ZOOM_API_KEY`, `ZOOM_API_SECRET` | zoom.api_key.ces.com, zoom.api_secret.ces.com     | zoom_meeting_list, zoom_recording_get                   |
| box                                                                              | `BOX_*`                           | (per env)                                         | box_search, box_upload                                  |
| relativity, everlaw, clio, spellbook, briefpoint, lexisnexis, tyler_technologies | (per vendor)                      | —                                                 | Legal workflow tools                                    |

### Internal Services

| Service    | Env Vars                                    | Tools                                       |
| ---------- | ------------------------------------------- | ------------------------------------------- |
| neo4j      | `NEO4J_URI`, `NEO4J_USER`, `NEO4J_PASSWORD` | neo4j*query, neo4j_create*\*, neo4j_analyze |
| supabase   | `SUPABASE_URL`, `SUPABASE_KEY`              | supabase_query, supabase_upload             |
| vector_db  | (pgvector via Supabase)                     | vector_search, vector_embed                 |
| elevenlabs | `ELEVENLABS_API_KEY`                        | elevenlabs_transcribe, elevenlabs_speak     |

### Connected Apps (MCP Plugins)

| App        | Server                   | Capabilities                 |
| ---------- | ------------------------ | ---------------------------- |
| notion     | plugin-Notion-notion     | search, read, create, update |
| linear     | plugin-linear-linear     | issues, projects, teams      |
| github     | plugin-github-github     | repos, prs, issues           |
| figma      | plugin-figma-figma       | design_context, code_connect |
| firebase   | plugin-firebase-firebase | auth, firestore, hosting     |
| greptile   | plugin-greptile-greptile | code_search, pr_review       |
| **docker** | MCP_DOCKER               | containers, images, compose  |
| **goose**  | API (api.goose.ai)       | completions, AI dev          |
| merge      | API                      | accounting, expense          |
| plaid      | API                      | banking, transactions        |

**Also in master-mcp**: attio, airtable, brave_search, atlassian

**From Mac audit**: Atlassian (Jira/Confluence), Clay, Todoist, Okta, Trello — see `docs/MAC_APP_INTEGRATION_AUDIT.md`

---

## 5b. MCP and Connectors Used by Major LLMs (Mirror Policy)

**Policy:** All major LLM entry points (Cursor, Claude Code, Codex, etc.) **mirror the same** MCP and connector inventory. The canonical sources are: **config/mcp-servers/master-mcp.yaml**, **config/mcp-servers/cursor-mcp-enhanced.json**, **config/connectors.yaml**, and **config/platform-connections.yaml**. This doc is the single master list.

| LLM / IDE             | MCP source                                                 | Connectors source                   | Env / launch                                       |
| --------------------- | ---------------------------------------------------------- | ----------------------------------- | -------------------------------------------------- |
| **Cursor**            | ~/.cursor/mcp.json ← cursor-mcp-enhanced.json + MCP_DOCKER | connectors.yaml                     | op run --env-file=.env.mcp -- cursor               |
| **Claude Code**       | ~/.claude.json (if MCP configured); CLAUDE.md              | Same inventory (this doc)           | op run --env-file=.env.mcp -- claude               |
| **Codex**             | Worktree/config; same inventory (this doc)                 | Same inventory (this doc)           | op run --env-file=.env.mcp -- codex                |
| **Master MCP router** | config/mcp-servers/master-mcp.yaml                         | Vendors + internal + connected_apps | Used by orchestrator / agents that read master-mcp |

**Unified master list (all MCP servers):** Supabase, Codacy, Auth0, MCP_DOCKER, Agent Skills, Notion, Linear, GitHub, Slack, Postgres, Brave Search, Fetch, Git, Neo4j, Attio, HubSpot, Stripe, Airtable, Figma, Firebase, Greptile, Apify, Hugging Face, Atlassian, mcp-graphql. **Plus Docker catalog (via MCP_DOCKER):** airtable-mcp-server, apify-mcp-server, brave, context7, duckduckgo, fetch, git, github-official, memory, neo4j-memory, playwright, slack, time, and others — see docs/DOCKER_APPS_AND_MCP_BEST_PRACTICES.md.

**Unified master list (all connectors):** google_cloud, gemini_api, vertex_ai, google_developer, microsoft_copilot, microsoft_365, aws, zoom, egnyte, box, google_file_management, replit, lovable, huggingface, vercel, v0, framer, canva, adobe, atlassian, clay, todoist, trello, okta, pipefy, zendesk, zoho, **goose**, perplexity, duckduckgo, relativity, everlaw, clio, spellbook, briefpoint, lexisnexis (and inference: anthropic, openai, blackbox). See **config/connectors.yaml** for full list.

**LLM providers (all mirror same env):** Anthropic, OpenAI, Google, Blackbox, **Goose** — key env vars in master-mcp.yaml external_llm + private_llm (Ollama). Launch with `./scripts/launch-ai-with-op.sh <cursor|claude|codex|goose|ollama|...>` so every tool gets the same .env.mcp.

### Single master list: all MCP servers (by source)

| Source                             | MCP servers                                                                                                                                                                                                                                                                       |
| ---------------------------------- | --------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| **cursor-mcp-enhanced.json**       | supabase, codacy, Auth0, MCP_DOCKER, Agent Skills, notion, linear, github, slack, postgres, brave_search, fetch, git, neo4j, attio, hubspot, stripe, airtable, figma, firebase, greptile, apify, huggingface, atlassian                                                           |
| **MCP_DOCKER catalog**             | airtable-mcp-server, apify-mcp-server, brave, cloud-run-mcp, context7, databutton, desktop-commander, dockerhub, duckduckgo, elasticsearch, fetch, git, github-official, hostinger-mcp-server, mcp-api-gateway, memory, neo4j-memory, playwright, sequentialthinking, slack, time |
| **master-mcp.yaml connected_apps** | notion, linear, github, figma, firebase, greptile, attio, airtable, brave_search, **docker (MCP_DOCKER)**, **goose**, atlassian                                                                                                                                                   |

### Single master list: all connectors (config/connectors.yaml)

google_cloud, gemini_api, vertex_ai, google_developer, microsoft_copilot, microsoft_365, aws, zoom, egnyte, box, google_file_management, replit, lovable, huggingface, vercel, v0, framer, canva, adobe, atlassian, clay, todoist, trello, okta, pipefy, zendesk, zoho, **goose**, perplexity, duckduckgo, e_discovery (relativity, everlaw), practice (clio), legal_ai (spellbook, briefpoint), research (lexisnexis), inference (vertex_ai, gemini_api, anthropic, openai, perplexity, blackbox).

---

## 6. Zoom (Meetings, Agents, SDK)

**Cursor secrets:** `zoom.api_key.ces.com`, `zoom.api_secret.ces.com` → see docs/MCP_SECRETS_REFERENCE.md §3.

| Component   | 1Password | Env Vars                          | Cursor Secret Name(s)                             | Docs                      |
| ----------- | --------- | --------------------------------- | ------------------------------------------------- | ------------------------- |
| Zoom API    | Zoom      | `ZOOM_API_KEY`, `ZOOM_API_SECRET` | `zoom.api_key.ces.com`, `zoom.api_secret.ces.com` | developers.zoom.us        |
| Zoom SDK    | Same      | Same                              | Same                                              | Meeting SDK, AI Companion |
| Zoom Agents | Same      | Same                              | Same                                              | Via Zoom API              |

---

## 7. Attio & Salesforce (CRM)

**Cursor secrets:** Attio: `attio.secret.ces.com` → `ATTIO_API_KEY`. Salesforce: `salesforce.token.ces.com`, `salesforce.instance.ces.com` → see docs/MCP_SECRETS_REFERENCE.md §3.

| Component  | 1Password            | Env Vars                                             | Cursor Secret Name(s)                                     |
| ---------- | -------------------- | ---------------------------------------------------- | --------------------------------------------------------- |
| Attio      | Attio, app.attio.com | `ATTIO_API_KEY`                                      | `attio.secret.ces.com`                                    |
| Salesforce | Salesforce           | `SALESFORCE_ACCESS_TOKEN`, `SALESFORCE_INSTANCE_URL` | `salesforce.token.ces.com`, `salesforce.instance.ces.com` |
| Developer  | Same                 | API key from settings                                | app.attio.com                                             |

---

## 8. Neo4j, Docker

**Cursor secrets:** Docker (optional): `docker.secret.ces.com` → `DOCKER_CONFIG`. Neo4j: see §3 table.

| Tool       | 1Password                               | Env Vars                                        | Cursor Secret Name(s)        | MCP/Config                     |
| ---------- | --------------------------------------- | ----------------------------------------------- | ---------------------------- | ------------------------------ |
| Neo4j      | Neo4j                                   | `NEO4J_URI`, `NEO4J_USERNAME`, `NEO4J_PASSWORD` | §3 (neo4j.uri/user/password) | neo4j MCP, master-mcp internal |
| Docker     | Docker, hub.docker.com, auth.docker.com | `DOCKER_CONFIG` (optional)                      | `docker.secret.ces.com`      | MCP_DOCKER                     |
| Docker Hub | Same                                    | docker login                                    | Same                         | For private images             |

---

## 9. Airtable, Google, DuckDuckGo, Brave

**Cursor secrets:** Google: `google.api_key.ces.com`, `google.credentials.ces.com` (Drive/Vertex). See docs/MCP_SECRETS_REFERENCE.md §2–3.

| Tool       | 1Password                   | Env Var                                | Cursor Secret Name(s)                                  | Config                        |
| ---------- | --------------------------- | -------------------------------------- | ------------------------------------------------------ | ----------------------------- |
| Airtable   | Airtable                    | `AIRTABLE_API_KEY`, `AIRTABLE_BASE_ID` | `airtable.secret.ces.com` (§9a)                        | MCP, platform-connections     |
| Google     | Google, accounts.google.com | `GOOGLE_*` (varies)                    | `google.api_key.ces.com`, `google.credentials.ces.com` | connectors, multiple products |
| DuckDuckGo | DuckDuckGo                  | `DDG_API_KEY` (Instant Answer)         | — Add when needed                                      | — Add when needed             |
| Brave      | Brave                       | `BRAVE_API_KEY`                        | `brave.secret.ces.com`                                 | MCP brave_search              |

### 9a. Airtable — All-Access Secret (Cursor, MCP, 1Password)

| Where              | Name / Item                                | Value / Notes                                                                                                                            |
| ------------------ | ------------------------------------------ | ---------------------------------------------------------------------------------------------------------------------------------------- |
| **Cursor Secrets** | `airtable.secret.ces.com`                  | Paste Airtable Personal Access Token (PAT). Map to MCP env `AIRTABLE_API_KEY`.                                                           |
| **MCP (mcp.json)** | Env var `AIRTABLE_API_KEY`                 | Injected from Cursor secret or `op run`; used by `@airtable/mcp-server`.                                                                 |
| **1Password**      | `airtable.com` or "Airtable"               | Store same PAT for `op run --env-file=config/mcp-servers/.env.mcp` and scripts.                                                          |
| **Airtable (PAT)** | Token name: `airtable.cec.com.auth.master` | Single master PAT; **Access**: All current and future bases. Create at [airtable.com/create/tokens](https://airtable.com/create/tokens). |
| **Scopes (PAT)**   | —                                          | `data.records:read`, `data.records:write`, `schema.bases:read`, `schema.bases:write` (minimum for MCP).                                  |

See **docs/AIRTABLE_SECRET_SETUP.md** for step-by-step setup.

---

## 10. Where Each Is Documented

| Topic                                                     | Primary Doc                                   | Secondary                                              |
| --------------------------------------------------------- | --------------------------------------------- | ------------------------------------------------------ |
| **This master list**                                      | `docs/MASTER_MCP_CONNECTORS_APIS.md`          | —                                                      |
| **All MCP secrets**                                       | `docs/MCP_SECRETS_REFERENCE.md`               | Cursor secret names, env vars, 1Password for every MCP |
| **Airtable secret**                                       | `docs/AIRTABLE_SECRET_SETUP.md`               | Cursor secret, MCP, 1Password, PAT                     |
| **Goose setup**                                           | `docs/GOOSE_SETUP_AND_INTEGRATION.md`         | API key, 1Password, launch, master-mcp, connectors     |
| **Sync trigger (add to all)**                             | `docs/MCP_CONNECTOR_SYNC_AND_TRIGGER.md`      | Canonical registry; sync script; add once → propagate  |
| **Marketing & design (v0, Sentry, Canva, Figma, Framer)** | `docs/MARKETING_AND_DESIGN_CONNECTIONS.md`    | Node, Figma MCP, v0, Sentry, Canva, 1Password refs     |
| Constitution                                              | `docs/constitution.md`                        | References this doc                                    |
| 1Password → env                                           | `docs/PLATFORMS_1PASSWORD_MAPPING.md`         | `scripts/agent-1password-index-env.sh`                 |
| Connectors                                                | `config/connectors.yaml`                      | —                                                      |
| Platform connections                                      | `config/platform-connections.yaml`            | —                                                      |
| Master MCP router                                         | `config/mcp-servers/master-mcp.yaml`          | —                                                      |
| Cursor MCP config                                         | `config/mcp-servers/cursor-mcp-enhanced.json` | —                                                      |
| Agent spec                                                | `.github/agents/my-agent.agent.md`            | `agents/my-agent.agent.md`                             |
| Claude Code setup                                         | `CLAUDE.md`, `docs/DEV_TOOLS_RULES_SETUP.md`  | ~/.claude.json                                         |
| Similar apps checklist                                    | `docs/SIMILAR_APPS_CONNECTION_CHECKLIST.md`   | —                                                      |
| Cross-system index                                        | `docs/cross-system-index.md`                  | —                                                      |
| **1Password / Mac alignment**                             | `docs/MCP_SECRETS_REFERENCE.md` §6            | Completeness vs vault + MAC_APP_INTEGRATION_AUDIT      |
| **Constitution**                                          | `docs/constitution.md` §6, Cloud & Inference  | New capabilities; platform audit                       |

---

## 11. Recently Added (Complete)

| Item       | Status                                                                                                                          | Env Var                           |
| ---------- | ------------------------------------------------------------------------------------------------------------------------------- | --------------------------------- |
| Perplexity | ✅ connectors, MCP_MAP, platform-connections                                                                                    | `PERPLEXITY_API_KEY`              |
| Genspark   | ✅ MCP_MAP (API TBD)                                                                                                            | `GENSPARK_API_KEY`                |
| DuckDuckGo | ✅ connectors, MCP_MAP                                                                                                          | `DDG_API_KEY`                     |
| Attio      | ✅ master-mcp connected_apps                                                                                                    | `ATTIO_API_KEY`                   |
| Airtable   | ✅ master-mcp connected_apps                                                                                                    | `AIRTABLE_API_KEY`                |
| Docker     | ✅ master-mcp connected_apps (MCP_DOCKER); mirrors cursor + master-mcp                                                          | `DOCKER_CONFIG`                   |
| Brave      | ✅ master-mcp connected_apps                                                                                                    | `BRAVE_API_KEY`                   |
| **Goose**  | ✅ connectors, platform-connections, master-mcp (external_llm + connected_apps), launch-ai-with-op, GOOSE_SETUP_AND_INTEGRATION | `GOOSE_API_KEY`                   |
| **v0**     | ✅ platform-connections, canonical-mcp-connectors, .env.mcp.example; V0_SETUP_AND_INSTRUCTIONS.md; 1Password: Vercel / v0       | `V0_API_KEY`, `VERCEL_TOKEN`      |
| **Sentry** | ✅ platform-connections, canonical-mcp-connectors, .env.mcp.example; 1Password: Sentry                                          | `SENTRY_DSN`, `SENTRY_AUTH_TOKEN` |
| **Canva**  | ✅ platform-connections, canonical-mcp-connectors, .env.mcp.example; segment design export; 1Password: Canva                    | `CANVA_ACCESS_TOKEN`              |
| **Figma**  | ✅ .cursor/mcp.json (project + user), platform-connections mcps; URL-based MCP (no key)                                         | —                                 |

**Marketing & design stack (Node, Figma, Framer, v0, Sentry, Canva):** See **docs/MARKETING_AND_DESIGN_CONNECTIONS.md**.

---

## 12. Re-index After Changes

```bash
./scripts/agent-1password-index-env.sh
```

Run after adding new 1Password items or MCP_MAP entries.
