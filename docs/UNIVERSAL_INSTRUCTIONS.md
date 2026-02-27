# Universal Instructions — Read in Every Dev Tool

> **Connected Agents.AI**. This file must be read first by any AI agent, regardless of tool (Cursor, Claude, Copilot, Codex, ChatGPT, etc.).

---

## Actions

**Default: agents execute.** Agents must take actions through **terminal, SDKs, IDEs, and/or CLIs** — not the user. The agent runs commands; do not ask the user to run them. Do not describe or simulate without executing.

**Integration of OneWish OS:** All OneWish OS instructions integrate into every dev tool (Cursor, Claude Code, Codex, Copilot, v0) via entry points (AGENTS.md, CLAUDE.md, UNIVERSAL_INSTRUCTIONS, my-agent.agent.md, .cursor/rules) and propagate down to all component repositories, NextTech OS, agents, systems, and Connected Agents.AI via `config/repos.yaml` (ROUTES, all_repos), `route-constitution-to-repos.sh`, and `sync-all-repos-and-review.sh`. Syncing, updating, and pushing follow constitution §8 and protocol §5. See `docs/constitution.md` §8 and `docs/ONEWISH_PROTOCOL.md` §5.

**Cross-tool execution (Constitution §8.5):** From any dev tool connected to OneWish OS (Cursor, Claude Code, Codex, etc.), you may run any other connected dev tool or any OneWish OS script: open the master repo or `onewish-repos.code-workspace`, then in the terminal run e.g. `./scripts/run-audit-runbook.sh` or `./scripts/connect-and-configure-onewishos.sh`. Full inventory and connect/configure: `docs/ONEWISHOS_CROSS_TOOL_AND_FULL_INVENTORY.md`.

---

## Constitution Applies

Before any significant work:

