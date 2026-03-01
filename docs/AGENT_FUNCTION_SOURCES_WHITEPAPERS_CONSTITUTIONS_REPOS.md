# Top White Papers, Constitutions, and Repos — By Agent, Skill, Workflow, and Work Item

**Purpose:** For **every specialty agent, tool, app, skill, workflow, and work item** we use, identify **top white papers**, **constitutions** (governance/ethical/legal standards), and **repos** that define or best exemplify that function. Use for emulation, Full Review sources, and best-repo-per-variety (see [AGENTS_ROLES_SWARMS_AND_CONTINUOUS_LEARNING.md](AGENTS_ROLES_SWARMS_AND_CONTINUOUS_LEARNING.md) §1.5).

**Governance:** [constitution.md](constitution.md); [SOURCES_AND_EMULATION_INDEX.md](SOURCES_AND_EMULATION_INDEX.md); [BEST_PRACTICES_FROM_TOP_REPOS_TO_ADD_OR_EMULATE.md](BEST_PRACTICES_FROM_TOP_REPOS_TO_ADD_OR_EMULATE.md).

**Constitutional / top-level / OneWish OS / Genie desktop / master-synced / never-miss / review:** This doc is **incorporated into and referenced by** constitutional, top-level, OneWish OS, and Genie desktop guidance. Its content is part of **master-synced** and **never-miss** file review: when adding capabilities or running Full Review, ensure **emulation**, **open source repos**, **white papers**, and **dev docs** from the **top LLMs and applications** we use are considered. See [SOURCES_AND_EMULATION_INDEX.md](SOURCES_AND_EMULATION_INDEX.md) §11b (Top LLMs and applications — emulation, OSS, white papers, dev docs) and [ALL_AGENTS_LLMS_MCPS_AND_CONNECTIONS.md](ALL_AGENTS_LLMS_MCPS_AND_CONNECTIONS.md) for the inventory.

---

## 0. Cross-cutting — white papers, constitutions, repos (all agents)

These apply across **all** agents, skills, workflows, and tools. Use as baseline for human-in-the-loop, audit, security, and agent design.

