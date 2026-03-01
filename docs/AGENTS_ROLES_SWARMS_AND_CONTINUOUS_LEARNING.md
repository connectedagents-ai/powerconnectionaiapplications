# Agents, Roles, Swarms, and Continuous Learning — Industry-Standard Titles, Expertise, Tools, and Best-in-Domain Regimen

**Purpose:** Set up **each agent and role** (attorney specialists and third-party specialists) with **industry-standard titles**; **narrow**, **core**, and **shared expertise**; **tools** (cloud stack, dev stack, tech stack, OneWish OS, and competitor tools/features); **knowledge, skills, tools, and scripts**; **swarms** with **instructions**, **filing systems**, and **structured output**; a **continuous-learning regimen**; and a **system to call on APIs for any LLM and any repo** so agents **use the right LLM for the right job**, directed by a **forum of dev tools** with **check-ins**, **evals**, and a **continuous improvement loop** that includes **human-in-the-loop steps**. When building agents, **always start with open source repos, emulations, or existing structures**; **identify best repos for each agent variety** based on **all conditions and variables** (domain fit, license, structure, activity, security, stack compatibility, documentation, community).

**Governance:** [constitution.md](constitution.md) (human-in-the-loop, claim typing); [security.md](security.md); [modules/lexvault.md](modules/lexvault.md); [playbooks/00-ONEWISH_PLAYBOOKS_INDEX.md](playbooks/00-ONEWISH_PLAYBOOKS_INDEX.md).

---

## 1. Agent and role roster — industry-standard title, narrow/core/shared expertise, tools

Each row is an **agent or role** (AI agent or human specialist). **Industry-standard title** = title used in law firms, LPOs, or legal tech (e.g. eDiscovery Analyst, Legal Research Specialist). **Narrow expertise** = domain in which the agent aims to be best-in-class. **Core expertise** = primary skills; **shared expertise** = overlap with other agents (e.g. LexVault read/write, structured output). **Tools** = cloud stack, dev stack, tech stack, OneWish OS, and competitor tools/features to use or consider.

### 1.1 Core pipeline and orchestration

| Agent / role | Industry-standard title | Narrow expertise | Core expertise | Shared expertise | Tools (cloud / dev / tech / OneWish OS / competitor) |
|--------------|-------------------------|-------------------|----------------|------------------|--------------------------------------------------------|
| **Orchestrator** | Litigation Workflow Orchestrator / Legal Operations Coordinator | End-to-end matter workflow planning and agent routing | Decomposition, dependency ordering, human checkpoint enforcement, audit logging | LexVault, config (playbooks, connectors), constitution, schemas | OneWish OS scripts, config/playbooks.yaml, config/connectors.yaml, MCPs; Cursor/Claude; competitor: Relativity workflows, Everlaw pipelines, iManage Work |
| **Intake** | Matter Intake Specialist / Legal Intake Coordinator | Matter setup, party/custodian scope, document queue | Matter config validation, matter_id assignment, queue to OCR | LexVault matter scope, matter-config schema, EDRM collection scoping | LexVault API, examples/matter-config.yaml, intake engine (Graph RAG, Pinecone); competitor: Clio intake, iManage intake, Relativity processing queue |
| **OCR / ingestion** | Document Processing Specialist / OCR Analyst | OCR, image-to-text, multi-format ingestion | Scanned doc and photo OCR, quality check, derivative storage | LexVault raw + derivatives, SHA-256, matter-scoped write | LexVault, OneWish ingestion scripts; competitor: Relativity processing, Everlaw processing, Adobe PDF Extract |
| **Entity extraction** | Entity Extraction Analyst / Knowledge Graph Analyst | NER, entity resolution, KG population | People, orgs, dates, places from unstructured text; link to KG | LexVault, ontology, structured output (fact, entity schemas) | LexVault, Pinecone/vector, Neo4j KG, docs/schemas; competitor: Luminance entity, Kira, contract analytics NER |
| **Claim mapper** | Claim & Element Analyst / Case Theory Analyst | Map claims to elements and evidence | Claim–element–evidence mapping, claim matrix, issue coding | LexVault, claim-matrix schema, ontology | LexVault, docs/ontology, claim_matrix schema; competitor: Everlaw issue coding, Relativity conceptual |
| **Evidence linker** | Evidence Linkage Analyst / Trial Support Analyst | Link exhibits to claims, facts, timeline | Evidence–claim–fact linking, exhibit numbering, provenance | LexVault, timeline, evidence-object schema | LexVault, timeline event schema, LITIGATION_EVIDENCE_AND_EXHIBITS; competitor: Trial Director, TrialLine, Relativity Trial |
| **ESI scoping** | ESI & Preservation Specialist / eDiscovery Scope Analyst | ESI scope, preservation, custodian/data source mapping | Custodian list, data sources, date range, preservation notices | LexVault matter scope, EDRM | Config, checklists; competitor: Relativity Collect, Everlaw scope, legal hold platforms |
| **Deposition planner** | Deposition Planning Specialist / Litigation Support Analyst | Deposition outlines, topic lists, exhibit lists | Outline by witness/topic, exhibit mapping, chronology tie-in | LexVault, timeline, claim matrix | LexVault, timeline schema; competitor: CaseMap, Opus 2, trial prep tools |
| **Damages modeler** | Damages & Financial Analyst / Forensic Accounting Support | Damages modeling, calculations, scenario runs | Financial model, loss calculations, expert-ready inputs | LexVault, financial schemas, human checkpoint | cost-estimator, financial-audit workflows; competitor: Veritext damages, Excel/BI, expert platforms |
| **Risk monitor** | Risk & Compliance Monitor / Legal Risk Analyst | Risk signals, compliance alerts, matter risk flags | Monitoring rules, alerting, escalation paths | LexVault, audit trail, security | config/connectors.yaml budgets, security.md; competitor: Intapp Risk, compliance dashboards |
| **Drafting** | Legal Drafting Assistant / Document Automation Specialist | Memos, motions, letters, first-draft pleadings | Template-based drafting, citation, tone; human sign-off for filings | LexVault matter context, Genie/private LLM | Genie, Ollama, drafting playbook; competitor: CoCounsel, Harvey, Lexis+ AI, Westlaw AI |
| **Document abstract & review** | Document Review Analyst / Abstractor | Summarization, classification, privilege/PII draft flags | One-line abstract, responsive/issue tags, privilege/PII draft for attorney | LexVault, provenance, RBAC | LexVault, private LLM; competitor: Relativity review, Everlaw, Luminance, DISCO AI |

