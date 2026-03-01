# OneWish OS — Pro Response & Execution Brief

**Purpose:** Use this to respond like a pro when another AI (or a human) has explored the repo and needs (1) **clarification** on NextTech OS / OneWish OS, and (2) a **single ordered execution plan** that matches the repo’s scripts and docs. Also for syncing with Cursor session context.

**Audience:** Claude Code, Cursor, or any agent that has done a “deep read” of CURSOR-CLOUD-AGENTS and needs to align with the real playbooks.

---

## 1. Clarify “NextTech OS” / “nextechos”

**NextTech OS** is not a separate repo or product name. It is the **user-facing layer** of the same system:

- **OneWish OS** = the top (this repo: **CURSOR CLOUD AGENTS**). Single source of truth: constitution, agents, config, sync scripts.
- **NextTech OS** = the **user-facing** instance of that. All users connect through NextTech OS. It exposes the same architecture and the same sub-OSes (LitigationForce.AI, PowerConnection, file-management, etc.).
- **Sub-OSes** = LitForce OS, FamilyOfficeOS, PowerConnection.AI OS, etc. — each a sub-repo with the **same** architecture (governance, sync, agents, MCPs).

**References:**  
`docs/ONEWISHOS_CRYSTAL_CLEAR_ARCHITECTURE_AND_AGENT_TAXONOMY.md` (diagram: OneWish OS → NextTech OS → sub-OSes).  
`docs/COMPLETE_REVIEW_ONEWISH_NEXTTECH_LITIGATIONFORCE_AND_LAUNCH.md` (NextTech OS = user-facing; not “NexTech.io”).  
`docs/NEXTTECH_OS_INSTRUCTIONS_FOR_ALL_USERS.md` (playbook for all users; master-authored, one-way).

**In one sentence:** NextTech OS is the user-facing layer of OneWish OS; both live in **CURSOR CLOUD AGENTS** and the child repos it syncs to.

---

## 2. Your diagnosis is right — here’s the OneWish OS frame

What you found is correct:

- **Master repo** = CURSOR-CLOUD-AGENTS (OneWish OS). No repo named “onewishagentsos.”
- **Canonical four** = CURSOR-CLOUD-AGENTS, LitigationForce.AI, connected-agents-platform, file-management-toolkit (plus others in `config/repos.yaml`).
- **The mess** = multiple GitHub accounts, duplicate/redundant repos, dev tools (Cursor, Claude Code, Codex, etc.) not all opening the same workspace or running the same sync.

The **OneWish OS** way to say it: single source of truth is the **master repo**; **never-miss propagation** (route constitution + sync-all-repos + workspace from config) is in `docs/ONEWISH_PROTOCOL.md` §5 and in the scripts below.

---

## 3. One ordered execution plan (match the repo)

Use this order. Everything is run from the **master repo** root (`CURSOR CLOUD AGENTS`), e.g.  
`cd ~/.cursor/CURSOR\ CLOUD\ AGENTS` (or your actual path).

| Step  | Action                                               | Command / doc                                                                                                                                                                                                                                                                                                                                       |
| ----- | ---------------------------------------------------- | --------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| **1** | **See/sync as Claude Code**                          | Read `docs/CLAUDE_CODE_ONEWISHOS_SYNC_AND_VISIBILITY.md`. Open **this folder** or `onewish-repos.code-workspace` in Claude Code. Run from master: `./scripts/sync-dev-tools-repos-from-config.sh` then `./scripts/connect-and-configure-onewishos.sh --connections-optional`.                                                                       |
| **2** | **Route constitution to all repos**                  | `./scripts/route-constitution-to-repos.sh` — sends governance to ROUTES (see `config/repos.yaml`).                                                                                                                                                                                                                                                  |
| **3** | **Sync all repos (docs + propagation)**              | `./scripts/sync-all-repos-and-review.sh` — copies MASTER_INDEX, ALL_AGENTS_LLMS_MCPS_AND_CONNECTIONS, CLAUDE_CODE_ONEWISHOS_SYNC_AND_VISIBILITY, and other §6a docs to every repo in `all_repos`.                                                                                                                                                   |
| **4** | **Verify platform connections**                      | `./scripts/verify-all-connections.sh` (or `--connections-optional` if env/1Password not fully populated). Config: `config/platform-connections.yaml`.                                                                                                                                                                                               |
| **5** | **Full Review (mandatory checklist)**                | `./scripts/run-full-review.sh` — then **complete** the mandatory checklist in `docs/audits/full-review-summary.md`. Full Review is not done until that checklist is done.                                                                                                                                                                           |
| **6** | **GitHub merge/archive (cleanup)**                   | Follow `docs/GITHUB_ORGANIZE_SIMPLIFY_NAMING_ARCHIVE_AND_INTEGRATE.md` and any existing merge plan (e.g. REPO_SIMILARITY_AND_MERGE_PLAN). Use scripts you have for merge/archive; consolidate to **connectedagents-ai** as canonical.                                                                                                               |
| **7** | **Aggregated data / agents / instructions / skills** | Master list of agents, LLMs, MCPs: `docs/ALL_AGENTS_LLMS_MCPS_AND_CONNECTIONS.md`. Master list of MCP/connectors and 1Password: `docs/MASTER_MCP_CONNECTORS_APIS.md`. Entry point for all docs: `docs/MASTER_INDEX.md`. Add new MCPs/connectors via `config/canonical-mcp-connectors.yaml` then `python3 scripts/sync-canonical-mcp-connectors.py`. |

