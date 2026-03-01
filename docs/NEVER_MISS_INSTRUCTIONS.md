# Never-Miss Instructions — Tools, Sequence, Sync, Push, Single Source of Truth

**Purpose:** One place that defines (1) **which tools we use** per the constitution, (2) **how, when, and for what** to use each script and config, (3) the **exact sequence** (sync → route → verify → review → commit → push), and (4) **single point of truth**: all dev tools (Cursor, Claude Code, Codex, etc.) commit to the **master repo** on GitHub; files live in proper locations; sync propagates to child repos.

**Governance:** Constitution §8, §8.5; [ONEWISH_PROTOCOL.md](ONEWISH_PROTOCOL.md) §5; [MCP_CONNECTOR_SYNC_AND_TRIGGER.md](MCP_CONNECTOR_SYNC_AND_TRIGGER.md). **Run the sequence below** after governance change, connector add/remove, repo change, or before commit. **Never skip a target.**

---

## 1. Tools per constitution (what we use)

The **constitution for connected tools** is the **canonical registry**: `config/canonical-mcp-connectors.yaml`. Only tools listed there are approved for platform-connections, MCP configs, and prebuilt-agent lists. No tool is added anywhere unless it is in the canonical registry first.

| Source | Purpose |
|--------|--------|
| **config/canonical-mcp-connectors.yaml** | Single source of truth for MCPs, connectors, LLMs, applications we officially connect. Add here only; then run sync. |
| **config/platform-connections.yaml** | Applications, MCPs, LLMs used by verify-all-connections and scripts. Synced from canonical; may have additional entries for local verification. |
| **config/repos.yaml** | ROUTES and all_repos — which repos receive governance and full sync. Single source for sync targets. |
| **docs/DEV_TOOLS_CANONICAL_LIST_AND_AUDIT.md** | All 9 dev tools (Cursor, Claude Code, Copilot, Codex, v0, VS Code, Windsurf, Warp, Goose). No-fail audit; never omit one. |

**Dev tools (all on same level):** Cursor, Claude Code, GitHub Copilot, Codex, v0, VS Code/Extensions, Windsurf, Warp, Goose. Each gets same governance, entry points, and ability to run any OneWish OS script. See [DEV_TOOLS_CANONICAL_LIST_AND_AUDIT.md](DEV_TOOLS_CANONICAL_LIST_AND_AUDIT.md).

---

## 2. When to use each tool (what for)

| Use case | Tool / script | When |
|----------|----------------|------|
| **Add or remove an MCP/connector** | Edit `config/canonical-mcp-connectors.yaml` only | When adding a new integration. Never add to platform-connections or elsewhere first. |
| **Propagate canonical → all configs** | `python3 scripts/sync-canonical-mcp-connectors.py` | Immediately after editing canonical-mcp-connectors.yaml. |
| **Push governance to ROUTES repos** | `./scripts/route-constitution-to-repos.sh` | After constitution, checklist, universal, or bootstrap change; before commit if governance changed. |
| **Sync master files to all repos** | `./scripts/sync-all-repos-and-review.sh` | After doc/config change that should reach children; weekly; before commit when master files changed. |
| **Refresh workspace for all dev tools** | `./scripts/sync-dev-tools-repos-from-config.sh` | After adding a repo to config/repos.yaml; when Claude Code/Codex need same roots. |
| **Verify connections (env/keys)** | `./scripts/verify-all-connections.sh` | After adding MCP/connector; optional in Full Review. |
| **Full Review (mandatory checklist)** | `./scripts/run-full-review.sh` | Before commit; when changing/merging repos; quarterly; on demand. Complete checklist in docs/audits/full-review-summary.md. |
| **One-shot: route + sync + workspace + Full Review** | `./scripts/connect-and-configure-onewishos.sh` | After adding repo/MCP/connector; when ensuring no target missed. |
| **Audit runbook (route + sync + workspace + Full Review)** | `./scripts/run-audit-runbook.sh` | Same as connect-and-configure; alternate entry point. |

---

## 3. Never-miss sequence (in order)

Run in this order so no target is skipped. From **any** connected dev tool (Cursor, Claude Code, Codex, etc.): open the **master repo** (CURSOR CLOUD AGENTS) or `onewish-repos.code-workspace`, then in terminal:

```
1. (If you changed MCP/connector list)
   Edit config/canonical-mcp-connectors.yaml only.
   python3 scripts/sync-canonical-mcp-connectors.py

2. Route governance to ROUTES
   ./scripts/route-constitution-to-repos.sh

3. Sync all repos (master → all_repos)
   ./scripts/sync-all-repos-and-review.sh

4. Refresh dev-tools workspace
   ./scripts/sync-dev-tools-repos-from-config.sh

5. (Optional) Verify connections
   ./scripts/verify-all-connections.sh

6. Full Review
   ./scripts/run-full-review.sh

7. Complete mandatory checklist
   Open docs/audits/full-review-summary.md and complete every item.

8. Commit and push (see §4)
   All changes committed in master repo; push to GitHub. Then child repos if they have their own remotes.
```

**Shortcut:** Steps 2–6 in one go: `./scripts/connect-and-configure-onewishos.sh` (then do 7 and 8).

