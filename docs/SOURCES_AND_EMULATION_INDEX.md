# Sources & Emulation Index — Top Files, Repos, and DevDocs for Every Action

> **Purpose**: Canonical map of top sources to emulate for every action type. Enables recursive improvement and virtuous-loop rapid improvement across all actions—big or small—architecture, tool calls, agent.md, skills, and automation.
>
> **Read before**: Any significant action. **Update**: When adding new patterns, tools, or best practices.

**Referenced by**: constitution §6, UNIVERSAL_INSTRUCTIONS, NEW_CAPABILITY_CHECKLIST, SUPER_DEVELOPER_PRINCIPLES, RECURSIVE_IMPROVEMENT, CONTINUOUS_IMPROVEMENT

---

## Virtuous Loop (Apply to Every Action)

| Trigger           | Action                                                 | Sources to Emulate                                         |
| ----------------- | ------------------------------------------------------ | ---------------------------------------------------------- |
| **Failure**       | Write `postmortem-{date}.md`; add rule/anti-pattern    | RECURSIVE_IMPROVEMENT, agent-efficiency anti-pattern table |
| **Success**       | Append to `patterns-that-work.md`                      | RECURSIVE_IMPROVEMENT, CONTINUOUS_IMPROVEMENT              |
| **Session end**   | Append to `lessons.md` (do more, do less, rule to add) | RECURSIVE_IMPROVEMENT, CONTINUOUS_IMPROVEMENT              |
| **New waste**     | Add to anti-pattern list                               | AGENTS_EFFICIENCY, agent-efficiency-context.mdc            |
| **Before change** | Note baseline; compare after                           | RECURSIVE_IMPROVEMENT "Eval Before Change"                 |
| **After prompt**  | One-line capture (pattern or postmortem)               | CONTINUOUS_IMPROVEMENT "After Each Prompt"                 |

**When expanding a plan or change list** (e.g. §19.7, or any gap/to-modify list): each change must list **related leading GitHub instances (or repos) to emulate** for that change. Add new entries to this index as you find them. Quick Review and Full Review require emulation sources per change; see `docs/QUICK_AND_FULL_REVIEW.md`. Full Review also triggers **architecture review** and **efficiency review** informed by these emulated repos.

---

## 1. Governance & Constitution Actions

| Action                                      | Top Sources                                               | Repos / DevDocs                                                    |
| ------------------------------------------- | --------------------------------------------------------- | ------------------------------------------------------------------ |
| Human-in-the-loop decisions                 | `docs/constitution.md` §1                                 | ABA Model Rule 1.1, EDRM, Sedona 2023                              |
| Claim typing (FACT/INFERENCE/OPINION/LEGAL) | `docs/constitution.md` §2                                 | Evaluator Swarm, `agents/RICO_Litigation_Intelligence_Agent_v2.md` |
| Audit trail, provenance                     | `docs/constitution.md` §3, `docs/standards-compliance.md` | EDRM, ISO/IEC 42001:2023, `docs/modules/lexvault.md`               |
| Bias & safety checks                        | `docs/constitution.md` §4                                 | ABA Standard 303, Sedona AI Commentary                             |
| Simulation disclaimer                       | `docs/constitution.md` §5                                 | `.cursor/rules/master-project-rules.mdc`                           |

---

## 2. New Capability Actions (Tools, Agents, Skills)