### 1.2 Attorney and third-party specialist roles (industry-standard)

| Role (human or agent-assisted) | Industry-standard title | Narrow expertise | Core expertise | Shared expertise | Tools |
|--------------------------------|-------------------------|-------------------|----------------|------------------|-------|
| **Case / matter lead** | Managing Attorney / Case Manager | Matter strategy, client relationship, final sign-off | Strategy, staffing, human checkpoints, privilege/production/filing sign-off | Constitution, LexVault RBAC, audit | OneWish OS, Genie, practice mgmt, DMS |
| **Privilege reviewer** | Privilege Review Attorney / Confidentiality Reviewer | Privilege and work-product determination | Privilege log, designations, redactions; human-only for final call | LexVault privilege flags, provenance | LexVault, review platform, Genie (draft only); competitor: Relativity privilege, Everlaw |
| **Legal research** | Legal Research Specialist / Research Attorney | Case law, statutes, secondary sources, memos | Research, citation, memo drafting; can use public APIs for non-matter research | LexVault for matter-specific; research vendors | Lexis, Westlaw, Casetext, Genie for matter; competitor: CoCounsel, vLex |
| **eDiscovery / litigation support** | eDiscovery Analyst / Litigation Support Specialist | Collection, processing, review, production | EDRM phases, TAR, quality control, production specs | LexVault, processing outputs, load files | Relativity, Everlaw, DISCO; OneWish for pipeline; competitor: Consilio, Epiq |
| **Contract / temporary attorney** | Document Review Attorney / Contract Attorney | Linear/TAR review, coding, quality control | Review, issue coding, batch sign-off per firm policy | LexVault, review UI, human checkpoint | Vendor review platform; OneWish for routing and provenance |
| **Expert / damages** | Damages Expert / Forensic Accounting Expert | Damages and financial analysis; expert report | Calculations, assumptions, report; human-only conclusions | LexVault, financial model inputs; human checkpoint | Damages modeler agent output; Excel, expert platforms |
| **Court reporting / transcription** | Court Reporter / Legal Transcriptionist | Depositions, hearings, real-time, final transcript | Transcript, exhibits, real-time feed | Timeline, exhibit linkage | Court reporting vendor; OneWish for timeline ingestion |

### 1.3 Research and profile agents (narrow domain)