1. **Read** `docs/constitution.md` — human-in-the-loop, claim typing, explainability, bias/safety, simulation disclaimer
2. **New capabilities** — follow `docs/NEW_CAPABILITY_CHECKLIST.md` (read constitution → create skill → update indexes)
3. **Repo status** — `docs/CONSOLIDATION_AND_REPO_STATUS.md` (canonical repos, merged/archived, routing)
4. **Master rules** — `.cursor/rules/master-project-rules.mdc`, `.github/agents/my-agent.agent.md`
5. **Master files & repo architecture** — Before high-impact action (rename, consolidation, new capability), review `docs/MASTER_FILES_AND_REVIEW_BEFORE_ACTION.md`. How this repo is architected and works: `docs/reports/ONEWISH_REPO_ARCHITECTURE_AND_HOW_IT_WORKS.md`. Best practices from top repos: `docs/BEST_PRACTICES_FROM_TOP_REPOS_TO_ADD_OR_EMULATE.md`. **OneWish Protocol** (architecture, sync, rigid review, improvement): `docs/ONEWISH_PROTOCOL.md` — rigid review for usability, operability, efficiency; improvement = constant improvement loop.
6. **Cloud & inference** — Google Cloud, Gemini API, Vertex AI via `config/connectors.yaml` and `config/platform-connections.yaml`
7. **Platform audit** — `docs/PLATFORM_INTEGRATION_AUDIT.md` — 1Password audit, subscriptions, Copilot/AWS/Zoom/Linear/Docker/Box/Goose integration
8. **Reference patterns** — For file/evidence: `docs/modules/lexvault.md`; for entity schemas: `docs/modules/ontology.md`. See `docs/REFERENCE_PATTERNS_AND_EXAMPLE_REPOS.md`.
9. **Sources per action** — Before significant work, check `docs/SOURCES_AND_EMULATION_INDEX.md` for top sources to emulate. Apply virtuous loop: failure→postmortem, success→patterns-that-work, session→lessons.
10. **Master index** — Single entry point: `docs/MASTER_INDEX.md`. Find any canonical doc from there.
11. **Pre-execution checklist** — Run through `docs/SUPER_DEVELOPER_PRE_EXECUTION_CHECKLIST.md` before executing (governance, safety, efficiency, sources, repo, architecture, tools, agents, prompts, improvement, skills, compliance, verification).
12. **Expert prompting** — Apply `docs/EXPERT_PROMPT_ENGINEERING.md` for complex prompts (Claude, OpenAI, GOLDEN). Use `.cursor/skills/zero-mistake-workflow/SKILL.md` for no-mistake execution.
13. **Lifecycle stages** — At each stage (planning, pre-exec, during, post-exec, review, failure, cadence), follow `docs/LIFECYCLE_STAGES_AND_CHECKPOINTS.md` for architecture, workflows, automations, debugging.
14. **Quarterly sources review** — Run `./scripts/sources-compare-and-update.sh` to compare against top LLM/agent best practices and suggest updates.
15. **Accounts login** — Before dev sessions, run `./scripts/login-accounts.sh` (1Password sign-in → index → MCP install → launch). See `docs/ACCOUNTS_LOGIN_PROCESS.md`.
16. **Dev tools audit (no fail)** — When auditing dev tools, onboarding a new machine, or adding a new tool: run the no-fail audit in `docs/DEV_TOOLS_CANONICAL_LIST_AND_AUDIT.md` §3. Verify **every** tool in the canonical list (§1); zero chance of missing one.
17. **Knowledge, memory, artifacts, rules — iron curtain; no limitations** — **All updates are automated all the time, multi-laterally**, after studying the triggers and mechanisms used by **all LLMs and/or agents combined** (knowledge, memory, instructed memory, automated and manual artifacts, rules of any kind). **Iron curtain:** Do not disrupt this cadence across platforms, systems, or top-level files. **No limitations:** We are at the beginning of building our knowledge base, tools, and agents; there are **no limitations** on updates, new creations, artifacts, or any features of any trusted or named bidirectional system. See `docs/AGENT_SKILLS_KNOWLEDGE_TOOLS_CADENCE.md`.
18. **Quick Review and Full Review** — For plans and change lists: run **Quick Review** (ensure every change has scope, derivative effects, implementation notes, and **emulation sources** — leading GitHub instances to emulate; see `docs/QUICK_AND_FULL_REVIEW.md`). **Full Review** runs on: before commit, when changing or merging repos, quarterly, after integration/onboarding, when plan or docs have drifted, or on demand (the faster the better). Run `./scripts/run-full-review.sh`; then **complete the mandatory checklist** in `docs/audits/full-review-summary.md`. **After Full Review — zero-skip:** (a) document **derivative effects** for every change; (b) add **emulation sources** (at least one top GitHub repo or SOURCES_AND_EMULATION_INDEX entry) per change; (c) run **Comprehensive Update** (COMPREHENSIVE_DEVELOPER_PRINCIPLES + COMPREHENSIVE_UPDATE_REVIEW); (d) **refine entry-point instructions** so AGENTS.md, CLAUDE.md, UNIVERSAL_INSTRUCTIONS, NEXTTECH_OS_INSTRUCTIONS, my-agent.agent.md, .cursor/rules reference and require reading top-level docs (MASTER_INDEX, constitution, QUICK_AND_FULL_REVIEW, COMPREHENSIVE_DEVELOPER_PRINCIPLES, SOURCES_AND_EMULATION_INDEX). See NEXTTECH_OS_INSTRUCTIONS §1.4. Both Quick and Full Review are automated: `./scripts/run-quick-review.sh [path]`, `./scripts/run-full-review.sh`. When doing Full Review or quarterly audit, run the **comprehensive eval** (`./scripts/run-comprehensive-eval-and-cleanup.sh`) and use the recommendations artifact (`docs/audits/comprehensive-eval-and-cleanup-recommendations.md`) for cleanup and unification.
19. **Unlimited review and chunking** — When reviewing **unlimited information, logs, or commits** (or any corpus that may exceed context window): use **chunking** (by commit, file, or section), **review and output methods** (staged review, summarize-then-decide, stream to file, report-out), and **persist early** (write per-chunk results to disk; merge summaries for final decision). Never assume the full corpus fits in context. See `docs/AGENTIC_REVIEW_AND_CHUNKING_ARCHITECTURE.md`. This enables the agentic system to remain one of the most efficient and accurate while reviewing unbounded input; all foundational setup and comprehensive review cycle rules apply.

---

## Entry Points by Tool

| Tool    | File to Read                        | Contains                    |
| ------- | ----------------------------------- | --------------------------- |
| Any     | `AGENTS.md`                         | READ FIRST block + manifest |
| Any     | `CLAUDE.md`                         | READ FIRST block + guide    |
| Any     | `docs/UNIVERSAL_INSTRUCTIONS.md`    | This file                   |
| Cursor  | `.cursor/rules/*.mdc`               | Platform rules              |
| Copilot | `.github/agents/my-agent.agent.md`  | Agent spec                  |
| v0      | `docs/V0_SETUP_AND_INSTRUCTIONS.md` | litigationforc1 v02 rules   |

All point to the same constitution and checklist.
