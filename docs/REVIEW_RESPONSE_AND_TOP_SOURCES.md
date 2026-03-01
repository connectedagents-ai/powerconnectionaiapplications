# Review Response Command — Top Repos, Whitepapers, and Required Summaries

**Purpose:** (1) Define the **command** that every **Review** (genie loop, go run, or comprehensive review) must satisfy: always respond with **reference to top repos**, **whitepapers**, **real-world** context, **average-person summary**, **technical summary**, and **visual summary**. (2) Summarize **what third-party tools and environments top dev teams use** that we use or align with. (3) Summarize **what our repos say we are emulating** (sources, frameworks, example repos).

**Governance:** Constitution §6.5 (outcome, derivative outcomes, chart/graph); [QUICK_AND_FULL_REVIEW.md](QUICK_AND_FULL_REVIEW.md) §5; [GAME_CHANGERS.md](GAME_CHANGERS.md) (charts and graphs on every genie run); [SOURCES_AND_EMULATION_INDEX.md](SOURCES_AND_EMULATION_INDEX.md); [EVAL_LOOP_AND_CHAIN_OF_EVENTS.md](EVAL_LOOP_AND_CHAIN_OF_EVENTS.md) §6.5.

---

## 0. Defined term: “Review” (expanded) — full specs in Game Changer doc

**“Review” or “review”** (upper or lower case) means the **full set of review types together plus the additional turn**:

- **Types:** Go flow, Full Review (Phases 1–3), Genie loop, Comprehensive (Full Review + 1Password + connections + MERGE/ARCHIVE/DELETE/FIX + post-run eval + **commands-and-architecture review**), Post-run eval, Omni audit, Quick Review.
- **Additional turn (every review):** **Commands-and-architecture review** — all new commands organized in place (COMMANDS_AND_SCRIPTS_INDEX); architecture updated/reviewed (in whole or in part) per CS rules, repos, best practices ([PRODUCT_THAT_BUILDS_THE_PRODUCT_AND_ARCHITECTURE_TENET.md](PRODUCT_THAT_BUILDS_THE_PRODUCT_AND_ARCHITECTURE_TENET.md)).
- **Single entry:** `./scripts/run-review.sh` (runs run-every-turn.sh). **Full specs, rules, processes, features:** [GAME_CHANGER_REVIEW_AND_AUDIT_EXPANDED.md](GAME_CHANGER_REVIEW_AND_AUDIT_EXPANDED.md).

---

## 1. Review response command (mandatory for every Review)

**Command:** For every **genie loop**, **go run**, or **comprehensive review** (“Review”), the output **must** include all of the following. This applies to `run-full-review.sh` (full-review-summary.md), `run-comprehensive-eval-and-cleanup.sh`, and any “every turn” / genie run.

| Element | Required | Where it appears |
|--------|----------|-------------------|
| **Reference to top repos** | Yes | At least one of: SOURCES_AND_EMULATION_INDEX, BEST_PRACTICES_FROM_TOP_REPOS, REFERENCE_PATTERNS_AND_EXAMPLE_REPOS; or explicit “Top repos & whitepapers (this run)” section in full-review-summary.md. |
| **Reference to whitepapers / standards** | Yes | ABA/EDRM/Sedona, Production-Grade Agentic AI (arXiv), 12-Factor Agents, MCP Best Practice, OWASP LLM, ISO/IEC 42001, or doc-refs in SOURCES_AND_EMULATION_INDEX. |
| **Real-world context** | Yes | One sentence or bullet: what this run means in practice (e.g. “Connections optional; 43/104 passed; apply FIX items for production MCPs.”). |
| **Average-person summary** | Yes | Plain-language summary in full-review-summary.md “Average-person summary” and in comprehensive-eval artifacts. |
| **Technical summary** | Yes | full-review-summary.md “Technical summary”; verification result; MERGE/ARCHIVE/DELETE/FIX counts; eval-after-run metrics. |
| **Visual summary** | Yes | Charts, graphs, or structured tables: full-review-summary.md “Architecture graphs, charts & artifacts”; waterfall table; verification result; recommendations tables; links to docs/audits/artifacts/README.md. |