| Action                                                        | Top Sources                                                                                           | Repos / DevDocs                                                                                                                                                                                   |
| ------------------------------------------------------------- | ----------------------------------------------------------------------------------------------------- | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| **Read first**                                                | `docs/constitution.md`, `.github/agents/my-agent.agent.md`, `.cursor/rules/master-project-rules.mdc`  | NEW_CAPABILITY_CHECKLIST                                                                                                                                                                          |
| **Create skill**                                              | `.cursor/skills/create-skill/SKILL.md`                                                                | Format: YAML frontmatter, Instructions, Examples                                                                                                                                                  |
| **Ontology/schemas**                                          | `.cursor/skills/ontology-schema-syntax/`, `lists-todos-projects/`, `names-and-connections/`           | docs/modules/ontology.md                                                                                                                                                                          |
| **Update indexes**                                            | `docs/cross-system-index.md`, `docs/CONSOLIDATION_AND_REPO_STATUS.md`, `agents/MASTER_AGENT_INDEX.md` | REFERENCE_PATTERNS_AND_EXAMPLE_REPOS                                                                                                                                                              |
| **File/evidence systems**                                     | `docs/modules/lexvault.md`                                                                            | LexVault ontology, Box integration, provenance                                                                                                                                                    |
| **Entity schemas**                                            | `docs/modules/ontology.md`                                                                            | RICO directory, naming conventions                                                                                                                                                                |
| **Example repos**                                             | `docs/REFERENCE_PATTERNS_AND_EXAMPLE_REPOS.md`                                                        | slack-agent-template, connected-agents-platform, nextjs-ai-chatbot                                                                                                                                |
| **Design / system / agent / MCP / workflow / repo structure** | `docs/LLM_AI_MULTIAGENT_AND_SYSTEMS_BEST_PRACTICES.md`                                                | Design, setup, naming, structure for LLM, AI/ML, multi-agent, cloud/private LLMs, dev tools, robotics; **all systems from now on** per this doc; white papers, MCP Best Practice, ROS/Viam naming |

---

## 3. Efficiency & Context Actions

| Action                | Top Sources                                                                           | Repos / DevDocs                    |
| --------------------- | ------------------------------------------------------------------------------------- | ---------------------------------- |
| Execute immediately   | `agent-efficiency/AGENTS_EFFICIENCY.md`, `.cursor/rules/agent-efficiency-context.mdc` | SUPER_DEVELOPER_PRINCIPLES §2      |
| Persist early         | AGENTS_EFFICIENCY "Persistence Protocol"                                              | One task; write to disk            |
| One task per message  | AGENTS_EFFICIENCY "Scope narrowly"                                                    | Split multi-part; ordered steps    |
| No verification loops | AGENTS_EFFICIENCY "Verify once"                                                       | Anti-pattern table                 |
| Self-correct planning | AGENTS_EFFICIENCY "Self-Correction During Planning"                                   | Refactor before executing          |
| API/MCP pagination    | AGENTS_EFFICIENCY, SUPER_DEVELOPER_PRINCIPLES §7                                      | Limit 10–25; minimal fields; cache |

---

## 4. Safety & Guardrail Actions

| Action                  | Top Sources                                                                    | Repos / DevDocs               |
| ----------------------- | ------------------------------------------------------------------------------ | ----------------------------- |
| Confirm destructive ops | `developer-enhancement/GUARDRAILS.md`, `.cursor/rules/guardrails-beginner.mdc` | SUPER_DEVELOPER_PRINCIPLES §1 |
| Never commit secrets    | Pre-commit scan                                                                | .env.example only             |
| Validate before write   | GUARDRAILS                                                                     | Read target; check patterns   |
| Human checkpoint        | constitution §1                                                                | High-stakes outputs           |

---

## 4b. Developer Setup & IDE / Extensions

| Action                           | Top Sources                                                                                             | Repos / DevDocs                                               |
| -------------------------------- | ------------------------------------------------------------------------------------------------------- | ------------------------------------------------------------- |
| Developer setup, IDE, extensions | `docs/DEVELOPER_FOUNDATION_AND_ONLY_THE_BEST.md`, `docs/VSCODE_EXTENSIONS_AI_ML_MCP_RECOMMENDATIONS.md` | See DEVELOPER_FOUNDATION_AND_ONLY_THE_BEST.md (external refs) |

## 4c. Enterprise IAM, Secrets, Orchestration (Okta, JumpCloud, Vault, Teleport, 1Password)

| Action | Top Sources | Repos / DevDocs |
|--------|-------------|------------------|
| **Connectors / passwords / names by entity** | `docs/ENTERPRISE_IAM_SECRETS_ORCHESTRATION_TOOLS_AND_OUR_PRINCIPLES.md`, `config/canonical-mcp-connectors.yaml`, `docs/1PASSWORD_VAULT_ORGANIZATION.md` | Okta (architectural factors, Zero Trust); JumpCloud (JIT, least privilege); HashiCorp Vault (namespaces, path taxonomy); Teleport (RBAC, labels); 1Password (vault taxonomy). Single source of truth, RBAC, audit trail, naming/ontology best practices. |
| **Entity / multi-entity naming and ontology** | `config/ontology/entity-account-master.yaml`, `docs/schemas/entity-account-master-file.schema.json`, `docs/PLATFORM_NARRATIVE_AND_ARCHITECTURE_CONTEXT.md` | Vault namespace/path structure; Okta org/tenant; entity-scoped naming; hierarchical isolation. |

