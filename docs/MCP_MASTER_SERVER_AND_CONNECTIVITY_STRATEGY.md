# Master MCP Server and Automated Connectivity Strategy

> **Purpose**: Expanded and clarified strategy for the master MCP server, automated connectivity, and integrations across apps and APIs. Complements docs/MASTER_MCP_CONNECTORS_APIS.md and docs/mcp-router.md.  
> **Vision:** Our **master interconnected MCP server** (Connected OneWishMCP) is a core value proposition. Full plan: [MASTER_INTERCONNECTED_MCP_SERVER_AND_ONEWISHMCP_PLAN.md](MASTER_INTERCONNECTED_MCP_SERVER_AND_ONEWISHMCP_PLAN.md).

---

## 1. Master MCP Router Architecture

### 1.1 Single Entry Point

The **Master MCP Router** (`litigationforce_mcp_router`) is the single entry point for all MCP tool access. Agents never connect directly to 20+ individual MCP servers—they connect to the router, which:

1. **Discovers** actions by intent (progressive discovery)
2. **Fetches** schemas on demand (no context overload)
3. **Executes** against upstream servers with audit logging
4. **Guards** privilege (routes privileged content to private LLM only)

### 1.2 Key Capabilities

| Capability                | Purpose                                                               |
| ------------------------- | --------------------------------------------------------------------- |
| **Progressive discovery** | `discover_server_actions` → intent → ranked actions (no full schemas) |
| **Lazy schema fetch**     | `get_action_details` → schema only when needed                        |
| **Execute**               | `execute_action` → proxy to upstream MCP server                       |
| **Privilege guard**       | NEVER send potentially_privileged content to external LLM             |
| **Audit logging**         | Log discovery, schema fetch, execution, upstream server               |

### 1.3 Router Tools (Minimal Surface)

| Tool                      | Input                     | Output              |
| ------------------------- | ------------------------- | ------------------- |
| `discover_server_actions` | Intent (natural language) | Ranked action names |
| `get_action_details`      | Action name               | Schema, parameters  |
| `execute_action`          | Action + params           | Result              |
| `search_documentation`    | Query                     | Doc snippets        |

---

## 2. Automated Connectivity — How Integrations Are Wired

### 2.1 Credential Flow

```
1Password (op:// refs)
    ↓
.env.mcp or .env (never committed)
    ↓
scripts/agent-1password-index-env.sh (index → .env.mcp)
    ↓
MCP server config (env var names)
    ↓
Runtime: MCP server reads env; connects to API
```

- **Never** hardcode keys in config
- Use `op://vault/item/field` or `$ENV_VAR` references
- `.env.example` documents required vars; no values

### 2.2 Config Files That Drive Connectivity

| File                                 | Purpose                                  |
| ------------------------------------ | ---------------------------------------- |
| `config/connectors.yaml`             | Cloud, LLM, storage, legal vendors       |
| `config/platform-connections.yaml`   | 1Password audit; app→vault mapping       |
| `config/mcp-servers/master-mcp.yaml` | Master router; LLM routing; vendor tools |
| `config/mcp-servers/*.yaml`          | Per-server configs                       |
| Cursor/VSCode MCP JSON               | Which servers to load; stdio vs HTTP     |

### 2.3 Auto-Connect Scripts

| Script                           | What It Connects                 |
| -------------------------------- | -------------------------------- |
| `agent-1password-index-env.sh`   | 1Password items → .env.mcp       |
| `setup-mcp-with-1password.sh`    | Validate .env.mcp, MCP config    |
| `route-constitution-to-repos.sh` | Master → child repos             |
| `sync-all-repos-and-review.sh`   | Governance to all repos          |
| `verify-platform-connections.sh` | Platform + constitution + rules  |
| `verify-all-connections.sh`      | Full run: apps, MCPs, CLIs, LLMs |

---

## 3. Integration Matrix — Apps and APIs

### 3.1 LLM and AI

| Provider         | Env               | Config                  | Auto           |
| ---------------- | ----------------- | ----------------------- | -------------- |
| Anthropic        | ANTHROPIC_API_KEY | master-mcp, connectors  | Via MCP        |
| OpenAI           | OPENAI_API_KEY    | master-mcp external_llm | Via MCP        |
| Google/Gemini    | GOOGLE_API_KEY    | connectors, master-mcp  | Via MCP        |
| Blackbox         | BLACKBOX_API_KEY  | blackbox-agents.yaml    | Via MCP        |
| Ollama (private) | —                 | localhost:11434         | Privilege only |

