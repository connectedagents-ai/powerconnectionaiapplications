# NextTech OS Instructions for All Users — Master-Authored Only (One-Way)

> **Purpose**: Instructions for NextTech OS (and any instance) to perform the same workflow for all users. Derived from logged actions in the comprehensive review cycle. **This file is in a non-bidirectional portion of the repo**: master is the single source; users receive it via sync but do not submit changes back. Edits to this file are made only in the master repo (CURSOR CLOUD AGENTS).
>
> **Governance:** Constitution applies. See MASTER_INDEX.md, QUICK_AND_FULL_REVIEW.md.

---

## 0. Actions (default: agents execute)

**Agents** must execute through **terminal, SDKs, IDEs, and/or CLIs** — not the user. The agent runs commands; do not ask the user to run them. Do not describe or simulate without executing.

**Integration:** OneWish OS instructions integrate into all dev tools and propagate to all component repos, NextTech OS, agents, systems, and Connected Agents.AI per constitution §8 and protocol §5 (sync, update, push). See [constitution.md](constitution.md) §8 and [ONEWISH_PROTOCOL.md](ONEWISH_PROTOCOL.md) §5.

---

## 1. Logged Actions Turned Into Instructions

The following steps are derived from the Full Review log, sync/review scripts, and the comprehensive update cycle. **NextTech OS (or any agent acting for all users) should perform these in order when running a full review and alignment cycle.**

### 1.1 Run Full Review (master file rules)

1. From repo root: `./scripts/run-full-review.sh`
2. This runs: `./scripts/run-all-verifications.sh --routing --connections`
3. Log is written to `scripts/.full-review-last.log`; summary to `docs/audits/full-review-summary.md`
4. If connections check fails (missing env vars), treat as known gap unless 1Password/env is fully populated; other checks (platform, routing, schema, taxonomy, skills) must pass or be documented.

### 1.2 Run Quick Review (plans and change lists)

1. For the active plan or doc: `./scripts/run-quick-review.sh [path]` (default: master architecture plan or QUICK_AND_FULL_REVIEW.md)
2. Ensures every change has: Scope, Derivative effects, Implementation notes, **Emulation sources**
3. If Quick Review fails, add missing elements per `docs/QUICK_AND_FULL_REVIEW.md` §2

### 1.3 Apply comprehensive principles and chunking when scale is large

1. When reviewing unlimited logs, commits, or docs: follow `docs/AGENTIC_REVIEW_AND_CHUNKING_ARCHITECTURE.md`
2. Chunk by unit (commit, file, section); write per-chunk results to disk; merge summaries for final decision
3. Do not load full corpus into context

### 1.4 Regenerate from context (after Full Review) — no-fail

**No-fail:** Full Review is not complete until all of the following are done. The script `run-full-review.sh` writes a **Mandatory completion checklist** into `docs/audits/full-review-summary.md` every run; use that checklist every time. See also QUICK_AND_FULL_REVIEW §3.3 and §3.4.

1. Gather verified context from Full Review log and summary
2. Update plan "What aligns" / "What is missing" if state changed
3. For **every** change: document **derivative effects** (what else is impacted) and **at least one top GitHub repo (or SOURCES_AND_EMULATION_INDEX entry) to emulate**. Do not consider Full Review complete until this is done.
4. Run **Comprehensive Update** (mandatory): expand principles from top repos (COMPREHENSIVE_DEVELOPER_PRINCIPLES); review all changes against that list and by emulated repo by relevant section (COMPREHENSIVE_UPDATE_REVIEW). Add top GitHub repos to emulate per change if not already present.
5. **Refine entry-point instructions** so that AGENTS.md, CLAUDE.md, UNIVERSAL_INSTRUCTIONS, NEXTTECH_OS_INSTRUCTIONS, my-agent.agent.md, .cursor/rules **reference and require reading** top-level docs (MASTER_INDEX, constitution, QUICK_AND_FULL_REVIEW, COMPREHENSIVE_DEVELOPER_PRINCIPLES, SOURCES_AND_EMULATION_INDEX as applicable). The system is reliable only when agents are explicitly instructed to read and apply these docs. Zero-skip.
6. Run **architecture review** and **efficiency review** (informed by COMPREHENSIVE_DEVELOPER_PRINCIPLES and COMPREHENSIVE_UPDATE_REVIEW)

### 1.5 No-fail dev tools audit (when relevant)

1. Run checklist in `docs/DEV_TOOLS_CANONICAL_LIST_AND_AUDIT.md` §3
2. Verify every tool in the canonical list (§1)
3. When verifying platform connections (e.g. `./scripts/verify-all-connections.sh`), ensure **Goose** is set up if in use: API key in 1Password, `.env.mcp` ref, and launch via `./scripts/launch-ai-with-op.sh goose`. See `docs/GOOSE_SETUP_AND_INTEGRATION.md`.

### 1.6 Sync instructions to all users

