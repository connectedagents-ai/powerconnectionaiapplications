# LLM, AI/ML, Multi-Agent, Cloud Agents, Private LLMs, Dev Tools & Robotics — Best Practices

**Purpose:** Single **full information** reference for design, setup, naming, and structuring of all LLM, AI/ML, multi-agent, cloud agents, private LLMs, dev tools, and robotics systems. Sourced from top white papers, top LLM/orchestration frameworks, MCP spec, OWASP/ISACA security guidance, and robotics standards. **From now on, all OneWish OS and downstream OS/features/"systems" are defined and designed according to these best practices** (see [ONEWISH_LOGIC.md](ONEWISH_LOGIC.md) §1.1 and [ONEWISH_PROTOCOL.md](ONEWISH_PROTOCOL.md)).

**Governance:** Constitution; ONEWISH_PROTOCOL; MASTER_FILES_AND_REVIEW_BEFORE_ACTION. When adding or changing any system, agent, MCP server, workflow, or repo structure, align with this doc and [BEST_PRACTICES_FROM_TOP_REPOS_TO_ADD_OR_EMULATE.md](BEST_PRACTICES_FROM_TOP_REPOS_TO_ADD_OR_EMULATE.md).

**Definition of "systems":** In this doc and in OneWish OS, **systems** means: any **OS** (OneWish OS, NextTech OS), **sub-OS** or **downstream OS** (LitigationForce.AI, Financial Audit & Tax, RobertBaileyFamilyOffice), **feature** (Connected OneWishMCP, LexVault, graph RAG, evaluator swarm), **agent** (orchestrator, specialist, workflow agent), **MCP server**, **workflow**, **repo** (master, ROUTES, all_repos), **robotics or physical-system component**, or any **module/tool/component** that is part of the One Wish Platform. All of these are **defined and designed** per this doc from now on.

---

# Full information section

## Average-person summary (full)

**What this doc is:** A single, readable guide that pulls together the best ideas from research and industry for building AI systems—large language models (LLMs), multi-agent setups, cloud and private AI, developer tools, and robotics. It covers **how to design** (clear roles, contracts, safety), **how to set up** (reproducible, secure, observable), **how to name** (consistent, discoverable), and **how to structure** (modular, scalable) so everything fits together and stays maintainable.

**Why it matters for OneWish:** Every "system" in OneWish OS—and every downstream product or feature we add—should follow these practices. That means: one clear job per agent or server, written contracts for inputs/outputs, human checkpoints where it matters, no secrets in code, and names and folders that make it obvious what something does. We also follow security best practices (e.g. OWASP Top 10 for LLM applications) so prompt injection, data leakage, and other risks are addressed. This doc is the **single source** we use when we add or change anything in that space.

**Sections below:** **Technical** (sources, design, naming, setup, security, robotics), then **average-person** take per area, then **integration with OneWish OS and downstream systems** and an **integration checklist**. References (white papers, MCP, OWASP, ROS, etc.) are listed so you can go deeper.

---

## Technical summary

### 1. Sources (white papers, frameworks, standards)