---

## 5. Recursive Improvement Actions

| Action                     | Top Sources                                      | Repos / DevDocs               |
| -------------------------- | ------------------------------------------------ | ----------------------------- |
| Post-mortem on failure     | `developer-enhancement/RECURSIVE_IMPROVEMENT.md` | postmortem-{date}.md template |
| Lesson at session end      | RECURSIVE_IMPROVEMENT, `lessons.md`              | Do more, do less, rule to add |
| Pattern capture on success | RECURSIVE_IMPROVEMENT, `patterns-that-work.md`   | What, why, reuse when         |
| Anti-pattern accretion     | AGENTS_EFFICIENCY, agent-efficiency-context.mdc  | Add before continuing         |
| Eval before change         | RECURSIVE_IMPROVEMENT "Eval Before Change"       | Note baseline; compare after  |

---

## 6a. 12-Factor Agents & Production Patterns

| Action                   | Top Sources                        | Repos / DevDocs             |
| ------------------------ | ---------------------------------- | --------------------------- |
| **Own prompts**          | config/playbooks.yaml              | Externalize; version        |
| **Own context**          | AGENTS_EFFICIENCY                  | Token-efficient; paginate   |
| **Tools = structured**   | docs/schemas/, MCP descriptors     | humanlayer/12-factor-agents |
| **Human via tool calls** | Constitution §1                    | HumanCheckpoint as tool     |
| **Small focused agents** | AGENT_ORCHESTRATION_BEST_PRACTICES | Single responsibility       |
| **Stateless reducer**    | Orchestrator pattern               | Execution ≠ business state  |

---

## 6b. Expert Prompting & Zero-Mistake Actions

| Action                    | Top Sources                                                               | Repos / DevDocs                                    |
| ------------------------- | ------------------------------------------------------------------------- | -------------------------------------------------- |
| **Expert prompting**      | `docs/EXPERT_PROMPT_ENGINEERING.md`, `.cursor/rules/expert-prompting.mdc` | Claude, OpenAI, GOLDEN, Cursor                     |
| **Zero-mistake workflow** | `.cursor/skills/zero-mistake-workflow/SKILL.md`                           | SUPER_DEVELOPER_PRE_EXECUTION_CHECKLIST            |
| **Lifecycle checkpoints** | `docs/LIFECYCLE_STAGES_AND_CHECKPOINTS.md`                                | Per-stage: arch, workflows, automations, debugging |
| **Agent orchestration**   | `docs/AGENT_ORCHESTRATION_BEST_PRACTICES.md`                              | Microsoft, arXiv, Collabnix                        |
| **Quarterly sources**     | `./scripts/sources-compare-and-update.sh`                                 | Compare vs top LLM/agent docs                      |

---

## 6c. Review & Audit (Full Review, Quick Review, quality gate)

| Action                  | Top Sources                                                         | Repos / DevDocs                                                                                                                                                |
| ----------------------- | ------------------------------------------------------------------- | -------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| **Review/audit stages** | `docs/audits/REVIEW_AND_AUDIT_STAGES_IMPROVED.md`                   | Production-Grade Agentic AI (arXiv 2512.08769), Google Cloud agent evaluation (three pillars), MCP security audit (four phases), 12-Factor verification, TRiSM |
| **Full Review steps**   | QUICK_AND_FULL_REVIEW §3.2, §5; REVIEW_AND_AUDIT_STAGES_IMPROVED §2 | Plan→Validate→Execute; deterministic orchestration; quality gate (success/process/safety)                                                                      |
| **Quick Review**        | QUICK_AND_FULL_REVIEW §2; REVIEW_AND_AUDIT_STAGES_IMPROVED §2.1     | Scope, derivative effects, emulation sources, reality check, dependency order                                                                                  |

---

## 7. Architecture & System Design Actions

