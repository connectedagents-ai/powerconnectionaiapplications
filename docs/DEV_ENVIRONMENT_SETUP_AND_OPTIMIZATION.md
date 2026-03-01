# Dev Environment Setup and Optimization — Docker, MCPs, Accounts

> **Purpose**: One-stop setup to optimize all dev activity across Cursor, Claude Code, Copilot, Codex. Covers Docker settings, MCP configuration, 1Password/accounts, and launch workflows.
>
> **Run**: `./scripts/setup-dev-environment.sh` for automated setup.

---

## 1. Quick Start (5 Minutes)

**One command**: `./scripts/login-accounts.sh`

Or step by step:

```bash
cd ~/.cursor/CURSOR\ CLOUD\ AGENTS

# 1. Index credentials from 1Password → .env.mcp
./scripts/agent-1password-index-env.sh

# 2. Validate MCP config, optionally install to ~/.cursor
./scripts/setup-mcp-with-1password.sh --install

# 3. Connect Docker MCP to Cursor (if Docker Desktop installed)
docker mcp client connect cursor

# 4. Launch Cursor with credentials injected
./scripts/launch-ai-with-op.sh cursor
```

See `docs/ACCOUNTS_LOGIN_PROCESS.md` for full stages and automations.

---

## 2. Docker Optimization

### 2.1 Docker Desktop Settings (Recommended)

| Setting                      | Value              | Why                                     |
| ---------------------------- | ------------------ | --------------------------------------- |
| **Resources > Memory**       | 6–8 GB             | MCP servers, build cache, containers    |
| **Resources > CPUs**         | 4+                 | Parallel builds, multi-container stacks |
| **Resources > Disk**         | 64 GB+             | Images, layers, MCP catalog             |
| **General > Start at login** | On                 | MCP_DOCKER requires Docker running      |
| **General > Use gRPC FUSE**  | On                 | Faster file sharing (macOS)             |
| **Docker Engine > BuildKit** | `"buildkit": true` | Faster, cache-aware builds              |

### 2.2 Docker MCP Gateway

The **MCP_DOCKER** server exposes Docker's MCP toolkit to Cursor. It provides additional servers (fetch, git, context7, brave, slack, etc.) from the Docker catalog.

| Command                             | Purpose                                                    |
| ----------------------------------- | ---------------------------------------------------------- |
| `./scripts/configure-docker-mcp.sh` | Full config: secrets + connect (recommended)               |
| `docker mcp client connect cursor`  | Connect Cursor to Docker MCP gateway                       |
| `docker mcp server ls`              | List available MCP servers in catalog                      |
| `docker mcp server enable <name>`   | Enable a specific server                                   |
| `docker mcp secret set`             | Configure secrets (or use Docker Desktop → Settings → MCP) |

See `docs/DOCKER_APPS_AND_MCP_BEST_PRACTICES.md` for all 21 Docker MCP servers and secret mapping.

### 2.3 Docker Config for Dev (daemon.json)

If using Docker Engine directly (no Desktop):

```json
{
  "builder": { "gc": { "enabled": true } },
  "experimental": false,
  "log-driver": "json-file",
  "log-opts": { "max-size": "10m", "max-file": "3" },
  "storage-driver": "overlay2"
}
```

### 2.4 Docker Hub Credentials

For private images, use `docker login` or store in 1Password:

| 1Password Item | Fields              | Usage                                                                       |
| -------------- | ------------------- | --------------------------------------------------------------------------- |
| Docker Hub     | username, pat_token | `op run --env-file=.env.mcp -- docker login -u $DOCKER_USER -p $DOCKER_PAT` |
| hub.docker.com | same                | GCR/ACR if needed                                                           |

Add to `.env.mcp.example`:

```
DOCKER_CONFIG=op://DevOps/Docker/config
```

---

## 3. MCP Configuration

### 3.1 Canonical MCP Servers (cursor-mcp-enhanced.json)

| Server           | Type    | Env Vars                                  | Purpose                        |
| ---------------- | ------- | ----------------------------------------- | ------------------------------ |
| **MCP_DOCKER**   | command | —                                         | Docker gateway; container MCPs |
| **supabase**     | url     | —                                         | Auth, DB, storage              |
| **codacy**       | npx     | —                                         | Code quality                   |
| **Auth0**        | url     | —                                         | Auth                           |
| **Agent Skills** | url     | —                                         | agentskills.io                 |
| **notion**       | npx     | NOTION_API_KEY                            | Wiki, case notes               |
| **linear**       | npx     | LINEAR_API_KEY                            | Projects, issues               |
| **github**       | npx     | GITHUB_PERSONAL_ACCESS_TOKEN              | Repos, PRs                     |
| **slack**        | npx     | SLACK_BOT_TOKEN                           | Comms                          |
| **postgres**     | npx     | POSTGRES_URL                              | Database                       |
| **brave_search** | npx     | BRAVE_API_KEY                             | Web search                     |
| **fetch**        | npx     | —                                         | HTTP fetch                     |
| **git**          | npx     | —                                         | Git ops                        |
| **neo4j**        | npx     | NEO4J_URI, NEO4J_USERNAME, NEO4J_PASSWORD | Knowledge graph                |
| **attio**        | url     | —                                         | CRM                            |
| **hubspot**      | url     | —                                         | CRM                            |
| **stripe**       | url     | —                                         | Payments                       |
| **airtable**     | npx     | AIRTABLE_API_KEY                          | Tables                         |
| **figma**        | url     | —                                         | Design                         |
| **firebase**     | npx     | FIREBASE_SERVICE_ACCOUNT                  | Auth, Firestore                |
| **greptile**     | url     | —                                         | Code context                   |
| **apify**        | npx     | APIFY_API_TOKEN                           | Web scraping                   |
| **huggingface**  | npx     | HF_TOKEN                                  | Models                         |