| Agent | Industry-standard title | Narrow expertise | Core expertise | Shared expertise | Tools |
|-------|-------------------------|-------------------|----------------|------------------|-------|
| **Witness research** | Witness Research Analyst / Impeachment Research Specialist | Witness background, impeachment, prior statements | Public records, social, prior testimony, credibility | LexVault parties, timeline; structured output | Brave/Firecrawl, LexVault; competitor: Westlaw People, public records APIs |
| **Jurisdiction research** | Jurisdiction & Venue Analyst / Forum Research Specialist | Venue, transfer, choice of law, jurisdiction | Courts, rules, transfer factors, choice of law | LexVault venue, matter config | Research APIs, config; competitor: Lexis, Westlaw, Court API |
| **Judge research** | Judicial Analytics Specialist / Judge Profile Analyst | Judge tendencies, rulings, biography | Orders, opinions, demographics, tendencies | LexVault, matter venue | Research APIs, structured output; competitor: Lexis CourtLink, Ravel |
| **Clerks research** | Law Clerk & Chambers Research Analyst | Clerks, chambers, procedures | Clerk bios, chambers rules, submission practices | Jurisdiction, judge linkage | Research, structured output |
| **Law firms research** | Law Firm Intelligence Analyst / Competitive Intelligence | Firm practice, cases, laterals | Firm profiles, cases, attorneys | LexVault, party/counsel | Research APIs, profiles |
| **Litigation finance research** | Litigation Finance Research Analyst | Litigation finance players, terms, case types | Finance companies, terms, case fit | Matter type, claim type | Research, structured output |
| **Case evaluation** | Case Evaluation Analyst / Case Assessment Specialist | Case valuation, liability, exposure | Evaluation framework, comparables, risk | Claim matrix, damages; human checkpoint | LexVault, cost-estimator; competitor: litigation analytics |
| **Tax / IRS specialist (orchestrator)** | Tax & IRS Research Orchestrator / Tax Defense Research Lead | Tax damages defense, IRS, NOL/OIC/QOZ | Orchestrate tax research sub-workflows, aggregate | Config, limits, provenance | config/workflows-tax, playbooks (IRS, NOL, OIC, QOZ, etc.) |
| **Oil & gas waste research (orchestrator)** | Oil & Gas Waste Research Orchestrator / Energy Research Lead | O&G waste, water, permits, capital, logistics | Orchestrate O&G research sub-workflows, aggregate | config/workflows-oil-gas-waste-research.yaml, limits | Brave, Firecrawl, playbooks, aggregated report |

### 1.4 Knowledge, skills, tools, and scripts per agent (cloud stack, dev stack, tech stack, OneWish OS, competitor features)

Each agent should have explicit **knowledge** (docs, schemas, ontology), **skills** (Cursor skills or playbook steps), **tools** (MCPs, APIs, LexVault, scripts), and **scripts** (OneWish OS scripts, runbooks). Include **competitor tools and features** that are underused or not yet considered so the agent can emulate or surpass them.

| Agent | Knowledge | Skills | Tools | Scripts | Competitor features to consider / adopt |
|-------|-----------|--------|-------|---------|----------------------------------------|
| **Orchestrator** | constitution, playbooks index, connector config, human-checkpoint list | Decompose request, route, enforce gate, log | config/playbooks.yaml, config/connectors.yaml, MCPs, eval scripts | run-review.sh, sync scripts, eval loop | Relativity workflow engine, Everlaw pipeline builder, iManage Work automation |
| **Intake** | matter-config schema, EDRM scoping, LexVault ontology | Validate matter, register, queue docs | LexVault API, intake engine config, examples/matter-config.yaml | Ingestion scripts, file naming | Clio intake automation, iManage matter creation, Relativity matter template |
| **Entity extraction** | Ontology (MASTER_ONTOLOGY, entity types), fact/entity schemas | NER, resolution, KG write | LexVault, Pinecone, Neo4j, extraction pipeline | Entity extraction script, KG update | Luminance entity extraction, Kira entities, contract analytics NER |
| **Claim mapper** | Claim taxonomy, predicate acts, element checklist | Map claim–element–evidence, produce claim matrix | LexVault, claim_matrix schema, ontology | Claim-mapper workflow | Everlaw issue coding, Relativity conceptual, CaseMap claim mapping |
| **Evidence linker** | Evidence-object schema, timeline schema, exhibit rules | Link doc to claim/fact/timeline, numbering | LexVault, timeline, evidence-object.schema.json | Evidence-linker script | Trial Director, TrialLine, Relativity Trial, Opus 2 |
| **Drafting** | Matter context, claim matrix, timeline (from LexVault); citation rules | Draft memos, motions, letters; cite-check | Genie/Ollama (private), LexVault read | Drafting playbook, template loader | CoCounsel, Harvey, Lexis+ AI, Westlaw AI, Spellbook |
| **Document abstract & review** | Classification schema, privilege/PII rules, ontology | Summarize, classify, flag privilege/PII (draft) | LexVault read/write, private LLM | Review batch script, provenance write | Relativity review, Everlaw AI, Luminance, DISCO AI, TAR 2.0 |
| **Witness research** | Witness profile schema, impeachment checklist | Search, extract, profile, prior statements | Brave/Firecrawl MCP, LexVault write, structured output | Research playbook, profile writer | Westlaw People, public records vendors, social discovery |
| **Judge research** | Judge profile schema, ruling taxonomy | Search opinions, orders, bio; tendencies | Research APIs, structured output, LexVault | Judge profile script | Lexis CourtLink, Ravel, judicial analytics |
| **Tax/IRS orchestrator** | Tax ontology, IRS links, OIC/NOL/QOZ knowledge | Route to sub-playbooks, enforce limits, aggregate | config/workflows-tax, limits, playbooks | Tax research swarm script | Tax research vendors, Bloomberg Tax, Checkpoint |
| **Oil & gas orchestrator** | O&G ontology, permits, waste streams | Route to sub-workflows, limits, aggregate | config/workflows-oil-gas-waste-research.yaml, playbooks | O&G swarm script | S&P Global, Enverus, energy research platforms |