**Where enforced:** Full Review writes full-review-summary.md with Technical summary, Average-person summary, Architecture graphs/charts (visual), and Agent/workflows/push/sync (which include “Top frameworks” and “Next steps” pointing to SOURCES_AND_EMULATION_INDEX and top repos). This doc adds an explicit **“Top repos & whitepapers (this run)”** section to the summary template so the command is satisfied every run. See §3 below for the exact template addition.

---

## 2. Third-party tools and environments top dev teams use (that we use or align with)

From SOURCES_AND_EMULATION_INDEX, REFERENCE_PATTERNS_AND_EXAMPLE_REPOS, and our config/docs:

| Category | Third-party tools / systems | Our alignment |
|----------|----------------------------|----------------|
| **IDEs & dev tools** | Cursor, VS Code, Claude Code, Codex, Windsurf, Warp | Canonical dev tools; connect-and-configure; AGENTS.md, CLAUDE.md. |
| **MCP & APIs** | Anthropic MCP, OpenAI, Model Context Protocol | config/canonical-mcp-connectors.yaml; verify-all-connections; master MCP. |
| **Agent frameworks** | LangChain, LangGraph, Google ADK (adk-python), orchestrator patterns | ONEWISHOS_CONNECTIONS_PREBUILT_AGENTS_AND_TOOLS; orchestrator + specialists. |
| **Quality & review** | Production-Grade Agentic AI (arXiv 2512.08769), Google Cloud agent evaluation (three pillars), MCP security audit, 12-Factor verification, TRiSM | QUICK_AND_FULL_REVIEW §5; REVIEW_AND_AUDIT_STAGES_IMPROVED; Full Review checklist. |
| **Standards & compliance** | ABA Model Rule 1.1, EDRM, Sedona 2023 AI Commentary, ISO/IEC 42001:2023, OWASP LLM Top 10 | constitution; standards-compliance; LLM_AI_MULTIAGENT_AND_SYSTEMS_BEST_PRACTICES. |
| **Repo & structure** | CONTRIBUTING, SECURITY.md, CODEOWNERS, 12-Factor Agents (humanlayer) | BEST_PRACTICES_FROM_TOP_REPOS_TO_ADD_OR_EMULATE; SOURCES_AND_EMULATION_INDEX §6a. |
| **Prompting & LLM** | Anthropic Claude Code, OpenAI Prompt Engineering, GOLDEN (promptbuilder.cc), Gemini | EXPERT_PROMPT_ENGINEERING; SOURCES_REVIEWED. |
| **Storage & evidence** | Box, LexVault-style ontology | docs/modules/lexvault.md; evidence-processor, provenance. |
| **UI / front-end** | Vercel, v0, Lovable, Next.js | MODULE_ARCHITECTURE_AND_PLATFORM_STACK; V0_SETUP_AND_INSTRUCTIONS; nextjs-ai-chatbot. |
| **Secrets & auth** | 1Password, op CLI | 1PASSWORD_VAULT_ORGANIZATION; agent-1password-index-env.sh; platform-connections. |

---

## 3. What our repos say we are emulating