### 3.2 Install MCP Config to Cursor

```bash
./scripts/setup-mcp-with-1password.sh --install
```

Copies `config/mcp-servers/cursor-mcp-enhanced.json` → `~/.cursor/mcp.json`

### 3.3 Env Vars Required

All MCP env vars use `${VAR}` in config; values come from `.env.mcp` (op:// refs). Run:

```bash
./scripts/agent-1password-index-env.sh
```

Edit `config/mcp-servers/.env.mcp` if vault/item names differ from `MVP-Dev`.

---

## 4. Accounts & Credentials Flow

### 4.1 1Password → .env.mcp

```
1Password (op:// refs)
    ↓
./scripts/agent-1password-index-env.sh
    ↓
config/mcp-servers/.env.mcp
    ↓
op run --env-file=.env.mcp -- cursor
```

### 4.2 Account Categories (platform-connections.yaml)

| Category         | Apps                                     | Config               |
| ---------------- | ---------------------------------------- | -------------------- |
| **LLM**          | Anthropic, OpenAI, Google, Blackbox, xAI | blackbox-agents.yaml |
| **Search**       | Brave, DuckDuckGo                        | .env.mcp             |
| **Productivity** | Notion, Linear, Slack                    | .env.mcp             |
| **Storage**      | Supabase, Postgres, Neo4j, Box           | .env.mcp             |
| **CRM**          | Attio, HubSpot, Airtable                 | .env.mcp             |
| **Design**       | Figma                                    | .env.mcp             |
| **Dev**          | GitHub, Docker, Vercel                   | .env.mcp             |
| **Legal**        | Relativity, Everlaw, Clio                | connectors.yaml      |
| **Obsidian**     | OBSIDIAN_VAULT_PATH (local vault)        | .env.mcp.example     |

### 4.3 Add New Account

1. Create 1Password item (Vault: MVP-Dev or DevOps)
2. Add to `MCP_MAP` in `scripts/agent-1password-index-env.sh` if MCP needs it
3. Run `./scripts/agent-1password-index-env.sh`
4. Add to `config/mcp-servers/.env.mcp.example` for documentation

---

## 5. Launch Workflows

### 5.1 Cursor (Full MCP + LLM Keys)

```bash
./scripts/launch-ai-with-op.sh cursor
```

Or manually:

```bash
op run --env-file=config/mcp-servers/.env.mcp -- cursor
```

### 5.2 Claude Code

```bash
./scripts/launch-ai-with-op.sh claude
```

### 5.3 Codex CLI

```bash
./scripts/launch-ai-with-op.sh codex
```

### 5.4 Verify All Connections

```bash
op run --env-file=config/mcp-servers/.env.mcp -- ./scripts/verify-all-connections.sh
```

---

## 6. Files Reference

| File                                          | Purpose                                     |
| --------------------------------------------- | ------------------------------------------- |
| `config/mcp-servers/cursor-mcp-enhanced.json` | Canonical MCP server list                   |
| `config/mcp-servers/.env.mcp`                 | Generated; op:// refs (never commit)        |
| `config/mcp-servers/.env.mcp.example`         | Template with vault/item placeholders       |
| `config/platform-connections.yaml`            | Inventory; drives verify-all-connections    |
| `config/connectors.yaml`                      | Cloud, LLM, legal vendors                   |
| `~/.cursor/mcp.json`                          | Cursor's active MCP config (install target) |
| `scripts/agent-1password-index-env.sh`        | Index 1P → .env.mcp                         |
| `scripts/setup-mcp-with-1password.sh`         | Validate + install mcp.json                 |
| `scripts/launch-ai-with-op.sh`                | Launch tools with credentials               |
| `scripts/setup-dev-environment.sh`            | Full setup orchestration                    |

---

## 7. Troubleshooting

| Issue                    | Fix                                                                       |
| ------------------------ | ------------------------------------------------------------------------- |
| MCP server "not found"   | Ensure env var in .env.mcp; run `op run --env-file=.env.mcp -- true`      |
| MCP_DOCKER fails         | Docker Desktop running? `docker mcp client connect cursor`                |
| Linear/Notion 401        | Check LINEAR_API_KEY, NOTION_API_KEY in 1Password item                    |
| Neo4j connection refused | NEO4J_URI, NEO4J_USERNAME, NEO4J_PASSWORD; note: some MCPs use NEO4J_USER |
| Docker build slow        | Enable BuildKit; increase Resources in Docker Desktop                     |

---

_Maintain at: docs/DEV_ENVIRONMENT_SETUP_AND_OPTIMIZATION.md. Update when MCP servers or Docker config changes._