**One command that does 2–4 (baseline sync + verify):**  
`./scripts/connect-and-configure-onewishos.sh --connections-optional`

---

## 4. Syncing with “logs from Cursor”

If you mean **Cursor session logs or conversation history**:

- Cursor stores project/session state under `~/.cursor/` (e.g. projects, agent transcripts). There is no single “log file” the repo scripts read.
- To **align** another AI (e.g. Claude Code) with what Cursor has: (1) Open the **same** root in both — the **master repo** or `onewish-repos.code-workspace` (generated by `./scripts/sync-dev-tools-repos-from-config.sh`). (2) Run the sync steps above so both see the same docs (MASTER_INDEX, ALL_AGENTS, CLAUDE_CODE_ONEWISHOS_SYNC_AND_VISIBILITY, etc.). (3) Point the other AI at this brief and at `docs/CLAUDE_CODE_ONEWISHOS_SYNC_AND_VISIBILITY.md` so it uses the same plan.

If you mean **run logs / verification output**:

- Full Review writes to `scripts/.full-review-last.log` and `docs/audits/full-review-summary.md`. Sharing that summary (or the log path) gives another AI the “last run” state.

---

## 5. Copy-paste “pro response” you can send

You can send something like this (e.g. to the other AI or into a ticket):

```
NextTech OS = the user-facing layer of OneWish OS (same system). Both live in CURSOR-CLOUD-AGENTS; there is no separate "nextechos" repo. See docs/ONEWISHOS_CRYSTAL_CLEAR_ARCHITECTURE_AND_AGENT_TAXONOMY.md and docs/COMPLETE_REVIEW_ONEWISH_NEXTTECH_LITIGATIONFORCE_AND_LAUNCH.md.

Your diagnosis is right. Use this execution order from the master repo root:

1. Claude Code: read docs/CLAUDE_CODE_ONEWISHOS_SYNC_AND_VISIBILITY.md; open this folder or onewish-repos.code-workspace; run sync-dev-tools-repos-from-config.sh then connect-and-configure-onewishos.sh --connections-optional.
2. route-constitution-to-repos.sh
3. sync-all-repos-and-review.sh
4. verify-all-connections.sh (or --connections-optional)
5. run-full-review.sh → complete the mandatory checklist in docs/audits/full-review-summary.md
6. GitHub cleanup per GITHUB_ORGANIZE_SIMPLIFY_NAMING_ARCHIVE_AND_INTEGRATE.md and any merge plan
7. Agents/MCPs/connections: docs/ALL_AGENTS_LLMS_MCPS_AND_CONNECTIONS.md + docs/MASTER_MCP_CONNECTORS_APIS.md; add via config/canonical-mcp-connectors.yaml + sync-canonical-mcp-connectors.py

Single baseline command: ./scripts/connect-and-configure-onewishos.sh --connections-optional

Full brief: docs/ONEWISHOS_PRO_RESPONSE_AND_EXECUTION_BRIEF.md (this file).
```

---

## 6. References

| Doc                                                                                                                              | Purpose                                   |
| -------------------------------------------------------------------------------------------------------------------------------- | ----------------------------------------- |
| [ONEWISHOS_CRYSTAL_CLEAR_ARCHITECTURE_AND_AGENT_TAXONOMY.md](ONEWISHOS_CRYSTAL_CLEAR_ARCHITECTURE_AND_AGENT_TAXONOMY.md)         | OneWish OS → NextTech OS → sub-OSes       |
| [CLAUDE_CODE_ONEWISHOS_SYNC_AND_VISIBILITY.md](CLAUDE_CODE_ONEWISHOS_SYNC_AND_VISIBILITY.md)                                     | Claude Code see/sync plan                 |
| [NEXTTECH_OS_INSTRUCTIONS_FOR_ALL_USERS.md](NEXTTECH_OS_INSTRUCTIONS_FOR_ALL_USERS.md)                                           | NextTech OS playbook (all users)          |
| [COMPLETE_REVIEW_ONEWISH_NEXTTECH_LITIGATIONFORCE_AND_LAUNCH.md](COMPLETE_REVIEW_ONEWISH_NEXTTECH_LITIGATIONFORCE_AND_LAUNCH.md) | NextTech OS = user-facing                 |
| [MASTER_INDEX.md](MASTER_INDEX.md)                                                                                               | Entry point for all docs                  |
| [ALL_AGENTS_LLMS_MCPS_AND_CONNECTIONS.md](ALL_AGENTS_LLMS_MCPS_AND_CONNECTIONS.md)                                               | Full inventory (agents, LLMs, MCPs, apps) |
| [ONEWISH_PROTOCOL.md](ONEWISH_PROTOCOL.md)                                                                                       | §5 never-miss propagation                 |
| [config/repos.yaml](../config/repos.yaml)                                                                                        | ROUTES, all_repos                         |

---

_Maintain at: docs/ONEWISHOS_PRO_RESPONSE_AND_EXECUTION_BRIEF.md._
