# Marketing & Design Connections — Node.js, Figma, Framer, v0, Sentry, Canva, Marketing Dev

**Purpose:** Get **Node.js**, **Figma**, **Framer**, **v0**, **Sentry**, **Canva**, and **marketing dev environments** connected for CURSOR CLOUD AGENTS and OneWish OS. Use this after [BEGINNERS_GUIDE_INITIALIZE_SYSTEMS_AND_AGENTS.md](BEGINNERS_GUIDE_INITIALIZE_SYSTEMS_AND_AGENTS.md) Phase 4 (MCPs) and when working on voice-app, Framer sites, v0 UI, or design-to-code.

**Secrets / 1Password:** All keys below are in [MASTER_MCP_CONNECTORS_APIS.md](MASTER_MCP_CONNECTORS_APIS.md) and [MCP_SECRETS_REFERENCE.md](MCP_SECRETS_REFERENCE.md). Store in 1Password (e.g. MVP-Dev vault); reference in `config/mcp-servers/.env.mcp` via `op://VAULT/Item/field` or use Cursor MCP env.

**Related:** [UI_UX_AND_MARKETING_TURNKEY_GUIDE_SOURCES_AND_ORGANIZATION.md](UI_UX_AND_MARKETING_TURNKEY_GUIDE_SOURCES_AND_ORGANIZATION.md), [WEBAPPS_INVENTORY_AND_IMPLEMENT_IN_CONTEXT.md](WEBAPPS_INVENTORY_AND_IMPLEMENT_IN_CONTEXT.md), [ALL_AGENTS_LLMS_MCPS_AND_CONNECTIONS.md](ALL_AGENTS_LLMS_MCPS_AND_CONNECTIONS.md).

---

## 1. Summary: What’s Connected

| Connection        | Type      | Where configured                                   | 1Password / env                                           | Purpose                                                    |
| ----------------- | --------- | -------------------------------------------------- | --------------------------------------------------------- | ---------------------------------------------------------- |
| **Node.js / npm** | Runtime   | System PATH; `node -v`, `npm -v`                   | —                                                         | Run voice-app, npx MCPs (GitHub, Firecrawl)                |
| **Figma**         | MCP       | `.cursor/mcp.json` (project + user)                | URL-based (no key)                                        | Design context, Code Connect, design-to-code               |
| **Framer**        | API / env | `config/platform-connections.yaml`, `.env.mcp`     | `FRAMER_API_KEY` → op://MVP-Dev/Framer/api_key            | Marketing/landing sites                                    |
| **v0**            | App / env | platform-connections, V0_SETUP_AND_INSTRUCTIONS.md | `V0_API_KEY`, `VERCEL_TOKEN` → Vercel / v0                | UI generation; litigationforc1 v02; Custom Instructions    |
| **Vercel**        | CLI + env | platform-connections, `.env.mcp`                   | `VERCEL_TOKEN` → op://AI-LLM/Vercel-Claude-Key or MVP-Dev | Deploy voice-app, Next.js, v0                              |
| **Sentry**        | API / env | platform-connections, `.env.mcp`                   | `SENTRY_DSN`, `SENTRY_AUTH_TOKEN` → op://MVP-Dev/Sentry   | Error monitoring; Vercel + Sentry per app                  |
| **Canva**         | API / env | platform-connections, `.env.mcp`                   | `CANVA_ACCESS_TOKEN` → op://MVP-Dev/Canva/access_token    | Design, presentations; segment design export               |
| **GitHub**        | MCP       | `.cursor/mcp.json` + `.env.mcp`                    | `GITHUB_PERSONAL_ACCESS_TOKEN` → op://MVP-Dev/GitHub      | Repos, PRs, issues                                         |
| **Marketing app** | Next.js   | `marketing/voice-app/`                             | —                                                         | Talk to Alex; design system from FUNDAMENTAL_STRATEGIES §4 |
| **Voice agent APIs (plug-and-play)** | Env / 1Password | VoiceAgent.AI repo: `config/api-keys-and-login.yaml`, `.env.example` | `ELEVENLABS_API_KEY`, `VAPI_API_KEY`, `RETELL_API_KEY`, `BLAND_API_KEY`, `DEEPGRAM_API_KEY` → op://VoiceAgent/… | All voice apps, website voice widget, webapp, Replit; see VoiceAgent.AI [API_KEYS_AND_LOGIN_PLUG_AND_PLAY.md](https://github.com/.../voiceagent.ai/blob/main/docs/API_KEYS_AND_LOGIN_PLUG_AND_PLAY.md), [VOICE_AGENT_UI_UX_NEVER_MISS_DESIGN_RULES.md](https://github.com/.../voiceagent.ai/blob/main/docs/VOICE_AGENT_UI_UX_NEVER_MISS_DESIGN_RULES.md) |

