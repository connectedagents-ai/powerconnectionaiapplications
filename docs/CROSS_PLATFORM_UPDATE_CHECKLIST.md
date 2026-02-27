# Cross-Platform Update Checklist

> **Purpose**: Ensure constitution, principles, rules, and architecture are propagated and verified across all repos, dev tools, LLMs, and agents.
>
> **Run after**: Any change to constitution, SUPER_DEVELOPER_PRINCIPLES, ALL_REPO_REVIEW, agent instructions (my-agent.agent.md, master-orchestrator), route script, or sync script.

---

## 1. Routed Repos (Constitution + Principles)

| Repo                          | Local Path                                    | Constitution           | Principles | Agent/Orchestrator                     | Sync Script |
| ----------------------------- | --------------------------------------------- | ---------------------- | ---------- | -------------------------------------- | ----------- |
| CURSOR CLOUD AGENTS           | (master)                                      | docs/constitution.md   | docs/      | .github/agents, .cursor/agents         | Source      |
| connected-agents-platform     | ~/Documents/connected-agents-platform         | agents/constitution.md | docs/      | my-agent.agent.md, master-orchestrator | ✅          |
| LitigationForce.AI            | ~/Documents/.../LitigationForce.AI            | docs/constitution.md   | docs/      | my-agent.agent.md, master-orchestrator | ✅          |
| file-management-toolkit       | ~/file-management-toolkit                     | docs/constitution.md   | docs/      | my-agent.agent.md, master-orchestrator | ✅          |
| powerconnectionaiapplications | ~/Documents/powerconnectionaiapplications     | docs/constitution.md   | docs/      | my-agent.agent.md, master-orchestrator | ✅          |
| slack-agent-template          | ~/.cursor/bootstrap-work/slack-agent-template | —                      | docs/      | my-agent.agent.md, master-orchestrator | ✅          |

**Verification**: `./scripts/sync-all-repos-and-review.sh --review`

---

## 2. Config Files (Must Stay in Sync)

| Config                                           | Purpose                               | Updated When                   |
| ------------------------------------------------ | ------------------------------------- | ------------------------------ |
| `scripts/route-constitution-to-repos.sh` ROUTES  | Constitution destinations             | New repo added                 |
| `scripts/sync-all-repos-and-review.sh` ALL_REPOS | Principles + bootstrap destinations   | New repo added                 |
| `config/routing-verification.yaml`               | Verify script references              | Constitution refs, child repos |
| `config/platform-connections.yaml`               | Replit, Lovable, LLM checks           | New platform                   |
| `config/connectors.yaml`                         | Connector definitions, repos          | New connector                  |
| `docs/CONSOLIDATION_AND_REPO_STATUS.md`          | Canonical map, merge status           | Repo changes                   |
| `docs/modules/` (LexVault, ontology, etc.)       | Reference patterns for new repos      | New module spec                |
| `docs/REFERENCE_PATTERNS_AND_EXAMPLE_REPOS.md`   | What new repos should emulate         | New example repo               |
| `docs/SOURCES_AND_EMULATION_INDEX.md`            | Top sources per action; virtuous loop | New action type; best practice |

---

## 3. Dev Tools & LLM Entry Points

| Tool               | Entry Point                           | Must Reference                           |
| ------------------ | ------------------------------------- | ---------------------------------------- |
| **Cursor**         | AGENTS.md, .cursor/rules/\*.mdc       | constitution, SUPER_DEVELOPER_PRINCIPLES |
| **Claude Code**    | CLAUDE.md, skills                     | constitution, agent-efficiency           |
| **GitHub Copilot** | .github/agents/my-agent.agent.md      | constitution                             |
| **Codex**          | Skills, system prompt                 | agent-efficiency, developer-enhancement  |
| **VS Code**        | .vscode/, Copilot instructions        | (if configured)                          |
| **Replit**         | replit-app/CLAUDE.md, Replit projects | constitution (if deployed)               |
| **Lovable**        | lovable.dev projects → export to repo | Constitution in exported repo            |
| **v0**             | v0.dev → copy to repo                 | —                                        |
| **Windsurf**       | Project instructions                  | —                                        |
| **Jules**          | Project instructions                  | —                                        |