---

## 4. Single point of truth — GitHub and proper locations

**Master repo = single source of truth.** The **CURSOR CLOUD AGENTS** repo (master) is the single point of truth for:

- Constitution, protocol, MASTER_INDEX, entry-point docs
- config/canonical-mcp-connectors.yaml, config/repos.yaml, config/platform-connections.yaml
- All scripts (route-constitution, sync-all-repos, connect-and-configure, run-full-review, etc.)
- docs/, .cursor/rules, .cursor/agents, .github/agents

**All dev tools commit to master first.** Whether you use Cursor, Claude Code, Codex, or any other connected dev tool:

1. **Work in the master repo** (or a child repo only when that repo is the correct owner of the change).
2. **Save and commit in the correct location:**  
   - Governance and platform-wide config → master repo (`CURSOR CLOUD AGENTS`).  
   - Project-specific code/docs that belong to a child repo → that child repo (e.g. LitigationForce.AI, file-management-toolkit).
3. **Push master to GitHub** so the canonical state is in version control. Paths: `config/`, `docs/`, `scripts/`, `.cursor/`, `.github/` in the master repo root.
4. **After pushing master,** run the never-miss sequence (at least route + sync) so child repos receive the updates. Child repos that have their own GitHub remotes: commit and push those after sync has copied files from master.

**Proper locations (master repo):**

| Content | Location in master |
|--------|---------------------|
| Canonical MCP/connector list | config/canonical-mcp-connectors.yaml |
| Repo list (ROUTES, all_repos) | config/repos.yaml |
| Platform connections (apps, MCPs, LLMs) | config/platform-connections.yaml |
| Connector definitions | config/connectors.yaml |
| Master MCP server config | config/mcp-servers/master-mcp.yaml |
| Constitution, protocol, indexes | docs/constitution.md, docs/ONEWISH_PROTOCOL.md, docs/MASTER_INDEX.md |
| Never-miss and cross-tool docs | docs/NEVER_MISS_INSTRUCTIONS.md, docs/ONEWISHOS_CROSS_TOOL_AND_FULL_INVENTORY.md |
| Sync script | scripts/sync-all-repos-and-review.sh |
| Route script | scripts/route-constitution-to-repos.sh |
| Connect-and-configure | scripts/connect-and-configure-onewishos.sh |
| Entry points (Cursor) | .cursor/rules/*.mdc, AGENTS.md |
| Entry points (Claude Code) | CLAUDE.md |
| Agent spec | .github/agents/my-agent.agent.md |

**Child repos** receive copies via sync; they do not edit canonical lists. Edits to governance or platform-wide config are made in **master only**, then propagated by route and sync.

---

## 5. Triggers (when to run the sequence)

| Trigger | Run |
|--------|-----|
| **Governance change** (constitution, checklist, universal, bootstrap) | route-constitution → sync-all-repos → Full Review → commit → push master |
| **Add/remove MCP or connector** | Edit canonical only → sync-canonical-mcp-connectors.py → connect-and-configure-onewishos.sh → commit → push master |
| **Add/remove repo** | Edit config/repos.yaml → route-constitution → sync-all-repos → sync-dev-tools-repos-from-config → Full Review → commit → push master |
| **Before commit** (any change in master) | Full Review + mandatory checklist; then commit; then push master to GitHub |
| **Weekly / recurring** | sync-all-repos-and-review.sh; optionally Full Review |
| **Quarterly** | Full pass: constitution, MASTER_INDEX, CONSOLIDATION, Full Review, sources compare; commit and push master |

---

## 6. Cross-references

| Doc | Purpose |
|-----|--------|
| [ONEWISH_PROTOCOL.md](ONEWISH_PROTOCOL.md) §5 | Never-miss propagation; targets and protocol data |
| [MCP_CONNECTOR_SYNC_AND_TRIGGER.md](MCP_CONNECTOR_SYNC_AND_TRIGGER.md) | Add to canonical only; sync trigger; constitution rule for connectors |
| [ONEWISHOS_CROSS_TOOL_AND_FULL_INVENTORY.md](ONEWISHOS_CROSS_TOOL_AND_FULL_INVENTORY.md) | Cross-tool execution; full inventory; scripts that connect/configure |
| [audits/artifacts/README.md](audits/artifacts/README.md) | Never-miss sync flow diagram; push/sync summaries |
| [audits/full-review-summary.md](audits/full-review-summary.md) | Mandatory checklist after Full Review |
| [MASTER_FILE_COMMIT_REVIEW_AND_FINAL_DECISION_SYSTEM.md](MASTER_FILE_COMMIT_REVIEW_AND_FINAL_DECISION_SYSTEM.md) | After commit to master: retroactive review (Claude Code, Cursor, Codex); gather; rerun; Claude Code final decisions on OneWish OS |
| [DEV_TOOLS_CANONICAL_LIST_AND_AUDIT.md](DEV_TOOLS_CANONICAL_LIST_AND_AUDIT.md) | All 9 dev tools; no-fail audit |

_Maintain at: docs/NEVER_MISS_INSTRUCTIONS.md. Update when adding scripts, triggers, or locations._
