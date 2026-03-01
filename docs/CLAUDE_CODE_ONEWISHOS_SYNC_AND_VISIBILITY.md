# Claude Code — See and Sync with OneWish OS (Systematic Plan)

**Purpose:** So **Claude Code** can **see** OneWish OS and **sync up** with it every time. Follow this plan in order; it is the single place that defines how Claude Code and OneWish OS connect.

**Who this is for:** Claude Code (and any dev tool) that needs to discover the master repo, open the right folder/workspace, and run the right scripts to be "synced" with OneWish OS.

**Related:** [CLAUDE_CODE_AND_CLAUDE_AI_INTEGRATION_BEGINNER.md](CLAUDE_CODE_AND_CLAUDE_AI_INTEGRATION_BEGINNER.md), [DEV_TOOLS_REPO_ALIGNMENT.md](DEV_TOOLS_REPO_ALIGNMENT.md), [ONEWISH_PROTOCOL.md](ONEWISH_PROTOCOL.md) §5 (never-miss propagation).

---

## 1. What OneWish OS is (and what it is not)

- **OneWish OS** = the **master repo**: **CURSOR CLOUD AGENTS**. There is **no** separate GitHub repo or folder named "onewishagentsos" or "OneWishAgentsOS".
- **Same thing:** OneWish OS, OneWish Agents OS, NextTech OS (user-facing), and this repo (**CURSOR CLOUD AGENTS**) are the **same** master. Child repos (LitigationForce.AI, connected-agents-platform, file-management-toolkit, etc.) are listed in `config/repos.yaml` and receive governance and docs from the master via sync scripts.

**If you are Claude Code and you are in a child repo (e.g. LitigationForce.AI):** The master is the **parent** in the OneWish layout. Typical paths:

- Master on Mac: `~/.cursor/CURSOR CLOUD AGENTS` or `~/Documents/.../CURSOR-CLOUD-AGENTS` (or wherever the repo is cloned).
- This doc is **synced into every child repo** as `docs/CLAUDE_CODE_ONEWISHOS_SYNC_AND_VISIBILITY.md`, so you can read it from any repo and then open the master path for your machine.

---

## 2. The plan (do these in order)

### Step 1 — Find the master repo path

- **If you are already in the master repo (CURSOR CLOUD AGENTS):** The current directory (project root) **is** the OneWish OS root. Use it as `MASTER_PATH` in steps below.
- **If you are in a child repo:** You need the **absolute path** to the master. Check:
  - `config/repos.yaml` in the **master** has `master: "."` and `all_repos` with paths **relative to master**. So the master is the folder that **contains** `config/repos.yaml` with that content.
  - On a typical Mac, master is often:  
    `$HOME/.cursor/CURSOR CLOUD AGENTS`  
    or  
    `$HOME/Documents/CURSOR-CLOUD-AGENTS`
  - Set it once:  
    `export MASTER_PATH="$HOME/.cursor/CURSOR CLOUD AGENTS"`  
    (replace with your actual path if different).

### Step 2 — Open the right folder in Claude Code

To **see** OneWish OS, Claude Code must have the **master repo** (or the multi-repo workspace) open.

1. **Option A (recommended):** Open the **workspace file** so all OneWish repos appear in one place:
   - From terminal: `cd "$MASTER_PATH"` then run `./scripts/sync-dev-tools-repos-from-config.sh` (generates or updates `onewish-repos.code-workspace`).
   - In Claude Code: **File → Open Workspace from File** → choose `onewish-repos.code-workspace` from the master repo root.
2. **Option B:** Open only the master folder:
   - In Claude Code: **File → Open Folder** → choose the **CURSOR CLOUD AGENTS** folder (your `MASTER_PATH`).
   - Or from terminal: `cd "$MASTER_PATH"` then `claude .`

**Do not** open a random or one-off folder (e.g. "New project") as your primary space; Claude Code will not see OneWish OS.

### Step 3 — Sync up (run the OneWish OS sync)

"Synced up" means: (a) governance and docs are **routed/synced** from master to all child repos, and (b) the **workspace** includes all canonical repos. Run these from the **master repo** root (`$MASTER_PATH`).

**Push to Claude Code and Codex (script):** To sync then optionally **launch** Claude Code or **print** Codex commands so both tools see the latest context, run from master:  
`./scripts/push-to-claude-code-and-codex.sh` (sync only),  
`./scripts/push-to-claude-code-and-codex.sh --launch` (sync + open Claude Code in master),  
`./scripts/push-to-claude-code-and-codex.sh --codex` (sync + print Codex run commands),  
or `--launch --codex` for both. There is no API to inject into Claude Code/Codex; "push" = update files on disk then open/run in the right folder so they read CLAUDE.md and docs.

