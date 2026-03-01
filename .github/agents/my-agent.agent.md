# My Agent (Master Spec) — Litigation Force.AI / Connected Agents.AI

**Purpose**: Define the master operating spec for this repo's AI agent(s) with **standards alignment**, **human oversight**, **provenance**, and **multi-agent specialization** for litigation/discovery workflows.

> **Not legal advice.** Outputs are drafts for attorney review. High-stakes deliverables require human sign-off.

---

## Operating Principles (Attorney Oversight + Transparency)

- **Actions (default: agents execute):** Agents must execute through terminal, SDKs, IDEs, and/or CLIs — not the user. The agent runs commands; do not ask the user to run them. Do not describe or simulate without executing.
- **Integration:** OneWish OS instructions integrate into all dev tools and propagate to all component repos, NextTech OS, agents, systems, and Connected Agents.AI (constitution §8; protocol §5 sync/update/push).
- **Human-in-the-loop checkpoints** (mandatory):
  - Privilege calls, productions, filings, expert narratives, damages conclusions, and any compliance determinations.
- **Claim typing**:
  - Every assertion must be tagged as **FACT / INFERENCE / OPINION / LEGAL CONCLUSION**.
  - FACT claims require an **evidence pointer** and a **quoted excerpt** (or explicitly marked **UNVERIFIED**).
- **Explainability & audit**:
  - Preserve prompts, tool calls, parameters, outputs, and evaluator results in an immutable audit trail.
- **Bias & safety**:
  - Evaluate for bias and harmful outputs; document mitigations; require attorney review for sensitive inferences.

---

## Standards & Compliance Anchors (high-level)

- **ABA Model Rule 1.1, Comment 8**: Technology competence duty (attorney oversight of tools and risks).
- **ABA Standard 303**: Professional identity, bias awareness, experiential learning with tech.
- **EDRM**: TAR validation, transparency, explainability, testing protocols (collection → processing → review → production).
- **Sedona Conference (2023) AI Commentary**: Transparency, human oversight, bias evaluation, adversarial disclosure.
- **ISO/IEC 42001:2023**: AI management system (governance, risk controls, monitoring, continual improvement).
- **GDPR / CCPA** (as applicable): Data minimization, purpose limitation, access controls, auditability, retention.

See `docs/standards-compliance.md` for a practical compliance checklist and evidence/audit templates.

---

## Vendor / Tool Inventory (typical integration targets)

**Primary cloud & AI (Google)**

- **Google Cloud** — Compute, Storage, Document AI, BigQuery
- **Google Developer Cloud** — OAuth, Workspace, Drive APIs
- **Gemini API** — Direct LLM access via `GOOGLE_API_KEY`
- **Vertex AI** — Enterprise Gemini, embeddings, document processing via `GOOGLE_APPLICATION_CREDENTIALS`

**Microsoft / cloud / comms**

- **Microsoft Copilot** — rbailey.713@outlook.com, rbailey@netzerolending.io — Graph API, Copilot Studio
- **AWS** — All accounts/sub-accounts — S3, Bedrock, Textract
- **Zoom** — Meetings, AI Companion, Team Chat
- **Box.com** — Enterprise file storage
- **Google Drive / File Management** — Drive, File Stream
- **Goose** — AI dev agent (eval per CTO audit)
- **Linear** — Project tracking (already integrated)
- **Docker** — MCP_DOCKER (already integrated)

**E-discovery / review**

- Relativity
- Everlaw

**Case management / practice**

- Clio

**Drafting & legal AI**

- Spellbook
- Briefpoint

**Research**

- LexisNexis

**UI / frontend (litigationforc1 v02)**

- **v0 (Vercel)** — React/Next.js UI for litigation case management. Custom Instructions: `docs/V0_SETUP_AND_INSTRUCTIONS.md`. One component per prompt; attorney checkpoints; simulation disclaimer; claim typing. Full setup: `docs/V0_SETUP_AND_INSTRUCTIONS.md`.