---

## 2. Node.js

- **Required for:** `npm run dev` in `marketing/voice-app/`, `npx` for MCP servers (firecrawl-mcp, GitHub).
- **Check:**  
  `node -v` (e.g. 18+ or 20+)  
  `npm -v`  
  `npx -y @modelcontextprotocol/server-github --help` (optional).
- **Install:** [nodejs.org](https://nodejs.org/) or `nvm` / `fnm`; ensure `node` and `npx` are on PATH in the terminal Cursor uses.

---

## 3. Figma MCP

- **Configured in:**
  - **Project:** `CURSOR CLOUD AGENTS/.cursor/mcp.json` — `figma` with `url: "https://figma.com/mcp"`.
  - **User (global):** `~/.cursor/mcp.json` — same Figma entry if you use global MCPs.
- **Use:** In Cursor, share a Figma URL (e.g. `figma.com/design/...`); the agent can use Figma MCP for `get_design_context`, screenshots, Code Connect. See [v0-litigation-ui skill](.cursor/skills/v0-litigation-ui/SKILL.md) and [UI_UX_AND_MARKETING_TURNKEY_GUIDE](UI_UX_AND_MARKETING_TURNKEY_GUIDE_SOURCES_AND_ORGANIZATION.md) §1.2.
- **Verify:** Open Cursor → MCP / Integrations; Figma should show as connected. Or prompt: “Get design context for [Figma URL]”.
- **Platform config:** `config/platform-connections.yaml` lists `figma` under `mcps` (design; get_design_context, code_connect).

---

## 4. Framer (API / connector)

- **Not an MCP.** Framer is a platform for marketing/landing sites (onewish.io, litigationforce.com marketing, talk landing). Connection is via **API key** for automation/deploy.
- **Config:**
  - `config/platform-connections.yaml` → `applications.framer`: `FRAMER_API_KEY`.
  - `config/mcp-servers/.env.mcp.example`: `FRAMER_API_KEY=op://MVP-Dev/Framer/api_key`.
- **Setup:**
  1. Copy `.env.mcp.example` to `.env.mcp` and set `FRAMER_API_KEY` (or 1Password ref).
  2. Store the key in 1Password (e.g. MVP-Dev/Framer) and use `op run --env-file=config/mcp-servers/.env.mcp -- cursor .` so scripts and agents see it.
- **Verify:** `[[ -n "$FRAMER_API_KEY" ]]` or use Framer’s API (sites/projects) if you have automation that uses it.

---

## 5. Vercel (marketing dev / deploy)

- **Used for:** Deploying `marketing/voice-app/` (talk.litigationforce.com), Next.js marketing, and v0 deployments.
- **Config:**
  - `config/platform-connections.yaml` → `applications.vercel`: `VERCEL_TOKEN`.
  - `config/mcp-servers/.env.mcp.example`: `VERCEL_TOKEN=op://...`
- **Setup:**
  1. Add `VERCEL_TOKEN` to `.env.mcp` (or 1Password ref).
  2. Optionally: `npm i -g vercel` and `vercel login` so CLI works.
- **Verify:** `vercel whoami` or `[[ -n "$VERCEL_TOKEN" ]]`.

---

## 6. GitHub MCP

- **Configured in:** `CURSOR CLOUD AGENTS/.cursor/mcp.json` — `github` with `npx` and `GITHUB_PERSONAL_ACCESS_TOKEN`.
- **Env:** Set `GITHUB_PERSONAL_ACCESS_TOKEN` in `.env.mcp` (or Cursor MCP env) so the GitHub MCP can access repos. See [BEGINNER_SETUP_AFTER_AUDIT.md](audits/BEGINNER_SETUP_AFTER_AUDIT.md) Part B.
- **Verify:** In Cursor, run a prompt that uses GitHub (e.g. list issues, create branch); or `gh auth status` if using GitHub CLI.

---

## 7. v0 (Vercel UI generation)

- **Configured in:** `config/platform-connections.yaml` → `applications.v0`: `V0_API_KEY`, `VERCEL_TOKEN`. Canonical: `config/canonical-mcp-connectors.yaml` (1Password: Vercel / v0).
- **Setup:**
  1. Add `V0_API_KEY` and/or `VERCEL_TOKEN` to `.env.mcp` (see `.env.mcp.example`). v0 often accepts `VERCEL_TOKEN`.
  2. Paste **Custom Instructions** from [V0_SETUP_AND_INSTRUCTIONS.md](V0_SETUP_AND_INSTRUCTIONS.md) into v0 UI (≤2000 chars) for litigationforc1 v02.
  3. Use [v0-litigation-ui](.cursor/skills/v0-litigation-ui/SKILL.md) skill when building litigation UI with v0.
- **1Password:** Store in "Vercel / v0" or "Vercel"; map to `V0_API_KEY` or `VERCEL_TOKEN`. See [MCP_SECRETS_REFERENCE.md](MCP_SECRETS_REFERENCE.md) §4.
- **Verify:** `[[ -n "${V0_API_KEY:-$VERCEL_TOKEN}" ]]` or use v0 in browser with project linked to Vercel.

---

## 8. Sentry (error monitoring)

- **Configured in:** `config/platform-connections.yaml` → `applications.sentry`: `SENTRY_DSN`, `SENTRY_AUTH_TOKEN`. Canonical: `config/canonical-mcp-connectors.yaml` (1Password: Sentry).
- **Use:** Vercel + Sentry per app (see archived APPLICATIONS_AND_ARCHITECTURE). Add `SENTRY_DSN` to app env (e.g. voice-app, Litigation Swarm) for error reporting.
- **Setup:**
  1. Create project in [sentry.io](https://sentry.io); copy DSN and auth token.
  2. Add to `.env.mcp`: `SENTRY_DSN=op://MVP-Dev/Sentry/dsn`, `SENTRY_AUTH_TOKEN=op://MVP-Dev/Sentry/auth_token`.
  3. In app: `npm install @sentry/nextjs` (or SDK of choice); set `SENTRY_DSN` in Vercel env.
- **Verify:** `[[ -n "$SENTRY_DSN" ]]`.

---

## 9. Canva (design, presentations)

- **Configured in:** `config/platform-connections.yaml` → `applications.canva`: `CANVA_ACCESS_TOKEN`. Segment: `config/segment-lit-force-lexvault-connected.yaml` (design export_to). Canonical: `config/canonical-mcp-connectors.yaml` (1Password: Canva).
- **Use:** Design and presentations; export to `data/designs/canva`, `examples/presentations/canva` per segment config. See [GET_COMMITS_FROM_CLAUDE_CODE_AND_CODEX](playbooks/GET_COMMITS_FROM_CLAUDE_CODE_AND_CODEX.md) for pulling designs from Canva.
- **Setup:**
  1. Get access token from Canva (developer / API).
  2. Add to `.env.mcp`: `CANVA_ACCESS_TOKEN=op://MVP-Dev/Canva/access_token`.
  3. Store in 1Password item "Canva". See [MCP_SECRETS_REFERENCE.md](MCP_SECRETS_REFERENCE.md) §4 (Dev Apps).
- **Verify:** `[[ -n "$CANVA_ACCESS_TOKEN" ]]`.

---

## 10. Marketing dev app (voice-app)

- **Path:** `marketing/voice-app/` (Next.js).
- **Run locally:**
  ```bash
  cd marketing/voice-app
  npm install
  npm run dev   # http://localhost:3000
  ```
- **Design system:** Tokens in `app/globals.css` align with FUNDAMENTAL_STRATEGIES §4 and litigation-swarm-ui. See [WEBAPPS_INVENTORY_AND_IMPLEMENT_IN_CONTEXT.md](WEBAPPS_INVENTORY_AND_IMPLEMENT_IN_CONTEXT.md) §3.2.
- **Deploy:** Vercel; domain talk.litigationforce.com. Uses `VERCEL_TOKEN` from platform-connections.

---

## 11. One-command verification (optional)

From repo root, with `.env.mcp` and 1Password available:

```bash
cd ~/.cursor/CURSOR\ CLOUD\ AGENTS
./scripts/verify-all-connections.sh
```

This checks platform-connections (applications, MCPs, CLIs). For **Node/npm** and **Figma MCP** specifically:

- **Node:** `node -v && npm -v`
- **Figma:** Cursor MCP panel shows Figma connected when the project is open.

---

## 12. Checklist: Marketing & design connected

| #   | Item                                                                                                       | Done |
| --- | ---------------------------------------------------------------------------------------------------------- | ---- |
| 1   | Node.js and npm on PATH; `node -v` and `npm -v` ok                                                         | ☐    |
| 2   | `.env.mcp` created from `.env.mcp.example`; 1Password refs filled (see §1 table)                           | ☐    |
| 3   | Figma in `.cursor/mcp.json` (project or user); MCP shows connected in Cursor                               | ☐    |
| 4   | GitHub MCP in `.cursor/mcp.json`; `GITHUB_PERSONAL_ACCESS_TOKEN` set                                       | ☐    |
| 5   | `FRAMER_API_KEY` in `.env.mcp` if using Framer API                                                         | ☐    |
| 6   | `VERCEL_TOKEN` in `.env.mcp`; `vercel whoami` works if using CLI                                           | ☐    |
| 7   | **v0:** `V0_API_KEY` or `VERCEL_TOKEN` set; Custom Instructions from V0_SETUP_AND_INSTRUCTIONS.md in v0 UI | ☐    |
| 8   | **Sentry:** `SENTRY_DSN` (and optional `SENTRY_AUTH_TOKEN`) in 1Password + app env                         | ☐    |
| 9   | **Canva:** `CANVA_ACCESS_TOKEN` in `.env.mcp` if using Canva API / export                                  | ☐    |
| 10  | `marketing/voice-app`: `npm install && npm run dev` runs                                                   | ☐    |
| 11  | Optional: `op run --env-file=config/mcp-servers/.env.mcp -- cursor .` so MCPs get env                      | ☐    |

---

## 13. References

- **Master connector list:** [MASTER_MCP_CONNECTORS_APIS.md](MASTER_MCP_CONNECTORS_APIS.md)
- **Secrets & 1Password:** [MCP_SECRETS_REFERENCE.md](MCP_SECRETS_REFERENCE.md)
- **Full inventory:** [ALL_AGENTS_LLMS_MCPS_AND_CONNECTIONS.md](ALL_AGENTS_LLMS_MCPS_AND_CONNECTIONS.md)
- **Platform config:** `config/platform-connections.yaml`; **canonical:** `config/canonical-mcp-connectors.yaml`
- **Env template:** `config/mcp-servers/.env.mcp.example`
- **Webapps & design system:** [WEBAPPS_INVENTORY_AND_IMPLEMENT_IN_CONTEXT.md](WEBAPPS_INVENTORY_AND_IMPLEMENT_IN_CONTEXT.md), [UI_UX_AND_MARKETING_TURNKEY_GUIDE_SOURCES_AND_ORGANIZATION.md](UI_UX_AND_MARKETING_TURNKEY_GUIDE_SOURCES_AND_ORGANIZATION.md)
- **v0:** [V0_SETUP_AND_INSTRUCTIONS.md](V0_SETUP_AND_INSTRUCTIONS.md)