1. After master doc/instruction updates: run `./scripts/sync-all-repos-and-review.sh` (or equivalent) so all users receive constitution, UNIVERSAL_INSTRUCTIONS, AGENTS.md, CLAUDE.md, master-project-rules, and other governance docs per config
2. Ensure sync script reads from `config/repos.yaml` when that is the single source (per plan §19.7)
3. **Iron curtain:** **All updates are automated all the time, multi-laterally** (per triggers and mechanisms used by all LLMs and agents combined). Sync and updates must **follow suit** and **must not disrupt** this cadence across platforms, systems, or top-level files. **No limitations** on updates, new creations, artifacts, or any features of any trusted or named bidirectional system (see `docs/AGENT_SKILLS_KNOWLEDGE_TOOLS_CADENCE.md` §1).

### 1.7 Run comprehensive evaluation and cleanup recommendations

1. Run `./scripts/run-comprehensive-eval-and-cleanup.sh` (or equivalent).
2. Read `docs/audits/comprehensive-eval-and-cleanup-recommendations.md`.
3. Apply or document MERGE/ARCHIVE/DELETE/FIX per policy; do not execute destructive actions without approval.

### 1.8 Automatic consolidation (LLM, applications, email, calendar)

1. **Automatic consolidation** of **all LLM data**, **applications data**, **email data**, and **calendar data** is performed per predefined workflows and processes for NextTech OS.
2. Scope is **expanded by function** (e.g. development, legal, CRM, project, comms, design, data) and **by class** (e.g. communications, scheduling, documents, structured, LLM/agent, config).
3. Workflows include: Full Review + audit artifacts, comprehensive eval and cleanup, omni-channel Mac review, 1Password + MCP index, sync-all-repos-and-review, route-constitution, LLM/agent run artifacts, and (when integrated) email/calendar connectors.
4. See `docs/AUTOMATIC_CONSOLIDATION_NEXTTECH_OS.md` for full scope, by function and by class, and workflow list.

---

## 2. Order of Operations (for all users)

**When Full Review runs:** Before commit (per policy), when changing or merging repos, quarterly, after integration or onboarding, when plan/docs have drifted, or on demand. Complete the mandatory checklist every time. Future: scoped (by section/repo/codebase) and cross-system Full Review as defined in QUICK_AND_FULL_REVIEW §3.1b. Evals and constant improvement loops tie into Full Review; the faster the better.

| Step | Action                                                                | Script / doc                                                                                                            |
| ---- | --------------------------------------------------------------------- | ----------------------------------------------------------------------------------------------------------------------- |
| 1    | Run Full Review                                                       | `./scripts/run-full-review.sh`                                                                                          |
| 2    | Read Full Review summary and log; complete mandatory checklist        | `docs/audits/full-review-summary.md`, `scripts/.full-review-last.log`                                                   |
| 3    | Run comprehensive eval and cleanup                                    | `./scripts/run-comprehensive-eval-and-cleanup.sh`; read `docs/audits/comprehensive-eval-and-cleanup-recommendations.md` |
| 4    | Run Quick Review on active plan                                       | `./scripts/run-quick-review.sh [path]`                                                                                  |
| 5    | If corpus is large, use chunking                                      | AGENTIC_REVIEW_AND_CHUNKING_ARCHITECTURE.md                                                                             |
| 6    | Regenerate/update plan from context; add emulation sources per change | QUICK_AND_FULL_REVIEW.md §3.2 Phase 2                                                                                   |
| 7    | Run architecture and efficiency review                                | COMPREHENSIVE_DEVELOPER_PRINCIPLES, COMPREHENSIVE_UPDATE_REVIEW                                                         |
| 8    | Run no-fail dev tools audit when auditing tools                       | DEV_TOOLS_CANONICAL_LIST_AND_AUDIT.md §3                                                                                |
| 9    | Sync to all users (from master)                                       | `./scripts/sync-all-repos-and-review.sh`                                                                                |

---

## 3. Non-Bidirectional Policy (this file)

- **Source of truth:** This file lives in the **master repo only** (CURSOR CLOUD AGENTS / NextTech OS). It is **master-authored**.
- **Direction:** One-way. Users receive it via sync (if added to route-constitution or sync list). Users do **not** submit PRs or edits to this file back to master; changes to "NextTech OS instructions for all users" are made only in master.
- **Rationale:** Ensures a single, consistent playbook for all users without divergence from user-edited copies. If a user needs a local variant, they maintain it separately; the canonical instruction set remains in master.

---

## 4. References

- Full Review: `docs/QUICK_AND_FULL_REVIEW.md` §3
- Quick Review: `docs/QUICK_AND_FULL_REVIEW.md` §2
- Comprehensive eval: `docs/audits/COMPREHENSIVE_EVAL_RECOMMENDATIONS_SPEC.md`, `scripts/run-comprehensive-eval-and-cleanup.sh`
- Chunking: `docs/AGENTIC_REVIEW_AND_CHUNKING_ARCHITECTURE.md`
- Principles: `docs/COMPREHENSIVE_DEVELOPER_PRINCIPLES.md`
- Change review: `docs/COMPREHENSIVE_UPDATE_REVIEW.md`
- Master index: `docs/MASTER_INDEX.md`

---

_Maintain at: docs/NEXTTECH_OS_INSTRUCTIONS_FOR_ALL_USERS.md. Update only from master repo. Part of NextTech OS one-way instruction set._