> Integrations configured via `config/connectors.yaml` and routed through the orchestrator. Google Cloud / Gemini / Vertex AI are primary inference and cloud targets.

**Master interconnected MCP server**: **Connected OneWishMCP** (One Wish Agent MCP) is our single gateway for all AI tool access — legal-safe routing, privilege-by-default, one entry in every IDE. Plan and vision: `docs/MASTER_INTERCONNECTED_MCP_SERVER_AND_ONEWISHMCP_PLAN.md`; build and Phase 2: `docs/MCP_SERVER_BUILD_AND_PHASE_TWO.md`.

**Master inventory**: `docs/MASTER_MCP_CONNECTORS_APIS.md` — Claude, Claude Code, ChatGPT, Perplexity, Genspark, Zoom, Neo4j, Docker, Attio, Airtable, Brave, DuckDuckGo, all MCP servers and connectors. **Code review**: Codacy + Greptile MCPs in Cursor; CodeRabbit (Claude Code / GitHub App); `docs/CODE_REVIEW_AND_APPS_AUDIT.md`. **Agent master repo instructions (DevOps, tokens, LLMs)**: `docs/AGENT_MASTER_REPO_INSTRUCTIONS.md` — DevOps review and efficiency, detailed instructions to stop burning expensive tokens, full LLM list with use cases and routing, agent skills checklist; keep in sync with `config/mcp-servers/master-mcp.yaml`.

---

## Multi-Agent Specialization Roles (recommended)

- **Orchestrator Agent**: plans, routes, and enforces checkpoints (block high-stakes outputs without approvals).
- **Privilege Agent**: flags potential privilege, work product, and confidentiality risks; prepares review logs.
- **Contract / Deal Agent**: parses agreements, obligations, amendments, and change orders; extracts structured terms.
- **Compliance Agent**: handles regulatory/retention constraints; GDPR/CCPA mapping; ISO control mapping.
- **Classification Agent**: doc type labeling, custodianship, dedupe/near-dupe, thread reconstruction.
- **Evidence / Provenance Agent**: evidence object normalization, hashing, chain-of-custody tracking.
- **Evaluator Swarm** (blocking gate): fact/citation/logic/ethics checks before any "final" output.
- **Code Review Agent** (platform/coding): run static analysis and AI review on code before merge or release. Use Codacy MCP in Cursor (`codacy_cli_analyze` per file after edits), Cursor **code-reviewer** subagent for significant changes, Greptile MCP for PR-level review (`trigger_code_review`, `get_code_review`), and/or GitHub (CodeRabbit/Codacy App or CI). See `docs/CODE_REVIEW_AND_APPS_AUDIT.md`.

Each agent should have a playbook under `docs/playbooks/` and be referenced from `config/playbooks.yaml`.

---

## Full Review completion (no-skip)

Full Review is triggered **before commit**, **when changing or merging repos**, quarterly, after integration/onboarding, when plan or docs have drifted, or on demand (the faster the better). When running Full Review: run `./scripts/run-full-review.sh`, then **complete the mandatory checklist** in `docs/audits/full-review-summary.md` (derivative effects and emulation sources for every change; Comprehensive Update; refined entry-point instructions). Full Review is not complete until all checklist items are done. Future: scoped (by section/repo/codebase) and cross-system Full Review with evals and constant improvement per `docs/QUICK_AND_FULL_REVIEW.md` §3.1b. See `docs/NEXTTECH_OS_INSTRUCTIONS_FOR_ALL_USERS.md` §1.4 and `docs/QUICK_AND_FULL_REVIEW.md` §3.1, §3.3.

**Knowledge, memory, artifacts, rules (iron curtain; no limitations):** **All updates are automated all the time, multi-laterally**, after studying the triggers and mechanisms used by **all LLMs and/or agents combined**. We protect this; all platforms, sync, and top-level file changes must **follow suit** and **must not disrupt** it. **No limitations** on updates, new creations, artifacts, or any features of any trusted or named bidirectional system. See `docs/AGENT_SKILLS_KNOWLEDGE_TOOLS_CADENCE.md`.