| Action               | Top Sources                           | Repos / DevDocs                               |
| -------------------- | ------------------------------------- | --------------------------------------------- |
| System design        | `docs/architecture.md`                | PRD, TECH_SPEC, AGENTIC_WORKFLOW_CONFIG       |
| Schema-first         | `docs/schemas/`, `examples/`          | Evidence, Claim, Timeline, Bundle             |
| Router-first MCP     | `docs/mcp-router.md`                  | Progressive discovery; fetch schema on demand |
| One evidence base    | architecture, cases/Tesla             | Multi-track mapping                           |
| Constitution routing | `docs/CONSTITUTION_ROUTING_DESIGN.md` | route-constitution-to-repos.sh                |

---

## 7b. Website / UI / Marketing Actions

| Action                            | Top Sources                                                                                                                       | Repos / DevDocs                                                                                |
| --------------------------------- | --------------------------------------------------------------------------------------------------------------------------------- | ---------------------------------------------------------------------------------------------- |
| **Website / landing / marketing** | `docs/UI_UX_AND_MARKETING_TURNKEY_GUIDE_SOURCES_AND_ORGANIZATION.md`; `docs/modules/onewish-architecture-website-ui-marketing.md` | Design system (FUNDAMENTAL_STRATEGIES §4; litigation-swarm-ui); content map; multi-site hybrid |
| **Design system & tokens**        | `docs/FUNDAMENTAL_STRATEGIES_AND_SPECIFICATIONS.md` §4; `docs/modules/litigation-swarm-ui.md`                                     | Figma Variables; shared library; one enforcer (NN/g)                                           |
| **Content SOT & copy**            | `docs/WEBSITE_AND_INVESTOR_PRESENTATION_INTEGRATED.md` (Part B); LAUNCH_BLOG §2; FOR_CUSTOMERS                                    | Doc → site map; turnkey guide §3.3                                                             |
| **Repos to search & enhance**     | `docs/STARRED_AND_REFERENCE_REPOS.md` (all platform + website/UI/marketing); CONSOLIDATION                                        | MASTER_FILES_AND_REVIEW_BEFORE_ACTION §5; module §10; turnkey Part 8                           |

---

## 8. Repo & Platform Actions

| Action                      | Top Sources                               | Repos / DevDocs                          |
| --------------------------- | ----------------------------------------- | ---------------------------------------- |
| Repo status                 | `docs/CONSOLIDATION_AND_REPO_STATUS.md`   | Canonical map, ROUTES, merge status      |
| Sync all repos              | `scripts/sync-all-repos-and-review.sh`    | ALL_REPOS, route-constitution            |
| Add new repo                | CONSOLIDATION_AND_REPO_STATUS §6          | ROUTES, bootstrap-repo-with-constitution |
| Cross-platform verification | `docs/CROSS_PLATFORM_UPDATE_CHECKLIST.md` | routing-verification.yaml, connectors    |
| Repo organization           | `docs/REPO_ORGANIZATION_ANALYSIS.md`      | Merge plan, best practices               |

---

## 9. Tool Calls & MCP Actions

| Action             | Top Sources                                                  | Repos / DevDocs            |
| ------------------ | ------------------------------------------------------------ | -------------------------- |
| MCP tool discovery | `docs/mcp-router.md`                                         | Progressive; intent-based  |
| Connector config   | `config/connectors.yaml`, `config/platform-connections.yaml` | MASTER_MCP_CONNECTORS_APIS |
| One tool per step  | SUPER_DEVELOPER_PRINCIPLES §7                                | Persist between steps      |
| Paginate, cache    | AGENTS_EFFICIENCY                                            | Limit; sparse fields       |

---

## 10. Agent & Orchestration Actions

| Action               | Top Sources                                | Repos / DevDocs                               |
| -------------------- | ------------------------------------------ | --------------------------------------------- |
| Master orchestration | `.cursor/agents/master-orchestrator.md`    | Decompose; delegate; monitor                  |
| Agent spec           | `.github/agents/my-agent.agent.md`         | Standards, vendor inventory                   |
| Playbooks            | `config/playbooks.yaml`, `docs/playbooks/` | Per-agent prompt templates                    |
| Evaluator Swarm      | constitution, RICO agent                   | Fact, Citation, Logic, Ethics gates           |
| Multi-agent roles    | my-agent.agent.md §Multi-Agent             | Orchestrator, Privilege, Contract, Compliance |

---

## 11. Prompt & LLM Best Practices (External)