**Verification**: `./scripts/verify-routing.sh`

---

## 4. Architecture & Design Docs

| Doc                                       | Purpose                     | Cross-Reference                             |
| ----------------------------------------- | --------------------------- | ------------------------------------------- |
| `docs/architecture.md`                    | System design               | SUPER_DEVELOPER_PRINCIPLES, ALL_REPO_REVIEW |
| `docs/CONSTITUTION_ROUTING_DESIGN.md`     | Routing design              | route-constitution, ROUTES                  |
| `docs/ALL_REPO_REVIEW.md`                 | Review protocol             | Scope table = sync script ALL_REPOS         |
| `docs/CROSS_PLATFORM_UPDATE_CHECKLIST.md` | Cross-platform verification | routing-verification.yaml, sync script      |
| `docs/SUPER_DEVELOPER_PRINCIPLES.md`      | Canonical principles        | SOURCES_REVIEWED, architecture              |
| `docs/SOURCES_REVIEWED.md`                | Repos/LLMs reviewed         | SUPER_DEVELOPER_PRINCIPLES                  |

---

## 5. Lovable & Replit Connection Checks

| Platform         | Config                                   | Env                      | Check                         |
| ---------------- | ---------------------------------------- | ------------------------ | ----------------------------- |
| **Replit**       | config/connectors.yaml vibe_code.replit  | REPLIT_API_KEY           | `[[ -n "$REPLIT_API_KEY" ]]`  |
| **Lovable**      | config/connectors.yaml vibe_code.lovable | LOVABLE_API_KEY          | `[[ -n "$LOVABLE_API_KEY" ]]` |
| **Hugging Face** | vibe_code.huggingface                    | HF_TOKEN                 | `[[ -n "$HF_TOKEN" ]]`        |
| **Vercel**       | applications.vercel                      | VERCEL_TOKEN             | `vercel whoami`               |
| **v0**           | vibe_code.v0                             | V0_API_KEY, VERCEL_TOKEN | —                             |

**Replit repos**: CURSOR-CLOUD-AGENTS, LitigationForce.AI, replit-app (per connectors.yaml)  
**Lovable repos**: marketing, nextjs-ai-chatbot

**Verification**: `python scripts/verify-all-connections.py`

---

## 6. Agents & MCP

| Category      | Config                                         | Verification                       |
| ------------- | ---------------------------------------------- | ---------------------------------- |
| Cursor agents | .cursor/agents/\*.md                           | platform-connections agents list   |
| Config agents | config/agents/\*.md                            | routing-verification config_agents |
| MCP servers   | config/mcp-servers/, platform-connections mcps | verify-all-connections mcps        |

---

## 7. Run All Verifications

```bash
# 1. Route constitution (writes to child repos)
./scripts/route-constitution-to-repos.sh

# 2. Sync all repos (principles, bootstrap)
./scripts/sync-all-repos-and-review.sh --review

# 3. Verify routing (constitution refs in master)
./scripts/verify-routing.sh

# 4. Verify all connections (platforms, MCPs, LLMs, routing)
python scripts/verify-all-connections.py --routing
# Or: ./scripts/run-all-verifications.sh --routing
```

---

## 8. GitHub Workflows

| Workflow               | Triggers                                                                                                                                                    | Verifies                                            |
| ---------------------- | ----------------------------------------------------------------------------------------------------------------------------------------------------------- | --------------------------------------------------- |
| verify-routing.yml     | constitution, rules, config/routing-verification.yaml, config/connectors.yaml, CROSS_PLATFORM_UPDATE_CHECKLIST, SUPER_DEVELOPER_PRINCIPLES, ALL_REPO_REVIEW | verify-routing.sh, verify-all-connections --routing |
| verify-connections.yml | platform config                                                                                                                                             | verify-all-connections                              |

---

_Maintain at: docs/CROSS_PLATFORM_UPDATE_CHECKLIST.md. Update when adding repos, tools, or config._