| Source doc | What we emulate |
|------------|------------------|
| **SOURCES_AND_EMULATION_INDEX.md** | Top sources per action: governance (ABA, EDRM, Sedona); new capabilities (constitution, my-agent.agent.md, LexVault, ontology); efficiency (AGENTS_EFFICIENCY, SUPER_DEVELOPER_PRINCIPLES); 12-Factor Agents, Production patterns; Review/audit (Production-Grade Agentic AI, Google Cloud three pillars, MCP security audit, 12-Factor, TRiSM); architecture (schema-first, router-first MCP); tool calls & MCP; agent & orchestration; prompt/LLM (Anthropic, OpenAI, GOLDEN). |
| **REFERENCE_PATTERNS_AND_EXAMPLE_REPOS.md** | Modules: LexVault, Ontology, Voice Agents, Litigation Swarm UI, OneWish website/UI. Example repos: slack-agent-template, connected-agents-platform, LitigationForce.AI, file-management-toolkit, powerconnectionaiapplications, nextjs-ai-chatbot, adk-python. |
| **BEST_PRACTICES_FROM_TOP_REPOS_TO_ADD_OR_EMULATE.md** | CONTRIBUTING, SECURITY.md, CODEOWNERS; MCP contracts first; gateway pattern; GitHub/MCP/OSS Guide/12-Factor; adopt in parts; tick when done. |
| **QUICK_AND_FULL_REVIEW.md §5** | Steps, scope, cadence, and tools aligned with **Production-Grade Agentic AI**, **Orchestral AI**, **12-Factor Agents**, **MCP Best Practice**, **SOURCES_AND_EMULATION_INDEX**. |
| **REVIEW_AND_AUDIT_STAGES_IMPROVED.md** | Production-Grade Agentic AI (arXiv 2512.08769), Google Cloud three-pillar quality gate, MCP security audit (four phases), 12-Factor verification, TRiSM; Plan→Validate→Execute; evaluation pillars (success/process/safety). |
| **LLM_AI_MULTIAGENT_AND_SYSTEMS_BEST_PRACTICES.md** | Design, setup, naming, structure for LLM, AI/ML, multi-agent, dev tools, robotics; white papers, MCP, OWASP, ISACA, ROS/Viam; technical + average-person; **all systems from now on** per this doc. |
| **full-review-summary.md (mandatory checklist)** | **Emulation sources** present for every change (at least one top GitHub repo or SOURCES_AND_EMULATION_INDEX entry); **Comprehensive Update** from top repos; **Architecture review** and **efficiency review** informed by emulated repos and SOURCES_AND_EMULATION_INDEX. |

---

## 4. Template addition: “Top repos & whitepapers (this run)” in Full Review summary

So that every Review satisfies the command, the Full Review summary (run-full-review.sh) includes a section that explicitly calls out top repos and whitepapers for the run. The script writes:

- **Top repos & whitepapers (this run):** SOURCES_AND_EMULATION_INDEX (by action); QUICK_AND_FULL_REVIEW §5 (Production-Grade Agentic AI, Orchestral AI, 12-Factor Agents, MCP Best Practice); BEST_PRACTICES_FROM_TOP_REPOS; REFERENCE_PATTERNS_AND_EXAMPLE_REPOS. Standards: ABA/EDRM/Sedona, constitution, EDRM/Sedona transparency and explainability.
- **Visual summary:** Architecture graphs, charts & artifacts (table with links to docs/audits/artifacts/README.md and FRAMEWORK_AUDITS_REVIEWS_INTEGRATIONS_BY_STAGE); Verification result; Waterfall table; Mandatory checklist table.

The existing “Technical summary,” “Average-person summary,” and “Architecture graphs, charts & artifacts” already provide technical, average-person, and visual summary; the new “Top repos & whitepapers (this run)” section satisfies the top-repos and whitepapers part of the command. Real-world context is covered by the one-line Average-person summary and the Verification result.

---

## 5. References

| Doc | Purpose |
|-----|--------|
| [SOURCES_AND_EMULATION_INDEX.md](SOURCES_AND_EMULATION_INDEX.md) | Canonical map of top sources to emulate per action |
| [REFERENCE_PATTERNS_AND_EXAMPLE_REPOS.md](REFERENCE_PATTERNS_AND_EXAMPLE_REPOS.md) | Modules and example repos we emulate |
| [QUICK_AND_FULL_REVIEW.md](QUICK_AND_FULL_REVIEW.md) | Full Review triggers; §5 top frameworks |
| [GAME_CHANGERS.md](GAME_CHANGERS.md) | Charts and graphs on every genie run (Constitution §6.5) |
| [GAME_CHANGER_REVIEW_AND_AUDIT_EXPANDED.md](GAME_CHANGER_REVIEW_AND_AUDIT_EXPANDED.md) | Full specs, rules, processes, features for Review & Audit (expanded definition; additional turn; eval loop; chain of events) |
| [EVAL_LOOP_AND_CHAIN_OF_EVENTS.md](EVAL_LOOP_AND_CHAIN_OF_EVENTS.md) | Best practices genie run; §6.5 charts and graphs |
| [audits/full-review-summary.md](audits/full-review-summary.md) | Generated Review output (technical, average-person, visual, checklist) |

_Maintain at: docs/REVIEW_RESPONSE_AND_TOP_SOURCES.md. Update when adding emulation sources or changing the Review response command._