| Action                     | Top Sources               | Repos / DevDocs                              |
| -------------------------- | ------------------------- | -------------------------------------------- |
| Self-verification          | Anthropic Claude Code     | Tests, screenshots, expected outputs         |
| Explore → Plan → Code      | Anthropic                 | docs/SOURCES_REVIEWED.md                     |
| Instructions first         | OpenAI Prompt Engineering | Delimiters, ###, """                         |
| Be specific                | OpenAI, Google Gemini     | Context, outcome, format                     |
| Output format via examples | OpenAI                    | Show, don't tell                             |
| GOLDEN checklist           | promptbuilder.cc          | Goal, Output, Limits, Data, Evaluation, Next |
| Course-correct early       | Anthropic                 | Redirect immediately                         |

**Full list**: `docs/SOURCES_REVIEWED.md`

---

## 12. Continuous Improvement Cadence

| Cadence          | Action                                       | Sources                      |
| ---------------- | -------------------------------------------- | ---------------------------- |
| **After prompt** | 1-line to patterns or postmortem             | CONTINUOUS_IMPROVEMENT       |
| **Weekly**       | Consolidate lessons; sync instructions       | sync-all-repos-and-review.sh |
| **Monthly**      | Research 1 topic; multi-agent review 2 rules | SOURCES_REVIEWED, top repos  |
| **Quarterly**    | Audit; refresh SOURCES_REVIEWED              | Full review                  |

---

## 13. Canonical File Map (Single Source of Truth)

| Category            | Canonical Path                                            | Propagates To                                                     |
| ------------------- | --------------------------------------------------------- | ----------------------------------------------------------------- |
| Constitution        | `docs/constitution.md`                                    | All repos via route-constitution                                  |
| Master rules        | `.cursor/rules/master-project-rules.mdc`                  | Always-apply in Cursor                                            |
| Agent spec          | `.github/agents/my-agent.agent.md`                        | Child repos via sync                                              |
| Efficiency          | `agent-efficiency/AGENTS_EFFICIENCY.md`                   | AGENTS.md, rules                                                  |
| Guardrails          | `developer-enhancement/GUARDRAILS.md`                     | guardrails-beginner.mdc                                           |
| This index          | `docs/SOURCES_AND_EMULATION_INDEX.md`                     | All repos via sync                                                |
| Reference patterns  | `docs/REFERENCE_PATTERNS_AND_EXAMPLE_REPOS.md`            | New capabilities                                                  |
| Expert prompting    | `docs/EXPERT_PROMPT_ENGINEERING.md`                       | expert-prompting.mdc, prompts                                     |
| Lifecycle stages    | `docs/LIFECYCLE_STAGES_AND_CHECKPOINTS.md`                | SUPER_DEVELOPER_PRE_EXECUTION                                     |
| Agent orchestration | `docs/AGENT_ORCHESTRATION_BEST_PRACTICES.md`              | my-agent.agent.md, orchestrator                                   |
| Zero-mistake skill  | `.cursor/skills/zero-mistake-workflow/SKILL.md`           | Pre-exec, no-mistake workflows                                    |
| Sources reviewed    | `docs/SOURCES_REVIEWED.md`                                | SUPER_DEVELOPER_PRINCIPLES                                        |
| Top-repo practices  | `docs/BEST_PRACTICES_FROM_TOP_REPOS_TO_ADD_OR_EMULATE.md` | GitHub, MCP, OSS Guide, 12-Factor; adopt in parts; tick when done |
| Top LLMs/apps — emulation, OSS, white papers, dev docs | `docs/SOURCES_AND_EMULATION_INDEX.md` §11b, `docs/AGENT_FUNCTION_SOURCES_WHITEPAPERS_CONSTITUTIONS_REPOS.md` | Constitutional, OneWish OS, Genie, master-synced, never-miss, Full Review |

---

## Quick Reference (Copy to Prompts)

```
BEFORE ACTION: Check SOURCES_AND_EMULATION_INDEX for this action type
AFTER FAILURE: postmortem + anti-pattern
AFTER SUCCESS: 1 line to patterns-that-work
SESSION END: lessons.md (do more, do less, rule to add)
NEW WASTE: Add to anti-pattern list immediately
CADENCE: Weekly sync; monthly research; quarterly audit
```

---

_Maintain at: docs/SOURCES_AND_EMULATION_INDEX.md. Update when adding action types, sources, or best practices. Re-review quarterly with SOURCES_REVIEWED._