### 1.5 Open source and emulation first; best repos per agent variety

**Principle:** When building agents, **always start with** open source repos, emulations, or existing structures. Prefer adapting and integrating proven patterns over building from scratch.

| Practice | Description |
|----------|-------------|
| **Open source first** | Before implementing a new agent (or major capability), **search for** and **evaluate** open source repos that already do the same or similar work: orchestration, intake, NER, document review, research tooling, workflow engines, etc. |
| **Emulations and structures** | Use **emulations** (copy patterns, architecture, or interfaces from leading repos) and **structures** (file layout, config shape, schema, playbook format) from reference repos so our agents align with industry patterns and are easier to maintain. |
| **Best repo per variety** | For **each agent variety** (orchestrator, intake, OCR/ingestion, entity extraction, claim mapper, evidence linker, research, drafting, etc.), **identify the best repos** to use or emulate, based on **all relevant conditions and variables** (see table below). |

**Identify best repos for each variety — conditions and variables**

When choosing which repo(s) to start from or emulate for a given agent variety, evaluate and rank candidates using these **conditions and variables**:

| Variable / condition | What to evaluate |
|---------------------|------------------|
| **Domain fit** | How well the repo matches the agent’s narrow domain (e.g. legal intake, eDiscovery, NER for contracts, workflow orchestration, research aggregation). |
| **License** | Prefer permissive (MIT, Apache-2.0, BSD) for integration and reuse; note copyleft (GPL) implications if we ship combined works. |
| **Structure and patterns** | Playbook-like config, MCP-compatible tools, LangGraph/LangChain patterns, schema-first outputs — match to our stack (OneWish OS, LexVault, constitution). |
| **Activity and maintenance** | Recent commits, issues addressed, releases; prefer maintained projects. |
| **Security and compliance** | Auth, RBAC, audit trail, no hardcoded secrets; alignment with [security.md](security.md) and [constitution.md](constitution.md). |
| **Stack compatibility** | Works with our LLM routing, vector/KG (Pinecone, Neo4j), config (playbooks, connectors), and human-checkpoint flow. |
| **Documentation and examples** | Clear README, CONTRIBUTING, examples or demos that map to our use case. |
| **Community and references** | Used or cited by other legal-tech or agent frameworks; mentioned in [SOURCES_AND_EMULATION_INDEX.md](SOURCES_AND_EMULATION_INDEX.md), [BEST_PRACTICES_FROM_TOP_REPOS_TO_ADD_OR_EMULATE.md](BEST_PRACTICES_FROM_TOP_REPOS_TO_ADD_OR_EMULATE.md), or [STARRED_AND_REFERENCE_REPOS.md](STARRED_AND_REFERENCE_REPOS.md). |

**References:** Maintain and extend the mapping of **agent variety → best repos** in [SOURCES_AND_EMULATION_INDEX.md](SOURCES_AND_EMULATION_INDEX.md) (by action/agent type) and in [REFERENCE_PATTERNS_AND_EXAMPLE_REPOS.md](REFERENCE_PATTERNS_AND_EXAMPLE_REPOS.md). When adding a new agent or capability, list the chosen open source or emulation source and the variables that drove the choice; update Full Review and improvement loop to keep the mapping current.

---

## 2. Swarms: instructions, filing systems, structured output

A **swarm** = a set of agents working together under an **orchestrator** with shared **instructions**, a **filing system** (where outputs go), and **structured output** (schemas). Goal: **gather all knowledge necessary** so each agent in the swarm can become **best in its narrow domain**, with **regular updates** and **coordinate sorts and pushes at every stage**.

### 2.1 Swarm definitions (instructions, filing system, structured output)