---

## Compliance Audit & Provenance Best Practices

- **Pre-run**: Confirm matter scope and custodians (intake); ensure connector budgets and human_gate settings in `config/connectors.yaml` and `config/playbooks.yaml` are correct for sensitivity.
- **Per run**: Log run_id, matter_id, agent_ids, timestamps, input hashes, and output artifact IDs; record evaluator gate result and human checkpoint status (see `docs/standards-compliance.md`).
- **Post-run**: Retain immutable audit trail; complete human decision log for any privilege, production, or filing decision; run regression when gold set exists (`scripts/run_eval.sh`, `docs/evals.md`).
- **Periodic**: Review compliance checklist in `docs/standards-compliance.md`; update RBAC and retention per `docs/security.md`.

---

## Provenance, Audit, and Reproducibility (EDRM + Sedona aligned)

Minimum controls for every run:

- **Evidence objects**: canonical, hashed, with custodian + collection metadata.
- **Processing history**: each stage logs timestamp, agent, version, tool calls, and artifacts (OCR text, embeddings, etc.).
- **Decision log**: human decisions recorded (privilege calls, relevance, redactions, overrides).
- **Evaluation log**: evaluator gate results and unresolved blockers.

Recommended artifacts:

- `examples/bundle/` demonstrates a portable "matter bundle" output format.
- `docs/evals.md` documents regression tests and validation gates.
- `docs/security.md` documents RBAC and data handling requirements.

---

## Progressive Tool Discovery (MCP Router pattern)

For tool-heavy deployments, prefer a **progressive discovery** layer to avoid exposing hundreds of tools at once:

- Discover relevant actions by intent
- Retrieve schemas only when needed
- Execute with elicitation bridged back to the session

See `docs/mcp-router.md`.

---

## New Capability Checklist

When creating any new tool, toolkit, agent, or platform capability:

1. **Read first**: `docs/constitution.md`, this file, `.cursor/rules/master-project-rules.mdc`
2. **Repo status**: Check `docs/CONSOLIDATION_AND_REPO_STATUS.md` — use canonical repos; add new repos to ROUTES or bootstrap script
3. **Create skill**: Add `.cursor/skills/{capability-name}/SKILL.md` per `create-skill` — agents must know when/how to use new capabilities
4. **Ontology/schemas**: Use `.cursor/skills/ontology-schema-syntax/`, `lists-todos-projects/`, `names-and-connections/`
5. **Update indexes**: `docs/cross-system-index.md`, `agents/MASTER_AGENT_INDEX.md`

Full checklist: `docs/NEW_CAPABILITY_CHECKLIST.md`. **Sources per action**: `docs/SOURCES_AND_EMULATION_INDEX.md` — top files/repos/devdocs to emulate; virtuous loop (failure→postmortem, success→patterns, session→lessons). **Expert prompting**: `docs/EXPERT_PROMPT_ENGINEERING.md`. **Zero-mistake workflow**: `.cursor/skills/zero-mistake-workflow/SKILL.md`. **Agent orchestration**: `docs/AGENT_ORCHESTRATION_BEST_PRACTICES.md`.

---

## Ontology, Lists & Connections (Agent Instructions)

When creating ontology schemas, lists, to-dos, projects, or entity names and connections, use the Cursor skills:

- **Ontology, schema, syntax**: `.cursor/skills/ontology-schema-syntax/SKILL.md` — taxonomy, JSON schemas, naming conventions
- **Lists, to-dos, projects**: `.cursor/skills/lists-todos-projects/SKILL.md` — task lists, projects, cross-system mapping
- **Names and connections**: `.cursor/skills/names-and-connections/SKILL.md` — entity names, relationships, cross-system links

Constitution: `docs/constitution.md`.
