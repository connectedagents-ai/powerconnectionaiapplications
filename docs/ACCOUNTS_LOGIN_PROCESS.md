# Accounts Login Process — Stages and Automations

> **Purpose**: Canonical process for logging into platform accounts and preparing credentials for all dev tools. Run before sessions or when credentials change.
>
> **One command**: `./scripts/login-accounts.sh`

---

## Process Stages

| Stage           | Action                       | Script / Command                        | When                                   |
| --------------- | ---------------------------- | --------------------------------------- | -------------------------------------- |
| **1. Sign in**  | Unlock 1Password             | `op signin`                             | Session start, or when session expired |
| **2. Index**    | Map vault items → .env.mcp   | `agent-1password-index-env.sh`          | After adding items, or vault changes   |
| **3. Validate** | Resolve op:// refs           | `setup-mcp-with-1password.sh`           | After .env.mcp changes                 |
| **4. Install**  | Copy mcp.json to ~/.cursor   | `setup-mcp-with-1password.sh --install` | After MCP config changes               |
| **5. Connect**  | Docker MCP → Cursor          | `docker mcp client connect cursor`      | When Docker Desktop running            |
| **6. Launch**   | Start tools with credentials | `launch-ai-with-op.sh cursor`           | Before dev work                        |

---

## Quick Reference

```bash
# Full flow (one command)
./scripts/login-accounts.sh

# Or step by step
op signin
./scripts/agent-1password-index-env.sh
./scripts/setup-mcp-with-1password.sh --install
docker mcp client connect cursor   # if Docker running
./scripts/launch-ai-with-op.sh cursor
```

---

## Account Categories

| Category        | Examples                      | Stored In                    | Injected Via               |
| --------------- | ----------------------------- | ---------------------------- | -------------------------- |
| **1Password**   | GitHub, Notion, Slack, Linear | 1Password vaults             | op run --env-file=.env.mcp |
| **MCP servers** | Supabase, Neo4j, Postgres     | .env.mcp (op:// refs)        | Cursor reads at launch     |
| **LLM APIs**    | Anthropic, OpenAI, Google     | 1Password                    | launch-ai-with-op.sh       |
| **Cloud**       | AWS, GCP, Azure               | 1Password / service accounts | config/connectors.yaml     |

---

## Automations

### Session Start (Manual)

```bash
cd ~/.cursor/CURSOR\ CLOUD\ AGENTS
./scripts/login-accounts.sh
```

### Pre-Push (Existing)

Constitution/governance changes trigger `route-constitution-to-repos.sh` automatically.

### Weekly Sync

```bash
./scripts/sync-all-repos-and-review.sh
```

### After 1Password Changes

1. Run `./scripts/agent-1password-index-env.sh`
2. Restart Cursor (or run `launch-ai-with-op.sh cursor`)

---

## Troubleshooting

| Issue                   | Fix                                                                |
| ----------------------- | ------------------------------------------------------------------ |
| "Session expired"       | Run `op signin`                                                    |
| "MVP-Dev isn't a vault" | Update op:// refs in .env.mcp to match your vault names            |
| MCP server 401          | Check env var in .env.mcp; verify 1Password item has correct field |
| Docker MCP fails        | Start Docker Desktop; run `docker mcp client connect cursor`       |

---

## Files

| File                                   | Purpose                              |
| -------------------------------------- | ------------------------------------ |
| `scripts/login-accounts.sh`            | One-command login flow               |
| `scripts/agent-1password-index-env.sh` | Index 1P → .env.mcp                  |
| `scripts/setup-mcp-with-1password.sh`  | Validate + install mcp.json          |
| `scripts/launch-ai-with-op.sh`         | Launch tools with credentials        |
| `config/mcp-servers/.env.mcp`          | Generated; op:// refs (never commit) |

---

_Referenced by: UNIVERSAL_INSTRUCTIONS, MASTER_INDEX, DEV_ENVIRONMENT_SETUP_AND_OPTIMIZATION_