| Swarm | Purpose | Instructions (summary) | Filing system (where outputs go) | Structured output (schemas) |
|-------|---------|------------------------|-----------------------------------|-----------------------------|
| **Core litigation pipeline** | Intake → OCR → entity → claim → evidence → deposition → damages → human checkpoints | Orchestrator playbook; route in order; enforce evaluator gate and human checkpoint for privilege, production, filing, damages | LexVault (raw, derivatives, provenance); matter-scoped folders; artifact IDs in chain-of-events | matter-config, fact.schema, timeline-event.schema, claim-matrix-entry.schema, evidence-object.schema, reviewer-annotation.schema |
| **Tax / IRS damages defense research** | Full tax research (experts, examples, arguments, case law, IRS updates, NOL/OIC/QOZ, etc.) | Orchestrate sub-workflows per config; enforce limits; aggregate reports | config output dir; research reports; tables; provenance | Research report schema, entity/data table schema, tax ontology |
| **Oil & gas waste research** | O&G waste domains (competitors, water, permits, trucking, P&A, investor, supply chain) | Orchestrate sub-workflows per workflows-oil-gas-waste-research.yaml; limits; aggregate | Per-workflow report + table; aggregated summary; provenance | Report schema, table schema, O&G ontology |
| **Case presentation profiles** | Investor, board, legal team, key personnel, customer, lender, bank profiles | Orchestrate profile agents; output per case-presentation-profile.schema | LexVault or profile store; KG Person/Org/Party | case-presentation-profile.schema.json |
| **Litigation searchers** | Witness, jurisdiction, judge, clerks, law firms, attorneys, litigation finance, RICO | Each searcher agent runs per playbook; structured output; optional orchestration | LexVault parties/KG; research artifact store; provenance | Per-agent schema (witness profile, judge profile, etc.) |
| **Messaging / email / sentiment timeline** | Ingest messaging, sentiment, timeline | Messaging ingestion → timeline → multi-agent review → sentiment summary | LexVault, timeline event schema, sentiment tags | timeline-event.schema, messaging/sentiment schema |
| **YouTube / social / photo evidence** | YouTube, social posts, photo-of-doc to evidence | Ingest → abstract → evidence linkage → KG/timeline | LexVault, evidence-object, timeline, KG | evidence-object.schema, document-abstract schema |

### 2.2 Filing system (canonical locations)

| Output type | Location | Schema / convention |
|-------------|----------|---------------------|
| **LexVault raw** | LexVault raw store (matter-scoped) | Immutable; SHA-256; matter_id, custodian |
| **LexVault derivatives** | LexVault derivatives (OCR, metadata, embeddings) | Versioned; hashed; provenance |
| **Vector index** | Pinecone (or equivalent) matter namespace | Embeddings; matter_id |
| **Knowledge graph** | Neo4j (or equivalent) | Ontology types; matter-scoped |
| **Timeline** | LexVault or timeline store | timeline-event.schema.json |
| **Claim matrix** | Matter artifact store | claim-matrix-entry.schema.json |
| **Research reports / tables** | config output dir or artifact store | Report + table schema; run_id |
| **Provenance / audit** | chain-of-events.jsonl, audit log | run_id, agent_ids, timestamps, artifact IDs |
| **Human checkpoint log** | standards-compliance decision log | Decision, approver, timestamp |

### 2.3 Structured output (schemas) — reference

| Schema | Purpose |
|--------|---------|
| **fact.schema.json** | Extracted facts |
| **timeline-event.schema.json** | Timeline events |
| **claim-matrix-entry.schema.json** | Claim–element–evidence |
| **evidence-object.schema.json** | Evidence items with provenance |
| **reviewer-annotation.schema.json** | Review flags (privilege, PII, etc.) |
| **connector-request.schema.json** | Connector/MCP request shape |
| **bundle-package.schema.json** | Export bundle |
| **case-presentation-profile.schema.json** | Profile (investor, board, etc.) |

---

## 3. Continuous learning: best-in-domain regimen, updates, coordinate sorts and pushes

Each agent and swarm should **gather all knowledge necessary** to become the **best agent that will ever exist in its narrow domain**, with **regular updates** via **cloud agents** and **all available data**, and **coordinate sorts and pushes at every stage**.

### 3.1 Knowledge gathering (best-in-domain)

| Practice | Description |
|----------|-------------|
| **Domain corpus** | Per narrow domain: maintain a **curated corpus** (docs, examples, gold labels, competitor outputs, industry standards). Stored in repo (e.g. `docs/knowledge/`, `data/synthetic/gold/`) or LexVault matter-scoped. |
| **Structured output feedback** | Every run produces **structured output**; compare to gold or attorney feedback; use for **evals** and **retraining or prompt updates**. |
| **Competitor and industry scan** | Regularly ingest **competitor tools and features** (Relativity, Everlaw, DISCO, Luminance, CoCounsel, Harvey, etc.) and **industry standards** (EDRM, Sedona, ABA); add to agent knowledge and skills so the agent can match or exceed them. |
| **OneWish OS and cloud stack** | Agent has access to **OneWish OS** (constitution, config, scripts, MCPs) and **cloud stack** (APIs, vector, KG); use for routing, limits, and context. **Dev stack** (Cursor, scripts, schemas) and **tech stack** (LexVault, practice mgmt, eDiscovery) are part of agent context. |
| **Cloud agent docs review and copy** | Run **cloud agent review** (Full Review or dedicated run); **fully copy** entire **developer docs**, **LLM dev docs**, and **application docs** (config: `config/docs-sources-for-knowledge-copy.yaml`); **save** to `docs/knowledge/`, `docs/knowledge/agent/`, `docs/knowledge/combined/`; **extract** relevant knowledge for agent knowledge and/or combined knowledge. End-to-end: [CLOUD_AGENT_DOCS_REVIEW_AND_KNOWLEDGE_COPY.md](CLOUD_AGENT_DOCS_REVIEW_AND_KNOWLEDGE_COPY.md); script: `./scripts/run-cloud-agent-docs-review-and-copy.sh`. |