1. **Generate the workspace** (so all repos are visible in one workspace):
   ```bash
   cd "$MASTER_PATH"
   ./scripts/sync-dev-tools-repos-from-config.sh
   ```
2. **Run the full OneWish OS connect-and-configure** (route constitution → sync all repos → optional connection checks):

   ```bash
   cd "$MASTER_PATH"
   ./scripts/connect-and-configure-onewishos.sh --connections-optional
   ```

   This runs: route-constitution → sync-all-repos-and-review → refresh workspace → optional verify connections. After it finishes, complete the checklist in `docs/audits/full-review-summary.md` when you are ready.

3. **Optional one-command from any connected tool:** From any dev tool that can run a shell in the master repo:
   ```bash
   cd "$MASTER_PATH" && ./scripts/connect-and-configure-onewishos.sh --connections-optional
   ```

### Step 4 — Confirm you are synced

- **You see OneWish OS** when: You have the **CURSOR CLOUD AGENTS** folder (or `onewish-repos.code-workspace`) open in Claude Code and you can read `CLAUDE.md`, `docs/MASTER_INDEX.md`, and `config/repos.yaml` from the project.
- **You are synced up** when: You have run `sync-dev-tools-repos-from-config.sh` and `connect-and-configure-onewishos.sh` (or `sync-all-repos-and-review.sh`) from the master so that child repos have the latest governance and docs.

---

## 3. Quick reference (copy-paste)

```bash
# 1. Set master path (Mac, typical)
export MASTER_PATH="$HOME/.cursor/CURSOR CLOUD AGENTS"

# 2. Go to master and generate workspace
cd "$MASTER_PATH"
./scripts/sync-dev-tools-repos-from-config.sh

# 3. Open Claude Code in master (or open onewish-repos.code-workspace in Claude Code)
claude .

# 4. Full sync (route + sync all repos)
./scripts/connect-and-configure-onewishos.sh --connections-optional
```

---

## 4. Where things live (per OneWish OS)

| What                            | Where                                                              |
| ------------------------------- | ------------------------------------------------------------------ |
| **Master repo**                 | CURSOR CLOUD AGENTS (this repo). Path: set `MASTER_PATH` as above. |
| **Repo list**                   | `config/repos.yaml` → `all_repos`, `routes`.                       |
| **Entry point for Claude Code** | `CLAUDE.md` in master root.                                        |
| **Doc index**                   | `docs/MASTER_INDEX.md`.                                            |
| **Sync script (all repos)**     | `./scripts/sync-all-repos-and-review.sh` (run from master).        |
| **Workspace generator**         | `./scripts/sync-dev-tools-repos-from-config.sh` (run from master). |
| **Connect + configure**         | `./scripts/connect-and-configure-onewishos.sh` (run from master).  |

---

## 5. If Claude Code still doesn’t see or sync

| Problem                | What to do                                                                                                                                                                                        |
| ---------------------- | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| "Where is OneWish OS?" | OneWish OS = **CURSOR CLOUD AGENTS** repo. Open that folder or `onewish-repos.code-workspace` in Claude Code.                                                                                     |
| "I’m in a child repo"  | Read this doc (it’s synced into `docs/` in your repo). Set `MASTER_PATH` to the path of CURSOR CLOUD AGENTS on your machine; then open that folder or workspace in Claude Code.                   |
| "Sync didn’t run"      | From a terminal (or Claude Code terminal), `cd "$MASTER_PATH"` and run `./scripts/sync-dev-tools-repos-from-config.sh` and `./scripts/connect-and-configure-onewishos.sh --connections-optional`. |
| Wrong or missing repos | Run `./scripts/sync-dev-tools-repos-from-config.sh` from the master; it reads `config/repos.yaml` and writes `onewish-repos.code-workspace`. Open that workspace.                                 |

---

## 6. Propagation (per OneWish OS)

Per **OneWish Protocol** §5 and **sync-all-repos-and-review.sh**:

- **Route constitution:** `./scripts/route-constitution-to-repos.sh` — sends governance to ROUTES.
- **Sync all repos:** `./scripts/sync-all-repos-and-review.sh` — copies designated docs (MASTER_INDEX, ALL_AGENTS_LLMS_MCPS_AND_CONNECTIONS, etc.) into every repo in `all_repos`.
- **Workspace:** `./scripts/sync-dev-tools-repos-from-config.sh` — builds `onewish-repos.code-workspace` from `config/repos.yaml`.

So: **one source (master repo + config/repos.yaml)** → **same docs and workspace** everywhere when you run the scripts from the master.

---

_Maintain at: docs/CLAUDE_CODE_ONEWISHOS_SYNC_AND_VISIBILITY.md. Update when sync steps or repo paths change._