| Type | Source | Scope / use |
|------|--------|-------------|
| **Constitution (ours)** | `docs/constitution.md` | Human-in-the-loop (§1), claim typing (§2), explainability & audit (§3), bias & safety (§4), simulation disclaimer (§5); New Capabilities (§7). |
| **ABA** | ABA Model Rule 1.1 Comment 8 (technology competence); ABA Standard 303 (professional identity, bias awareness, experiential learning) | Ethics; human oversight; tech competence. |
| **EDRM** | EDRM Framework (collection, processing, review, production); EDRM TAR guidelines | eDiscovery phases; TAR validation; transparency. |
| **Sedona** | Sedona Conference (2023) AI Commentary — transparency, explainability, human oversight, bias evaluation, adversarial disclosure | AI in law; oversight; disclosure. |
| **ISO** | ISO/IEC 42001:2023 (AI management); ISO 27001 (security) | AI governance; infosec. |
| **GDPR/CCPA** | GDPR, CCPA (data subject rights, retention, consent) | Data privacy; PII handling. |
| **12-Factor Agents** | [humanlayer/12-factor-agents](https://github.com/humanlayer/12-factor-agents) | Externalized prompts; human via tool; small focused agents; stateless. |
| **Production-Grade Agentic AI** | arXiv 2512.08769 (Agentic Workflows); Google Cloud agent evaluation (three pillars) | Design; tool-first; quality gates. |
| **MCP** | [modelcontextprotocol.info](https://modelcontextprotocol.info), [MCP Best Practice](https://mcp-best-practice.github.io/mcp-best-practice/) | Tool contracts; single responsibility; gateway; observability. |
| **OWASP LLM Top 10** | OWASP LLM Application Security | Prompt injection; data leakage; unsafe output. |
| **TRiSM** | Transparency, Responsibility, Safety, Mitigation (agent/AI governance) | Agent governance framing. |

---

## 1. Orchestrator & workflow coordination

| Function / work item | White papers | Constitutions / standards | Repos |
|----------------------|--------------|---------------------------|-------|
| End-to-end workflow planning, agent routing | Production-Grade Agentic AI (arXiv); Google Cloud agent workflows | Constitution §1 (checkpoints), §3 (audit); EDRM phases | humanlayer/12-factor-agents; LangChain/LangGraph (orchestration patterns); Relativity workflow docs (commercial reference); Everlaw pipeline (commercial); our `docs/playbooks/orchestrator-agent.md` |
| Decomposition, dependency ordering | Agentic Workflows arXiv; Microsoft Multi-Agent design | Constitution §7; 12-Factor (own context) | karpathy/nanoGPT (minimal loop structure); build-nanogpt (incremental steps); config/playbooks.yaml, config/connectors.yaml |
| Human checkpoint enforcement, audit logging | Sedona AI Commentary; ABA Standard 303; EDRM | Constitution §1, §3; ISO 42001 | docs/standards-compliance.md; Evaluator Swarm (constitution §2); our orchestrator playbook |
| Evaluator gate (fact, citation, logic, ethics) | Sedona (human oversight, bias); ABA (ethics) | Constitution §2 (claim typing), §4 (bias) | agents/RICO_Litigation_Intelligence_Agent_v2.md; our evaluator swarm |

---

## 2. Intake, matter setup, document queue

| Function / work item | White papers | Constitutions / standards | Repos |
|----------------------|--------------|---------------------------|-------|
| Matter config validation, matter_id assignment | EDRM (collection scoping); legal hold best practices | Constitution §3 (provenance); EDRM | docs/examples/matter-config.yaml; config/workflows-intake-engine.yaml; Clio/iManage intake (commercial); our intake-agent.md |
| Custodian/party scope, document queue | EDRM collection; FRCP 26(f), 34 | ABA; EDRM; Sedona | LexVault ontology (docs/modules/lexvault.md); Relativity Collect; Everlaw scope; INTAKE_ENGINE_GRAPH_RAG_PINECONE_KNOWLEDGE_GRAPH.md |
| Queue to OCR, file naming, routing | EDRM processing; NIST file integrity | Constitution §3 (audit trail) | OneWish ingestion scripts; Relativity processing queue; docs/playbooks/intake-agent.md |

---

## 3. OCR, document processing, ingestion

| Function / work item | White papers | Constitutions / standards | Repos |
|----------------------|--------------|---------------------------|-------|
| OCR, image-to-text, multi-format | NIST document processing; PDF/A; TIFF specs | EDRM processing; provenance | Tesseract (OCR); Adobe PDF Extract API; Relativity/Everlaw processing; docs/playbooks/ocr-ingestion-agent.md |
| Quality check, derivative storage | EDRM; checksum/hash best practices | Constitution §3 (input_hash, output_hash); ISO 27001 | LexVault (SHA-256, derivatives); docs/modules/lexvault.md; karpathy/llm.c (efficiency patterns) |
| Photo-of-document, social post ingestion | EDRM; social media discovery guidance | Sedona; ABA (competence) | docs/workflows/SOCIAL_POST_AND_PHOTO_DOCUMENT_EVIDENCE_WORKFLOWS.md; photo-document-to-evidence-ingestion.md |

---

## 4. Entity extraction, NER, knowledge graph

| Function / work item | White papers | Constitutions / standards | Repos |
|----------------------|--------------|---------------------------|-------|
| NER (people, orgs, dates, places) | NER/IE surveys; spaCy, Hugging Face NER | Constitution §2 (FACT/evidence); ontology consistency | spaCy NER; Hugging Face transformers NER; Luminance/Kira (legal NER commercial); docs/ontology; docs/schemas (fact, entity) |
| Entity resolution, deduplication | Entity resolution literature; record linkage | EDRM; LexVault ontology | Neo4j (graph); entity resolution libs; docs/modules/ontology.md; entity-extraction-agent.md |
| KG population, schema-first output | Knowledge graph best practices; property-graph (Neo4j) | Constitution §3; LexVault ontology | Neo4j docs; Pinecone (vector); docs/schemas; REFERENCE_PATTERNS_AND_EXAMPLE_REPOS (LitigationForce.AI Neo4j) |

---

## 5. Claim mapping, case theory, issue coding

| Function / work item | White papers | Constitutions / standards | Repos |
|----------------------|--------------|---------------------------|-------|
| Claim–element–evidence mapping | Legal element checklists; FRCP 9(b) (particularity); RICO predicate acts | Constitution §2 (claim typing); ABA | CaseMap (commercial); Everlaw issue coding; Relativity conceptual; docs/ontology (claim taxonomy); claim-mapper-agent.md |
| Claim matrix, issue coding | EDRM review; TAR 2.0 (classification) | Sedona (transparency); EDRM | docs/schemas/claim-matrix-entry.schema.json; Everlaw; claim-mapper workflow |
| Predicate acts, element checklist | RICO (18 USC 1962); civil procedure | ABA; claim typing (LEGAL_CONCLUSION) | docs/ontology; RICO agents; claim-mapper playbook |

---

## 6. Evidence linking, trial support, timeline

| Function / work item | White papers | Constitutions / standards | Repos |
|----------------------|--------------|---------------------------|-------|
| Evidence–claim–fact linking, exhibit numbering | Trial presentation; FRE 901 (authentication); EDRM production | Constitution §3 (provenance); EDRM | Trial Director; TrialLine; Relativity Trial; Opus 2; docs/LITIGATION_EVIDENCE_AND_EXHIBITS.md; evidence-linker-agent.md |
| Timeline, chronology | Litigation chronology best practices; timeline schemas | Constitution §2 (FACT); audit trail | docs/schemas/timeline-event.schema.json; timeline builder agents; party-scrape-kg-timeline-agent.md |
| Provenance, chain of custody | EDRM; NIST chain of custody | Constitution §3; ISO 42001 | docs/modules/lexvault.md; evidence-object.schema.json; standards-compliance.md |

---

## 7. ESI scoping, preservation, legal hold

| Function / work item | White papers | Constitutions / standards | Repos |
|----------------------|--------------|---------------------------|-------|
| Custodian list, data sources, date range | EDRM collection; FRCP 26(f), 34; Zubulake | ABA; EDRM; Sedona | Relativity Collect; Everlaw scope; legal hold platforms; esi-scoping-agent.md; config, checklists |
| Preservation notices, legal hold | EDRM; Zubulake; Rule 37(e) | ABA (duty to preserve); EDRM | Legal hold vendor docs; EDRM model; esi-scoping playbook |

---

## 8. Deposition planning, outlines, exhibits

| Function / work item | White papers | Constitutions / standards | Repos |
|----------------------|--------------|---------------------------|-------|
| Deposition outlines, topic lists, exhibit lists | Deposition practice guides; FRCP 30 | ABA; constitution (human sign-off for strategy) | CaseMap; Opus 2; trial prep tools; deposition-planner-agent.md; timeline + claim matrix as inputs |
| Witness/topic mapping, chronology tie-in | Litigation prep; chronology | Constitution §2 (FACT) | docs/playbooks/deposition-planner-agent.md; timeline schema |

---

## 9. Damages modeling, financial analysis

| Function / work item | White papers | Constitutions / standards | Repos |
|----------------------|--------------|---------------------------|-------|
| Damages modeling, calculations, scenario runs | Forensic accounting; damages experts (Daubert); lost profits, reasonable royalty | Constitution §1 (human checkpoint for conclusions); ABA | cost-estimator.md; financial-audit workflows; Veritext damages (commercial); damages-modeler-agent.md |
| Expert-ready inputs, financial schemas | Expert report standards; Fed. R. Evid. 702 | Sedona (human oversight); ABA | docs/ontology (financial); financial-audit-forensic-damages-agent.md; LexVault financial schemas |

---

## 10. Risk monitor, compliance alerts

| Function / work item | White papers | Constitutions / standards | Repos |
|----------------------|--------------|---------------------------|-------|
| Risk signals, compliance alerts, matter risk flags | Intapp Risk; compliance frameworks; ISO 27001 | Constitution §4 (bias/safety); security.md; ABA | config/connectors.yaml (budgets); security.md; Intapp (commercial); risk-monitor-agent.md |
| Escalation paths, audit trail | EDRM; ISO 42001; OWASP | Constitution §3; RBAC | docs/security.md; LexVault audit; risk-monitor playbook |

---

## 11. Drafting (memos, motions, letters)

| Function / work item | White papers | Constitutions / standards | Repos |
|----------------------|--------------|---------------------------|-------|
| Template-based drafting, citation, tone | Legal writing; citation (Bluebook, ALWD); court rules | Constitution §1 (no auto-file); §2 (LEGAL_CONCLUSION gate); ABA | CoCounsel; Harvey; Lexis+ AI; Westlaw AI; Spellbook (commercial); drafting-agent.md; Genie/Ollama (private LLM) |
| First-draft pleadings, human sign-off | FRCP; local rules; ethics (no unauthorized practice) | Constitution §1 (human checkpoint); ABA Model Rules | docs/playbooks/drafting-agent.md; LexVault matter context |

---

## 12. Document abstract & review, privilege/PII

| Function / work item | White papers | Constitutions / standards | Repos |
|----------------------|--------------|---------------------------|-------|
| Summarization, classification, one-line abstract | TAR 2.0; EDRM review; classification science | Sedona (transparency); EDRM; Constitution §2 | Relativity review; Everlaw AI; Luminance; DISCO AI; document-abstract-and-review-agent.md |
| Privilege/PII draft flags (attorney final call) | Sedona (privilege); ABA (confidentiality); work product | Constitution §1 (privilege human-only); §4 (safety) | Relativity privilege; Everlaw; reviewer-annotation.schema.json; docs/security.md (PII) |
| Responsive/issue tags, provenance | EDRM; TAR validation | Constitution §3; EDRM | docs/playbooks/document-abstract-and-review-agent.md; LexVault provenance |

---

## 13. Legal research (case law, statutes, memos)

| Function / work item | White papers | Constitutions / standards | Repos |
|----------------------|--------------|---------------------------|-------|
| Case law, statutes, secondary sources | Legal research methodology; citation validation | Constitution §2 (citation validator); ABA | Lexis; Westlaw; Casetext; vLex; CoCounsel (commercial); research playbooks |
| Memo drafting, citation check | Legal writing; Bluebook/ALWD | Constitution §2 (LEGAL_CONCLUSION); ABA | Drafting agent refs; research-litigation-finance.md; jurisdiction-research-agent.md |
| Matter-specific vs public research | Data sovereignty; client confidences | Constitution §1; security.md (no client data to public LLM) | LexVault (matter); Genie (private); LEGAL_TECH_STACK §5 (LLM routing) |

---

## 14. Witness, jurisdiction, judge, clerks, law firms, litigation finance (research agents)

| Function / work item | White papers | Constitutions / standards | Repos |
|----------------------|--------------|---------------------------|-------|
| Witness background, impeachment, prior statements | Impeachment (FRE 613, 801); public records | Constitution §2 (FACT); ABA | Westlaw People; public records APIs; witness-research-agent.md; Brave/Firecrawl MCP |
| Jurisdiction, venue, choice of law | Civil procedure; venue statutes; 28 USC 1404 | ABA; claim typing | Lexis; Westlaw; Court API; jurisdiction-research-agent.md |
| Judge tendencies, rulings, biography | Judicial analytics; sentencing/civil studies | Constitution §2 (OPINION/LEGAL); ABA | Lexis CourtLink; Ravel; judge-research-agent.md; civil-rico-judges-agent.md |
| Law clerks, chambers procedures | Court rules; chambers practices | ABA | clerks-research-agent.md; structured output |
| Law firm intel, litigation finance | Competitive intelligence; litigation finance reports | Matter type, claim type | law-firms-research-agent.md; research-litigation-finance.md; case-presentation profiles |
| Case evaluation, trend analysis | Case valuation; litigation analytics | Constitution §1 (human for conclusions); ABA | case-evaluation-agent.md; trend-analysis-agent.md; cost-estimator.md; LexVault claim matrix |

---

## 15. Tax / IRS / damages defense (orchestrator + specialists)

| Function / work item | White papers | Constitutions / standards | Repos |
|----------------------|--------------|---------------------------|-------|
| Tax damages defense, IRS, NOL/OIC/QOZ | IRS publications; tax procedure; OIC, NOL, QOZ regs | Constitution §1 (human for conclusions); ABA; CPA/counsel | docs/knowledge/IRS_BANKRUPTCY_QOZ_OIC_NOL_AND_LOOKBACK.md; config/agents-irs-tax-specialists.yaml; irs-tax-specialist-orchestrator.md |
| Sub-workflow orchestration, limits, aggregate | Production-Grade Agentic AI; workflow design | Constitution §3 (provenance); config limits | orchestrator-tax-damages-defense-research.md; playbooks (NOL, OIC, QOZ, bankruptcy, deadlines, etc.); Bloomberg Tax, Checkpoint (commercial) |
| Tax ontology, entity/account master | Tax entity structures; account mapping | LexVault; ontology | config/ontology/tax-ontology.yaml; entity-account-master-file-agent.md; ira-itc-tax-evidence-litforce-agent.md |

---

## 16. Oil & gas waste research (orchestrator + sub-workflows)

| Function / work item | White papers | Constitutions / standards | Repos |
|----------------------|--------------|---------------------------|-------|
| O&G waste, water, permits, trucking, P&A, capital | Energy sector reports; environmental regs; permits (R20, etc.) | Constitution (simulation disclaimer); research only | config/workflows-oil-gas-waste-research.yaml; orchestrator-oil-gas-waste-research-swarm.md; research-oil-gas-*.md playbooks; S&P Global, Enverus (commercial) |
| Competitors, investor calls, supply chain | Industry research; investor materials | Same | research-oil-gas-competitors-investment-bankers.md; research-oil-gas-equipment-supply-chain.md; Brave, Firecrawl |

---

## 17. Case presentation profiles (investor, board, legal, key personnel, customer, lender, bank)

| Function / work item | White papers | Constitutions / standards | Repos |
|----------------------|--------------|---------------------------|-------|
| Profile building, KG Person/Org/Party | Litigation finance pitch; judge/jury presentation; entity profiles | Constitution §2 (FACT/OPINION); ABA | case-presentation-profiles-orchestrator.md; investor-profile-agent.md; docs/schemas/case-presentation-profile.schema.json; KG + LexVault |
| Role relationships, structured output | Schema-first design; MCP contracts | Constitution §3 | REFERENCE_PATTERNS; profile playbooks |

---

## 18. Messaging, email, sentiment, timeline

| Function / work item | White papers | Constitutions / standards | Repos |
|----------------------|--------------|---------------------------|-------|
| Messaging ingestion, timeline, sentiment | EDRM (email); sentiment analysis; communication discovery | Constitution §3; Sedona; EDRM | messaging-ingestion-agent.md; messaging-timeline-agent.md; messaging-multi-agent-review-agent.md; messaging-sentiment-summary-agent.md; timeline-event.schema |
| Multi-agent review, summary | TAR; multi-agent design | Sedona (transparency); 12-Factor | docs/workflows/MESSAGING_EMAIL_SENTIMENT_TIMELINE_WORKFLOW.md |

---

## 19. YouTube, social, photo evidence ingestion

| Function / work item | White papers | Constitutions / standards | Repos |
|----------------------|--------------|---------------------------|-------|
| YouTube/social search, evidence ingestion | Social media discovery; authentication (FRE 901); EDRM | Constitution §2 (FACT); ABA; Sedona | youtube-search-evidence-agent.md; social-post-search-evidence-agent.md; photo-document-to-evidence-ingestion.md; evidence-object.schema |
| Video transcript, comments, linkage to timeline | EDRM; transcript standards | Constitution §3 | youtube-to-evidence-ingestion.md; INTAKE_ENGINE; LexVault |

---

## 20. Financial audit, forensic, comprehensive financial review

| Function / work item | White papers | Constitutions / standards | Repos |
|----------------------|--------------|---------------------------|-------|
| Statement vs receipt reconciliation, assets/liabilities | Forensic accounting; GAAP; audit standards | Constitution §1 (human for conclusions); ABA; CPA | financial-audit-forensic-damages-agent.md; docs/ontology/FINANCIAL_AUDIT_FORENSIC_DAMAGES_ONTOLOGY.md; config/workflows-financial-audit-forensic-damages.yaml |
| Comprehensive financial interaction review | Payments, expenses, income, tax, HR, predicate acts | Same; RICO (predicate acts) | comprehensive-financial-interaction-review-agent.md; docs/workflows/COMPREHENSIVE_FINANCIAL_INTERACTION_REVIEW_WORKFLOW.md |

---

## 21. Skills, MCP tools, and dev-tool integrations

| Function / work item | White papers | Constitutions / standards | Repos |
|----------------------|--------------|---------------------------|-------|
| Cursor skills (when/how to use) | Skill format (YAML, instructions, examples) | Constitution §7 (create skill); NEW_CAPABILITY_CHECKLIST | .cursor/skills/create-skill/SKILL.md; .cursor/skills/*/SKILL.md |
| MCP tools, contracts, single responsibility | MCP Best Practice; modelcontextprotocol.info | 12-Factor; gateway pattern | config/canonical-mcp-connectors.yaml; MASTER_MCP_CONNECTORS_APIS.md; MCP server descriptors |
| LLM routing, right-LLM-for-right-job | LEGAL_TECH_STACK §5; cost/sensitivity/capability | Constitution §1 (sensitive data); security.md | config/connectors.yaml; config/llm-routing (or equivalent); AGENTS_ROLES_SWARMS §4 |
| Eval loop, chain-of-events, check-ins | Production-Grade Agentic AI; eval harness design | Constitution §3 (audit); EVAL_METRICS_FLAGS_AND_METHODS | EVAL_LOOP_AND_CHAIN_OF_EVENTS.md; run-post-run-eval-loop.sh; evals.md |
| Open-source-first, best-repos-per-variety | SOURCES_AND_EMULATION_INDEX; Karpathy-style minimalism | Constitution §7; AGENTS_ROLES §1.5 | SOURCES_AND_EMULATION_INDEX.md §10b; BEST_PRACTICES_FROM_TOP_REPOS; STARRED_AND_REFERENCE_REPOS.md |

---

## 22. Reference: where this doc is used

| Use case | Doc / script |
|----------|--------------|
| **New agent or capability** | NEW_CAPABILITY_CHECKLIST; constitution §7; AGENTS_ROLES_SWARMS §1.5 — pick white papers/constitutions/repos for this function from this doc. |
| **Full Review (emulation sources)** | QUICK_AND_FULL_REVIEW; full-review-summary.md — list “top repos & whitepapers” per change; use tables above. |
| **Best-repo-per-variety** | AGENTS_ROLES_SWARMS §1.5 — extend with specific repo names from §1–§21; STARRED_AND_REFERENCE_REPOS. |
| **Playbook authoring** | Each playbook in docs/playbooks/ should reference the row(s) here for that agent’s function. |

---

**Maintain at:** docs/AGENT_FUNCTION_SOURCES_WHITEPAPERS_CONSTITUTIONS_REPOS.md. Update when adding agents, skills, workflows, or when new white papers/constitutions/repos become authoritative for a function.