### 3.2 Search and Research

| Tool         | Env                | MCP          |
| ------------ | ------------------ | ------------ |
| Brave Search | BRAVE_API_KEY      | brave_search |
| DuckDuckGo   | DDG_API_KEY        | —            |
| Perplexity   | PERPLEXITY_API_KEY | connectors   |

### 3.3 Productivity and Comms

| App    | Env             | MCP    | Purpose          |
| ------ | --------------- | ------ | ---------------- |
| Slack  | SLACK_BOT_TOKEN | slack  | Comms            |
| Notion | NOTION_API_KEY  | notion | Wiki, case notes |
| Linear | LINEAR_API_KEY  | linear | Projects, issues |
| Zoom   | ZOOM_API_KEY    | —      | Meetings         |

### 3.4 Storage and Database

| Service  | Env                 | MCP      | Purpose           |
| -------- | ------------------- | -------- | ----------------- |
| Supabase | SUPABASE\_\*        | supabase | Auth, DB, storage |
| Postgres | POSTGRES_URL        | postgres | Database          |
| Neo4j    | NEO4J*URI, NEO4J*\* | neo4j    | Knowledge graph   |
| Box      | BOX\_\*             | —        | LexVault storage  |
| AWS S3   | AWS\_\*             | —        | Storage           |

### 3.5 Legal and e-Discovery

| Vendor     | Config     | Purpose         |
| ---------- | ---------- | --------------- |
| Relativity | connectors | e-discovery     |
| Everlaw    | connectors | e-discovery     |
| Clio       | connectors | Case management |
| Spellbook  | connectors | Drafting        |
| Briefpoint | connectors | Drafting        |
| LexisNexis | connectors | Research        |

### 3.6 CRM and Workflow

| App      | Env              | MCP      |
| -------- | ---------------- | -------- |
| Attio    | URL/headers      | attio    |
| HubSpot  | URL-based        | hubspot  |
| Airtable | AIRTABLE_API_KEY | airtable |
| Stripe   | URL-based        | stripe   |

### 3.7 Development and Design

| Tool   | Env                          | MCP        |
| ------ | ---------------------------- | ---------- |
| GitHub | GITHUB_PERSONAL_ACCESS_TOKEN | github     |
| Git    | —                            | git        |
| Figma  | URL-based                    | figma      |
| Docker | —                            | MCP_DOCKER |

---

## 4. Automated Workflows

| Trigger              | Action                             | Integrations Used    |
| -------------------- | ---------------------------------- | -------------------- |
| **Pre-push**         | Constitution/routing changed       | Git; prompt sync     |
| **PR opened**        | verify-routing, verify-connections | GitHub Actions       |
| **Weekly**           | sync-all-repos-and-review          | Git; all child repos |
| **Linear issue**     | linear-to-repo-buildout            | Linear API; GitHub   |
| **Notion update**    | sync-notion-to-repo                | Notion API           |
| **1Password change** | agent-1password-index-env          | 1Password CLI        |
| **Agent task**       | Blackbox API, MCP tools            | Blackbox; MCP router |

---

## 5. Security and Privilege

| Rule                | Implementation                                                            |
| ------------------- | ------------------------------------------------------------------------- |
| **Privilege guard** | master-mcp privilege_guard: true                                          |
| **Private LLM**     | Ollama for privilege_scan, privilege_determination, attorney_client       |
| **Never external**  | Documents with privilege_status=potentially_privileged → private LLM only |
| **Audit**           | Log every private LLM call                                                |
| **OAuth2**          | MCP endpoint protected; WWW-Authenticate                                  |
| **Least privilege** | Session-verified tokens; tight scoping                                    |

---

## 6. Adding a New Integration

1. **1Password**: Add item; add to .env.mcp via agent-1password-index-env
2. **Connectors**: Add to config/connectors.yaml with env refs
3. **MCP server**: If MCP: add server config; add to Cursor MCP JSON
4. **Master MCP**: If tool: add to master-mcp vendors or tools
5. **Docs**: Update MASTER_MCP_CONNECTORS_APIS.md
6. **Verify**: Run verify-all-connections.sh

---

_Maintain at: docs/MCP_MASTER_SERVER_AND_CONNECTIVITY_STRATEGY.md. Update when integrations change._