### 3.2 Regular updates (cloud agents and all available data)

| Practice | Description |
|----------|-------------|
| **Scheduled refresh** | Run **cloud agents** (or scheduled jobs) that pull **all available data** (new case law, IRS updates, regulations, competitor changelogs, research APIs) into the **domain corpus** or into **vector/KG** so agents see up-to-date context. |
| **Playbook and config sync** | **Never-miss propagation** (OneWish OS): when playbooks, config, or schemas change, **sync** to all repos and agents so every stage uses latest instructions and filing system. |
| **Eval and regression** | **Eval loop** (see docs/EVAL_LOOP_AND_CHAIN_OF_EVENTS.md, evals.md): after runs, compute metrics; log to chain-of-events; compare to baseline. Use to **update** prompts, few-shot examples, or model selection. |
| **Human feedback loop** | Attorney and specialist **feedback** (e.g. reviewer annotations, sign-off comments) is written back to LexVault or audit log; use to **tune** agent behavior and to **retrain or update** gold labels. |

### 3.3 Coordinate sorts and pushes at every stage

| Stage | Sort (what to do) | Push (where it goes) |
|-------|-------------------|----------------------|
| **Intake** | Sort: validate matter, queue docs by custodian/type | Push: matter record to LexVault/config; queue to OCR agent |
| **OCR / ingestion** | Sort: by format (PDF, image, email); quality check | Push: raw to LexVault; derivatives to LexVault; vector index update |
| **Entity extraction** | Sort: by doc, by entity type; resolve duplicates | Push: entities to KG; fact schema to artifact store; LexVault provenance |
| **Claim mapping** | Sort: by claim, element, evidence link | Push: claim matrix to artifact store; LexVault |
| **Evidence linking** | Sort: by exhibit, claim, timeline event | Push: evidence-object to LexVault; timeline update |
| **Review / privilege** | Sort: by batch, by designation (draft); human sign-off | Push: reviewer-annotation to LexVault; decision log; no production without checkpoint |
| **Research** | Sort: by query, by source; dedupe | Push: report + table to output dir; optional LexVault; provenance |
| **Drafting** | Sort: by template, matter context | Push: draft to artifact store; human edit; never auto-file |
| **Bundle / export** | Sort: by matter, by deliverable type | Push: bundle-package to export path; chain-of-events final |

**Coordination:** Orchestrator (or swarm orchestrator) **sorts** at each step (what to process, in what order, with what limits) and **pushes** to the **filing system** (LexVault, artifact store, schema-compliant). **Sorts** respect config (limits, budgets); **pushes** respect schema and provenance so the next stage and downstream systems (including cloud agents and reporting) have consistent data.

### 3.4 Swarm instructions template (for each swarm)

Each swarm should have:

1. **Instructions** — Who runs first, in what order; what each agent reads (LexVault, config, prior stage output) and writes (filing system, structured output); human checkpoint rules; limits and budgets.
2. **Filing system** — Canonical locations (see §2.2) for each output type; naming and matter-scoping.
3. **Structured output** — Schema for every artifact (see §2.3); validation before push.
4. **Update cadence** — How often the swarm’s knowledge and prompts are refreshed (e.g. weekly corpus update, quarterly competitor scan, continuous eval feedback).
5. **Sort and push checklist** — Per-stage sort (what to process, order, limits) and push (where, schema, provenance).

---

## 4. LLM and API routing system; dev-tools forum; check-ins, evals, and human-in-the-loop

Agents must **use the right LLM for the right job**. A **single system** calls on **APIs for any LLM and/or repo**, is **inclusive** (all providers and repos in one routing layer), and is **directed by a forum of dev tools** with **check-ins**, **evals**, and a **continuous improvement loop** that includes **human-in-the-loop steps**.

### 4.1 System to call on APIs for any LLM and any repo (inclusive)