| Area                             | Top sources                                                                                                                                                                                                                                                                                                                                                       | Key ideas                                                                                                                                                                                                                                         |
| -------------------------------- | ----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| **Multi-agent LLM**              | Enterprise Guide to High-Performance Multi-Agent LLM Deployments (Swarms); Multi-Agent Design (arXiv 2502.02533); Talk Structurally, Act Hierarchically (arXiv 2502.11098); LLM Multi-Agent Systems: Challenges and Open Problems (arXiv 2402.03578); MegaAgent (500+ agents); LaMAS (privacy, monetization); MARCO (94.48% accuracy, guardrails, error recovery) | Token processing & specialization; prompt + topology optimization; structured communication; hierarchical refinement; task allocation and iterative debate; dynamic agents and system-level parallelism; guardrails for hallucinations/formatting |
| **Production agentic AI**        | Production-Grade Agentic AI (arXiv 2512.08769 / Emergent Mind); Orchestral AI (arXiv 2601.02577); Compound AI blueprint; LangGraph; Dapr Agents                                                                                                                                                                                                                   | Tool-first design; pure-function invocation; single-responsibility agents; externalized prompts; containerized deployment; deterministic orchestration; Responsible AI; KISS; clean separation of workflow logic and MCP                          |
| **MCP (Model Context Protocol)** | [MCP Best Practice](https://mcp-best-practice.github.io/mcp-best-practice/best-practice/); Anthropic MCP; Google Cloud MCP                                                                                                                                                                                                                                        | Contracts first; single responsibility; bounded toolsets; controlled autonomy; stateless; gateway pattern; security by design; observability; versioned schemas                                                                                   |
| **Private LLM / cloud agents**   | Vertex AI Agent Builder; Anthropic secure deployment; LangChain standalone server; Llama private cloud deployment; ISACA Securing LLMs (2024)                                                                                                                                                                                                                     | Deploy from Git/source/objects; dependency pinning; Redis/Postgres for state; isolation, least privilege, sandbox; secrets out of agent env; input validation; versioning and monitored pipelines                                                 |
| **LLM security**                 | OWASP Top 10 for LLM Applications (2024/2025); ISACA Securing LLMs; Elastic LLM risks; Llama security in production                                                                                                                                                                                                                                               | Prompt injection; insecure output handling; data poisoning; model inversion/extraction; sandboxing; Security & Governance Checklist; align with OWASP mitigation guidance                                                                         |
| **Robotics / systems naming**    | ROS REP-0144, ROS Naming, ROS Patterns/Conventions; Autoware.Auto namespaces; Viam triplet `namespace:module-name:model-name`                                                                                                                                                                                                                                     | Lowercase, alphanumeric + underscore; no consecutive underscores; descriptive; namespaces (control, localization, navigation, perception); hierarchical IDs; package.xml/manifest                                                                 |
| **Dev tools / repo structure**   | OSS Guide; GitHub best practices; 12-Factor Agents; BEST_PRACTICES_FROM_TOP_REPOS (this repo)                                                                                                                                                                                                                                                                     | CONTRIBUTING, SECURITY, CODEOWNERS; secret scanning; .env.example only; single entry point (AGENTS.md, MASTER_INDEX)                                                                                                                              |

### 2. Design principles (apply to all systems)

| Principle                      | Meaning                                                                    | OneWish alignment                                                                              |
| ------------------------------ | -------------------------------------------------------------------------- | ---------------------------------------------------------------------------------------------- |
| **Single responsibility**      | One clear domain per server/agent; one job per component                   | Segment agents, MCP servers, playbooks; Connected OneWishMCP as gateway routing to specialists |
| **Contracts first**            | Strict input/output schemas; documented side effects and errors; versioned | MCP tool schemas; playbook prompts; LexVault/ontology schemas; constitution claim typing       |
| **Bounded toolsets**           | Focused tools, not kitchen-sink; avoid mega-servers                        | Per-domain MCP servers; tool-list per capability                                               |
| **Controlled autonomy**        | Least-privilege tools; approval paths for high-impact actions              | Constitution human-in-loop; attorney checkpoints; high-risk tools behind approval              |
| **Stateless by default**       | Execution stateless; state in store (Neo4j, Pinecone, DB), not in-memory   | Session/context in KG or DB; MCP servers stateless                                             |
| **Security by design**         | Identity, authorization, audit in the design—not bolted on                 | MCP_SECRETS_REFERENCE; platform-connections; audit trail in constitution/LexVault              |
| **Additive change**            | Version schemas; prefer additive evolution; publish deprecations           | Schema versioning; deprecation notes in config/docs                                            |
| **Observability from day one** | Logging, tracing, metrics for tools/resources                              | verify-all-connections; Full Review log; audit trail                                           |

### 3. Naming and structuring

| Scope                        | Rule                                                                                | Example                                                                                 |
| ---------------------------- | ----------------------------------------------------------------------------------- | --------------------------------------------------------------------------------------- |
| **Agents**                   | Descriptive role; lowercase with underscores if needed; cluster prefix when grouped | `entity_extractor`, `damages_modeler`, `irs_tax_specialist_orchestrator`                |
| **MCP servers**              | One domain per server; name = domain or product                                     | `notion`, `github`, `firecrawl`; Connected OneWishMCP = gateway                         |
| **Workflows**                | `workflows-<domain>-<subdomain>.yaml`; docs match                                   | `workflows-financial-audit-tax-lexvault.yaml`, `workflows-litigation-searchers.yaml`    |
| **Repos**                    | Canonical map in CONSOLIDATION_AND_REPO_STATUS; paths consistent                    | `config/repos.yaml` ROUTES and all_repos; no ad-hoc paths                               |
| **Config files**             | `<domain>-<purpose>.yaml` or `config/<subdir>/`                                     | `playbooks.yaml`, `connectors.yaml`, `segment-lit-force-lexvault-connected.yaml`        |
| **Robotics-style (if used)** | Namespace + module + model; lowercase; alphanumeric + underscore                    | Viam-style: `org:module-name:model-name`; ROS-style: `control`, `perception` namespaces |

### 4. Setup and deployment

| Area             | Practice                                                                   | Reference                                                 |
| ---------------- | -------------------------------------------------------------------------- | --------------------------------------------------------- |
| **Dependencies** | Pin versions; lock files; minimize transitive risk                         | requirements.txt, package-lock, go.sum; BEST_PRACTICES §2 |
| **Secrets**      | Never in repo; .env.example only; managed store (e.g. 1Password)           | MCP_SECRETS_REFERENCE; PLATFORMS_1PASSWORD_MAPPING        |
| **Containers**   | Minimal base; non-root; health/readiness; signed/SBOM when possible        | MCP Best Practice: Packaging and Supply Chain             |
| **Environments** | Separate dev/stage/prod credentials, routes, policies                      | CONSOLIDATION_AND_REPO_STATUS; config per env             |
| **Gateway**      | Single policy-enforced ingress for MCP when scaling (Connected OneWishMCP) | MCP Best Practice: Gateway pattern                        |

### 5. Dev tools and repo structure

| Item                     | Practice                                                            | OneWish                                                            |
| ------------------------ | ------------------------------------------------------------------- | ------------------------------------------------------------------ |
| **Entry points**         | Single entry (README, AGENTS.md, MASTER_INDEX)                      | AGENTS.md READ FIRST; MASTER_INDEX canonical docs                  |
| **Governance**           | Constitution, checklist, universal instructions routed to all repos | route-constitution-to-repos.sh; sync-all-repos-and-review.sh §6a   |
| **Review before action** | No high-impact change without reviewing master files                | MASTER_FILES_AND_REVIEW_BEFORE_ACTION                              |
| **Skills and playbooks** | Externalized prompts; one playbook per agent/capability             | config/playbooks.yaml; docs/playbooks/; 00-ONEWISH_PLAYBOOKS_INDEX |

### 6. Robotics and physical systems (when applicable)

| Area             | Practice                                                                      | Source                                |
| ---------------- | ----------------------------------------------------------------------------- | ------------------------------------- |
| **Naming**       | Lowercase; alphanumeric + underscore; no consecutive underscores; descriptive | ROS REP-0144, Naming                  |
| **Namespaces**   | Functional categories (e.g. control, localization, navigation, perception)    | Autoware.Auto                         |
| **Resource IDs** | Hierarchical: namespace : module-name : model-name                            | Viam                                  |
| **Safety**       | Fail-safe; versioned firmware/config; audit trail for actuators               | Extend from guardrails + constitution |

### 7. Security (LLM and private deployment)

| Area                            | Practice                                                                                                                                       | Source                                                     |
| ------------------------------- | ---------------------------------------------------------------------------------------------------------------------------------------------- | ---------------------------------------------------------- |
| **OWASP Top 10 LLM**            | Address prompt injection, insecure output handling, data leakage, sandboxing, unauthorized code execution; use Security & Governance Checklist | OWASP Top 10 for LLM Applications 2024/2025                |
| **Prompt injection**            | Input validation; do not trust LLM output as code or commands without validation; human checkpoints for high-impact outputs                    | OWASP, ISACA Securing LLMs                                 |
| **Private deployment**          | Isolate credentials; version and monitor pipelines; least privilege; no secrets in agent env; .env.example only                                | ISACA, Llama security in production, MCP_SECRETS_REFERENCE |
| **Data poisoning / extraction** | Control training data provenance; limit extraction via rate limits and output filtering; audit trail                                           | ISACA, Elastic LLM risks                                   |

---

## Average-person summary by area

- **LLMs and multi-agent:** Use one clear job per agent, written “contracts” for what goes in and out, and guardrails so the system can recover from mistakes. Optimize both the prompts and how agents talk to each other (topology).
- **Cloud and private LLMs:** Deploy from Git or defined config when you can; pin library versions; keep secrets out of code; use a gateway so one place handles security and policy.
- **MCP (how AI talks to tools):** Each server does one thing well; tools have strict inputs/outputs; high-risk actions need approval; no hidden state in the server; design for security and observability from the start.
- **Naming and structure:** Names should tell you what something does. Use consistent patterns (e.g. `workflows-<domain>.yaml`, one domain per MCP server). Repos and configs follow the canonical map.
- **Dev tools:** One place to start (AGENTS.md, MASTER_INDEX). Governance (constitution, rules) is pushed to all repos. No big change without checking the master files list.
- **Robotics-style systems:** If we add hardware or robotics, use lowercase descriptive names, namespaces by function, and hierarchical IDs; plan for safety and audit trails.
- **Security:** Follow OWASP Top 10 for LLM applications (prompt injection, output validation, no secrets in code). For private LLMs, use isolated credentials and monitored pipelines. Human checkpoints for high-impact outputs.

---

## Integration with OneWish OS and downstream systems

**From now on,** all **systems** (and every downstream OS and feature) in OneWish are **defined and designed** according to this doc:

- **OneWish OS** (top-level): All logic, functionality, components, systems, architecture, best practices, and edge cases align with this doc and [BEST_PRACTICES_FROM_TOP_REPOS_TO_ADD_OR_EMULATE.md](BEST_PRACTICES_FROM_TOP_REPOS_TO_ADD_OR_EMULATE.md).
- **Downstream OS / sub-OS** (e.g. LitigationForce.AI, Financial Audit & Tax, RobertBaileyFamilyOffice): Same design, naming, and structuring principles; full inventory (repos, workflows, tools, agents) per [ONEWISH_LOGIC.md](ONEWISH_LOGIC.md) §1.1 and [SECOND_LEVEL_REPOS_AND_INTERCONNECTIONS.md](SECOND_LEVEL_REPOS_AND_INTERCONNECTIONS.md).
- **Features:** Any new feature (agent, MCP server, workflow, repo, or robotics-related component) must follow the design principles (§2), naming and structuring (§3), and setup/deployment (§4) above.

**Checkpoints:** When adding or changing a system, run [NEW_CAPABILITY_CHECKLIST.md](NEW_CAPABILITY_CHECKLIST.md); ensure SOURCES_AND_EMULATION_INDEX and this doc are updated if new sources are adopted. Full Review and architecture review (QUICK_AND_FULL_REVIEW §3.2) use this doc and BEST_PRACTICES_FROM_TOP_REPOS for alignment.

### Integration checklist (systems, from now on)

When defining or changing any **system** (OS, sub-OS, feature, agent, MCP, workflow, repo, robotics component):

| #   | Check                                                                                                                    | Doc / action                    |
| --- | ------------------------------------------------------------------------------------------------------------------------ | ------------------------------- |
| 1   | **Design** — Single responsibility, contracts first, bounded toolsets, controlled autonomy, stateless by default         | This doc §2                     |
| 2   | **Naming & structure** — Descriptive names; workflows-&lt;domain&gt;.yaml; one domain per MCP server; canonical repo map | This doc §3                     |
| 3   | **Setup & deployment** — Pinned deps, secrets out of repo, gateway pattern where applicable                              | This doc §4                     |
| 4   | **Security** — OWASP LLM Top 10; prompt injection mitigation; no secrets in code; human checkpoints for high-impact      | This doc §7                     |
| 5   | **Dev tools** — Entry points (AGENTS.md, MASTER_INDEX); governance routed/synced; review before action                   | This doc §5                     |
| 6   | **Robotics (if applicable)** — Lowercase, namespaces, hierarchical IDs, safety and audit trail                           | This doc §6                     |
| 7   | **OneWish alignment** — ONEWISH_LOGIC §1.1, ONEWISH_PROTOCOL; never-miss propagation; BEST_PRACTICES_FROM_TOP_REPOS      | ONEWISH_LOGIC, ONEWISH_PROTOCOL |
| 8   | **NEW_CAPABILITY_CHECKLIST** — Run when adding new capability; update SOURCES_AND_EMULATION_INDEX if new sources adopted | NEW_CAPABILITY_CHECKLIST.md     |

---

## References (links)

| Reference                                                                | URL                                                                              |
| ------------------------------------------------------------------------ | -------------------------------------------------------------------------------- |
| MCP Best Practice                                                        | https://mcp-best-practice.github.io/mcp-best-practice/best-practice/             |
| Model Context Protocol (Anthropic)                                       | https://modelcontextprotocol.io                                                  |
| Production-Grade Agentic AI (arXiv 2512.08769)                           | https://arxiv.org/abs/2512.08769                                                 |
| Multi-Agent Design (arXiv 2502.02533)                                    | https://arxiv.org/html/2502.02533v1                                              |
| Talk Structurally, Act Hierarchically (arXiv 2502.11098)                 | https://arxiv.org/abs/2502.11098                                                 |
| LLM Multi-Agent Systems: Challenges and Open Problems (arXiv 2402.03578) | https://arxiv.org/pdf/2402.03578                                                 |
| Orchestral AI (arXiv 2601.02577)                                         | https://arxiv.org/abs/2601.02577                                                 |
| OWASP Top 10 for LLM Applications                                        | https://owasp.org/www-project-top-10-for-large-language-model-applications/      |
| OWASP Top 10 LLM 2025 / GenAI                                            | https://genai.owasp.org/resource/owasp-top-10-for-llm-applications-2025/         |
| ISACA Securing LLMs (2024)                                               | https://www.isaca.org/resources/isaca-journal/issues/2024/volume-6/securing-llms |
| ROS Package Naming (REP-0144)                                            | https://reps.openrobotics.org/rep-0144/                                          |
| ROS Naming                                                               | https://wiki.ros.org/Naming                                                      |
| ROS Patterns/Conventions                                                 | https://wiki.ros.org/ROS/Patterns/Conventions                                    |
| Autoware naming                                                          | https://autowarefoundation.gitlab.io/autoware.auto/                              |
| Viam naming                                                              | https://docs.viam.com/operate/get-started/other-hardware/naming-modules          |
| 12-Factor Agents                                                         | https://github.com/humanlayer/12-factor-agents                                   |
| OSS Guide                                                                | https://opensource.guide/                                                        |
| Swarms Enterprise Multi-Agent LLM                                        | https://docs.swarms.world/en/latest/swarms_cloud/production_deployment/          |
| Llama security in production                                             | https://www.llama.com/docs/deployment/security-in-production/                    |
| Llama private cloud deployment                                           | https://www.llama.com/docs/deployment/private-cloud-deployment/                  |

See also: [SOURCES_AND_EMULATION_INDEX.md](SOURCES_AND_EMULATION_INDEX.md), [BEST_PRACTICES_FROM_TOP_REPOS_TO_ADD_OR_EMULATE.md](BEST_PRACTICES_FROM_TOP_REPOS_TO_ADD_OR_EMULATE.md), [STARRED_AND_REFERENCE_REPOS.md](STARRED_AND_REFERENCE_REPOS.md).