| Element | Purpose |
|--------|---------|
| **LLM API layer** | Single routing layer that can **call any LLM API**: OpenAI, Anthropic, Google (Gemini/Vertex), OpenRouter, Ollama (local/Genie), Azure OpenAI, and any other provider added to config. No agent is locked to one vendor. |
| **Repo and context APIs** | Same system can **call any repo or data source**: LexVault, GitHub, config (playbooks, connectors, ontology), Pinecone, Neo4j, Notion (via MCP), and other connected systems. Routing decides which **context** to pull (matter, tag, subject) and which **LLM** to use for the task. |
| **Right LLM for right job** | Routing rules use **work type**, **data sensitivity**, **capability**, and **cost** (see [LEGAL_TECH_STACK_COST_AND_EVALUATION.md](LEGAL_TECH_STACK_COST_AND_EVALUATION.md) §5). Examples: LexVault/matter data → private (Genie/Ollama); public research → subscription or API economy; high-stakes drafting → private or API premium with human checkpoint. |
| **Config-driven** | Routing table lives in config (e.g. `config/llm-routing.yaml` or `config/connectors.yaml`). Fields: `work_type`, `data_sensitivity`, `preferred_llm_type`, `provider`, `model`, `fallback`, `human_gate`. Orchestrator and scripts read config; no hardcoded provider per agent. |

**Inclusive scope:** Every LLM and every repo we use is **registered** in this system so that (1) any agent can be assigned the best available LLM for its task, and (2) any run can pull the right context from the right repo. New providers or repos are added to config and optionally to evals; they then participate in routing and the improvement loop.

### 4.2 Forum of dev tools that direct routing, check-ins, and evals

A **forum of dev tools** (Cursor, Claude Code, Codex, scripts, MCPs, CI) **directs** routing and improvement: they trigger runs, read/write config, run evals, and enforce check-ins.

| Dev tool / component | Role in directing LLM routing and improvement |
|----------------------|------------------------------------------------|
| **Cursor** | Runs agents and workflows; uses routing config when invoking LLMs (via MCP or env); can trigger eval and check-in scripts. |
| **Claude Code / Codex** | Same: open master repo, run scripts (route-constitution, sync, eval, run-post-run-eval-loop); routing config is source of truth. |
| **Orchestrator / playbooks** | Read `config/llm-routing.yaml` (or equivalent) and `config/connectors.yaml`; pass selected provider/model and context to each agent. |
| **Scripts** | `run-post-run-eval-loop.sh`, `run-full-review.sh`, `run-comprehensive-eval-and-cleanup.sh` produce outcomes that feed the improvement loop; scripts can also **validate** routing config (e.g. all referenced providers have env keys). |
| **MCPs** | MCP servers (e.g. Firecrawl, GitHub, Notion) supply context; connector config defines which MCP is used for which work type; routing decides LLM after context is gathered. |
| **CI / scheduled jobs** | Run evals and check-ins on a schedule; update chain-of-events; optionally suggest routing or prompt changes from regression. |

**Check-ins:** Before a run, the forum can **check in** that (1) routing config is valid, (2) required env/API keys are present, (3) human_gate flags are set for high-stakes work types. After a run, **check-in** = run post-run eval and append to chain-of-events.

### 4.3 Evals in the continuous improvement loop

| Practice | Description |
|----------|-------------|
| **Post-run eval** | After each run (omni-audit, comprehensive-eval, full-review, or workflow run), run **post-run eval** (see [EVAL_LOOP_AND_CHAIN_OF_EVENTS.md](EVAL_LOOP_AND_CHAIN_OF_EVENTS.md)). Metrics (outcome, verify_summary, merge/archive/delete/fix) are written to `chain-of-events.jsonl` and `eval-after-run-latest.json`. |
| **LLM-specific evals** | Where applicable, evals include **which LLM was used** and **outcome** (e.g. pass/warn, quality score). Over time, this data informs routing: e.g. prefer model A for entity extraction, model B for research. |
| **Regression and drift** | Compare outcomes across runs (see EVAL_LOOP §5). If a given (work_type, llm_provider) regresses, the loop can suggest fallback or prompt update. |
| **Update routing and prompts** | Improvement loop **updates** (1) routing table (preferred_llm_type, fallback) and (2) prompts/few-shot examples based on eval results and human feedback. Changes are propagated via never-miss propagation (sync to repos, route constitution). |

### 4.4 Human-in-the-loop steps in the loop

Human-in-the-loop steps are **mandatory** for high-stakes outputs and **optional feedback** for improvement.

| Trigger | Human step | How it feeds the loop |
|---------|------------|------------------------|
| **Privilege / production / filing / damages** | Attorney (or designee) must **approve** before output is used for production, filing, or expert conclusion. Orchestrator blocks until checkpoint passed. | Decision and optional comment are logged (standards-compliance, reviewer-annotation); used as **gold/feedback** for evals and tuning. |
| **Evaluator gate failed** | If evaluator swarm fails (fact, citation, logic, ethics), output is **blocked**; human reviews and either fixes or overrides with justification. | Override and justification are logged; inform eval metrics and future prompt/routing updates. |
| **Routing or model change** | When adding a new LLM provider or changing preferred model for a work type, human **reviews** config and (optionally) runs a smoke test. | Ensures no unintended switch of provider for sensitive work types; change is versioned and propagated. |
| **Eval outcome = warn / fail** | When post-run eval yields warn or fail, human **reviews** recommendations (MERGE, ARCHIVE, DELETE, FIX) and decides next actions. | Human actions (e.g. “fix these 5”) close the loop; next run’s eval measures improvement. |
| **Periodic review of routing table** | On a set cadence (e.g. quarterly), human **reviews** routing table and eval history (which LLM per work type, success rates) and approves or adjusts. | Keeps “right LLM for right job” aligned with practice and cost; avoids drift. |

**Principle:** The continuous improvement loop **always** includes a path for human checkpoints where required by [constitution.md](constitution.md) and [security.md](security.md); human feedback is **ingested** into the loop (eval store, routing config, prompts) so the system improves without removing human control.

### 4.5 End-to-end flow (summary)

1. **Route** — Orchestrator (or dev-tool-triggered script) receives work request; reads **routing config** (work type, sensitivity, preferred LLM, repo context); selects **LLM API** and **repo/context**.
2. **Call APIs** — Call selected **LLM API** (any provider) with context from **repo** (LexVault, config, vector, KG, etc.); run agent/swarm.
3. **Check-in (pre)** — Dev tool or script verifies config and env; human_gate set for high-stakes.
4. **Run** — Execute workflow; emit structured output to filing system.
5. **Check-in (post)** — Run **post-run eval**; append to **chain-of-events**; write eval-after-run-latest.
6. **Human step (if required)** — If privilege/production/filing/damages or gate failed: **block** and wait for human approval; log decision.
7. **Improve** — Use eval results and human feedback to **update** routing table and/or prompts; **propagate** via sync and route-constitution; next run uses updated config.

This ensures **one system** for all LLMs and repos, **directed by dev tools** with check-ins and evals, and **continuous improvement** with **human-in-the-loop** at every required step.

---

## 5. References

| Doc | Purpose |
|-----|---------|
| [playbooks/00-ONEWISH_PLAYBOOKS_INDEX.md](playbooks/00-ONEWISH_PLAYBOOKS_INDEX.md) | All playbooks; link to orchestrator and specialist agents |
| [constitution.md](constitution.md) | Human-in-the-loop; claim typing; audit; API keys and cross-tool execution |
| [security.md](security.md) | RBAC; PII/privilege; audit |
| [modules/lexvault.md](modules/lexvault.md) | LexVault store, ontology, provenance |
| [EVAL_LOOP_AND_CHAIN_OF_EVENTS.md](EVAL_LOOP_AND_CHAIN_OF_EVENTS.md) | Eval loop; chain-of-events; post-run eval; check-in wiring |
| [evals.md](evals.md) | Eval scripts and metrics |
| [LEGAL_TECH_STACK_COST_AND_EVALUATION.md](LEGAL_TECH_STACK_COST_AND_EVALUATION.md) | Stack cost; work types → LLM assignment (right LLM for right job); LitForce/LexVault/OneWish/Genie context |
| [LAW_FIRM_ORG_CHARTS_AND_OUTSOURCED_SERVICES.md](LAW_FIRM_ORG_CHARTS_AND_OUTSOURCED_SERVICES.md) | Org charts; roles; outsourced services; execution org |
| config/playbooks.yaml | Runtime playbook config |
| config/connectors.yaml | Connectors, LLM providers, budgets, human_gate; extend for routing table or use config/llm-routing.yaml |
| config/workflows-intake-engine.yaml | Example: llm_router (open_router_or_local); eval and stages |
| docs/schemas/ | Schema definitions |
| [SOURCES_AND_EMULATION_INDEX.md](SOURCES_AND_EMULATION_INDEX.md) | Canonical map of top sources to emulate by action/agent type; virtuous loop |
| [BEST_PRACTICES_FROM_TOP_REPOS_TO_ADD_OR_EMULATE.md](BEST_PRACTICES_FROM_TOP_REPOS_TO_ADD_OR_EMULATE.md) | Practices from leading repos to add or emulate; adopt in small parts |
| [REFERENCE_PATTERNS_AND_EXAMPLE_REPOS.md](REFERENCE_PATTERNS_AND_EXAMPLE_REPOS.md) | Example repos and patterns for design, structure, agent/MCP/workflow |
| [STARRED_AND_REFERENCE_REPOS.md](STARRED_AND_REFERENCE_REPOS.md) | Starred and reference repos; extend with best-repo-per-variety mapping |

---

**Simulation disclaimer:** Agents and swarms are for litigation support and operations only. Not legal advice. Human checkpoints required for privilege, production, filing, and legal conclusions. Maintain at: docs/AGENTS_ROLES_SWARMS_AND_CONTINUOUS_LEARNING.md.
