# Review — Industry Terms by Specialization, Core, Game Changers, Principles & DevOps

**Purpose:** Expand the mapping of our **Review** (and its parts) to **industry terms, examples, principles, and workflows** across (1) **specialization types** (litigation, privilege, contract, compliance, classification, financial, eDiscovery, PI/PII), (2) **core features**, (3) **game changers**, (4) **principles**, and (5) **rules that guide all DevOps**. Each row translates to **industry speak** for external teams and frameworks.

**Governance:** [REVIEW_RESPONSE_AND_TOP_SOURCES.md](REVIEW_RESPONSE_AND_TOP_SOURCES.md); [GAME_CHANGERS.md](GAME_CHANGERS.md); [best-practices/INSTITUTIONAL_GRADE_BEST_PRACTICES_INDEX.md](best-practices/INSTITUTIONAL_GRADE_BEST_PRACTICES_INDEX.md); [.github/agents/my-agent.agent.md](../.github/agents/my-agent.agent.md).

---

## 1. Industry terms (expanded list) — whole and by part

| Our term | Industry term(s) | Industry speak (how to say it externally) |
|----------|------------------|-------------------------------------------|
| **Review** (all types together) | Quality gate; audit; assessment; evaluation; stage gate; health check; retrospective | “We run a full quality gate before release: governance sync, verification run, audit checklist, and remediation backlog. Same idea as a CI quality gate or a compliance audit.” |
| **Full Review** | Audit; verification run; Plan → Validate → Execute | “We execute a verification run and write an audit summary with technical and plain-language sections and a mandatory sign-off checklist.” |
| **Go flow** | Deployment pipeline; propagation run; governance sync | “We propagate governance to all repos and run a health check; equivalent to a deployment pipeline plus a config audit.” |
| **Genie loop** | Codify-and-run; runbook automation; remediation automation | “We turn recommendations into executable runbooks and run them in dry-run or execute mode; same pattern as infrastructure-as-code or runbook automation.” |
| **Comprehensive eval** | Comprehensive assessment; aggregate audit; remediation backlog (MERGE/ARCHIVE/DELETE/FIX) | “We aggregate findings from verification, 1Password, and connection checks into a single remediation backlog with merge, archive, delete, and fix categories.” |
| **Post-run eval** | Eval loop; metrics persistence; chain of events; observability | “We append one eval record per run to a chain-of-events log and write latest metrics for dashboards or alerts.” |
| **Mandatory checklist** | Human checkpoint; stage gate; sign-off checklist; quality gate checklist | “No release until the sign-off checklist is complete; human checkpoint per 12-Factor and ABA/EDRM.” |
| **Never-miss propagation** | Canonical source propagation; config drift prevention; single source of truth | “We push canonical config and docs from master to all consumers so nothing is missed; same idea as GitOps or config sync.” |
| **Three pillars (success/process/safety)** | Evaluation pillars; quality gate dimensions (Google Cloud) | “We align to success, process, and safety pillars: correctness, trajectory/process, and operational safety (env, secrets, human gate).” |
| **P/D/A/W classification** | Deterministic vs probabilistic vs automated vs workflow; audit taxonomy | “We tag each audited function as deterministic, probabilistic, automated, or workflow so we can reason about reproducibility and risk.” |

---

## 2. By specialization type (with examples and industry speak)

| Specialization | What we do (example) | Industry term | Industry speak |
|----------------|----------------------|---------------|----------------|
| **Privilege** | Privilege reviewer checklist; privilege-scanner agent; no production of privilege-designated content without attorney sign-off | Privilege review; legal hold; privilege log; human-in-the-loop gate | “We run a privilege review workflow with a mandatory attorney sign-off before any production; EDRM/Sedona-aligned privilege log and human gate.” |
| **Contract** | contract-analyst agent; contract extraction and review workflows | Contract review; clause extraction; obligation tracking | “We use a contract analyst agent for extraction and review; outputs are tagged and gated for attorney review before reliance.” |
| **Compliance** | Constitution §1–6; standards-compliance; ABA/EDRM/Sedona/ISO; compliance determinations require human checkpoint | Compliance audit; control check; regulatory alignment | “Compliance-related decisions go through a human checkpoint; we align to ABA, EDRM, Sedona, and ISO 42001 and document the audit trail.” |
| **Classification** | Claim typing (FACT/INFERENCE/OPINION/LEGAL); document/evidence classification; P/D/A/W | Classification taxonomy; tag-based review; evidence coding | “We apply a fixed classification taxonomy (e.g. claim type, P/D/A/W) so every output is tagged for traceability and review.” |
| **Litigation (general)** | Phase checklists (intake → discovery → production → trial prep); litigator/defender roles; evaluator swarm | Litigation phase gates; matter lifecycle; quality gate per phase | “We use phase-based checklists (intake, discovery, privilege, production, trial prep) with a quality gate and sign-off per phase.” |
| **Financial audit / damages** | Financial audit review checklist; damages support; human checkpoint for damages conclusions | Financial audit trail; damages support review; sign-off | “Damages and financial conclusions require a documented audit trail and human sign-off; same as a financial audit review or damages support review.” |
| **eDiscovery** | EDRM alignment; collection → processing → review → production; TAR validation; chain of custody | EDRM workflow; TAR validation; defensible process | “We align to EDRM (collection through production), run TAR validation where used, and maintain chain of custody and audit trail.” |
| **PI / PII review** | PI/PII reviewer checklist; minimize/redact; document basis; retention/access per GDPR/CCPA | Privacy review; PII minimization; data protection impact | “We run a PI/PII review with minimization and redaction; basis and retention are documented; GDPR/CCPA-aligned where applicable.” |
| **Intake** | Intake checklist; matter scope, custodians, legal hold; claim typing at intake | Matter intake; matter onboarding; scope and hold | “Intake is a defined checklist: scope, custodians, legal hold, claim typing; same as matter onboarding or intake quality gate.” |
| **Production** | Production checklist; final privilege/PII check; production log; human approval | Production release; production sign-off; certification | “We treat production as a release: final privilege/PII check, production log, and human certification before release.” |

---

## 3. Core features → industry terms and industry speak

| Core feature | What we do | Industry term | Industry speak |
|--------------|------------|---------------|----------------|
| **Waterfall (layers 1–7)** | OneWish OS → systems → repos → logic → workflows → MCPs → core features | Layered audit scope; dependency-ordered verification | “We run verification in a fixed layered order (top-level down to MCPs and core features) so dependencies are respected.” |
| **LexVault** | Case file storage; evidence ontology; Box/metadata; naming and provenance | Evidence management; document ontology; chain of custody | “We use a single evidence ontology and naming standard with provenance; same idea as evidence management or document ontology with chain of custody.” |
| **KG / graph RAG** | Knowledge graph; graph RAG for retrieval and reasoning | Knowledge graph; graph-augmented retrieval | “We use a knowledge graph and graph-augmented retrieval for matter context; standard pattern for enterprise RAG.” |
| **Evaluator swarm** | Fact, citation, logic, ethics gates before human review | Multi-criteria evaluation; quality gate (fact/citation/logic/ethics) | “We run a multi-criteria evaluation (fact, citation, logic, ethics) before human review; same as an evaluator gate or quality gate.” |
| **Attorney checkpoints** | Human sign-off for privilege, productions, filings, damages, compliance | Human-in-the-loop; sign-off gate; attorney oversight | “High-impact outputs require attorney sign-off; we implement human-in-the-loop gates per ABA and EDRM.” |
| **Verification pipeline** | run-all-verifications → log → summary; routing, connections, schema, taxonomy | Verification pipeline; health check; config audit | “We run a verification pipeline (platform, routing, connections, schema) and persist a log and summary; equivalent to a health check plus config audit.” |

---

## 4. Game changers → industry terms and industry speak

| Game changer | What we do | Industry term | Industry speak |
|--------------|------------|---------------|----------------|
| **OneWish OS** | Master repo; constitution; never-miss propagation; single source of truth; sub-OSes | Platform control plane; governance plane; config as single source of truth | “We treat the platform as a control plane: one source of truth for governance and config, propagated to all sub-systems.” |
| **Full ingestion + one-button** | Backup then ingest; one-button orchestration across tools and workflows | One-click orchestration; full-stack automation; backup-then-ingest | “We run full-stack automation from a single trigger after backup; same idea as one-click orchestration or pipeline trigger.” |
| **First system to build itself** | Ingest systems, reviews, audits, files; infer features; expand by users | Self-improving system; continuous ingestion; feature inference | “The system ingests data and config and infers features; we document outcome and derivative outcomes per run (Constitution §6.5).” |
| **ONEWISH DESKTOP** | One subscription; agents by need; all LLMs; private LLM; OpenCLAW 24/7 | Unified workspace; multi-LLM orchestration; always-on assistant | “We provide a unified workspace with multi-LLM orchestration and an always-on assistant; comparable to a unified dev or legal workspace.” |
| **Neo4j / Timeline / Map** | Graph, timeline, and map as first-class outputs and UX | Graph and spatiotemporal context; timeline and mapping | “We expose graph, timeline, and map as first-class context for matters; same as graph-backed and timeline-backed matter views.” |
| **OCR / evidence ingestion** | OCR and evidence workflows; document abstract/review; privilege/PII flags for attorney review | Document processing; abstract/review; flagging for attorney review | “We run document processing and abstract/review with privilege and PII flags; attorney review before production or reliance.” |
| **Voice agents** | Voice → tool calls, code, workflows; voice-to-terminal; exponential capability | Voice-driven automation; conversational DevOps | “Voice drives tool calls and automation; we treat it as conversational automation or voice-driven DevOps.” |
| **Codify (Genie)** | Recommendations → executable scripts; pre/post checks; dry-run default | Runbook generation; remediation as code; safe-by-default execution | “We turn recommendations into runbooks and run them with pre/post checks and dry-run by default; remediation-as-code pattern.” |

---

## 5. Principles → industry terms and industry speak

| Principle | What we do | Industry term | Industry speak |
|-----------|------------|---------------|----------------|
| **Constitution** | Human-in-loop, claim typing, audit, bias/safety, simulation disclaimer | Governance policy; ethical AI principles; human oversight | “We have a written governance policy: human oversight, claim typing, audit trail, and bias/safety; aligned to ABA/EDRM/Sedona.” |
| **Never-miss propagation** | Route + sync so every target gets updates; no skip | Canonical propagation; config drift prevention; single source of truth | “We propagate from a single source so no target is missed; same as canonical config propagation or GitOps-style sync.” |
| **Human-in-the-loop** | Checkpoints for privilege, productions, filings, damages, compliance | Human checkpoint; sign-off gate; attorney oversight | “We require human sign-off at defined checkpoints; industry term is human-in-the-loop or sign-off gate.” |
| **Claim typing** | FACT / INFERENCE / OPINION / LEGAL; evidence pointer or UNVERIFIED | Assertion taxonomy; evidence linkage; provenance | “Every assertion is tagged and linked to evidence or marked unverified; same as assertion taxonomy or provenance.” |
| **12-Factor / Plan → Validate → Execute** | Verification as core step; validate before execute; human as tool | Verification-first; stage gate; human as tool (12-Factor) | “We verify before we execute and treat the human as a tool in the pipeline; 12-Factor and Plan→Validate→Execute.” |
| **Rigid review** | Usability, operability, efficiency; no bypass | Rigorous review; quality bar; no shortcut | “We apply a rigid review bar (usability, operability, efficiency) with no shortcut; same as rigorous review or quality bar.” |

---

## 6. Rules that guide all DevOps → industry terms and industry speak

| Rule / sequence | What we do | Industry term | Industry speak |
|------------------|------------|---------------|----------------|
| **Sequence: sync → route → verify → review → commit → push** | Exact order in NEVER_MISS_INSTRUCTIONS; run from any dev tool | DevOps pipeline; release pipeline; governance-then-verify-then-release | “We run a fixed pipeline: propagate governance, then verify, then review, then commit and push; same as a release or DevOps pipeline.” |
| **Mandatory checklist** | Full Review not complete until checklist done; 6–9 items | Stage gate; sign-off checklist; quality gate | “We use a mandatory sign-off checklist before we consider the review complete; industry term is stage gate or quality gate checklist.” |
| **Guardrails** | Confirm destructive ops; never commit secrets; validate before write | Guardrails; safety checks; pre-commit hooks | “We enforce guardrails: no destructive action without confirmation, no secrets in repo, validate before write.” |
| **No destructive without approval** | 1Password execute, delete repos, etc.: dry-run first; --execute only with approval | Safe-by-default; explicit approval for destructive actions | “Destructive actions are dry-run by default and require explicit approval; same as safe-by-default or change control.” |
| **Single point of truth (GitHub master)** | All dev tools commit to master; sync propagates to children | Single source of truth; canonical repo; propagation | “Master repo is the single source of truth; all tools commit there and we propagate to child repos.” |
| **Run Review (run-review.sh)** | One command runs go + genie loop + comprehensive | Full quality gate; full audit run; one-command review | “We have one command that runs the full quality gate: go flow, codify, and comprehensive audit; one-command review or full audit run.” |

---

## 7. Frameworks and principles we align with (names they use)

| Framework / source | Terms they use | How we use it |
|--------------------|----------------|---------------|
| **Production-Grade Agentic AI** (arXiv 2512.08769) | Tool-first design; deterministic orchestration; observability; single-responsibility agents | Full Review phases; verification order; summary and log as observability |
| **Orchestral AI** (arXiv 2601.02577) | Deterministic orchestration; bounded judgment; state machines | Go flow and comprehensive eval as deterministic steps |
| **12-Factor Agents** | Verification as core step; Plan → Validate → Execute; human as tool; golden sets | Phase 1 verify then Phase 2 summary; mandatory checklist as human tool |
| **Google Cloud agent evaluation** | Quality gate; three pillars (success, process, safety) | Evaluation pillars in full-review-summary; safety = connections, secrets, constitution |
| **MCP security audit** | Four-phase audit (repo, code, runtime, documentation); cadence | Verification pipeline; connections check; doc in summary and FIX table |
| **TRiSM** (Trust, Risk, Security Management) | Governance; explainability; ModelOps; privacy/security | Constitution; audit trail; human checkpoint; standards-compliance |
| **EDRM** | Collection → processing → review → production; TAR validation; transparency | Litigation phases; privilege/PII review; chain of custody; audit trail |
| **Sedona (2023) AI Commentary** | Transparency; human oversight; bias evaluation; adversarial disclosure | Claim typing; human checkpoint; simulation disclaimer; evaluator swarm |
| **ABA Model Rule 1.1, Comment 8** | Technology competence; attorney oversight of tools and risks | Human-in-the-loop; attorney checkpoints; my-agent.agent.md and constitution |

---

## 8. References

| Doc | Purpose |
|-----|--------|
| [REVIEW_RESPONSE_AND_TOP_SOURCES.md](REVIEW_RESPONSE_AND_TOP_SOURCES.md) | Review response command; defined term “Review”; third-party tools |
| [GAME_CHANGERS.md](GAME_CHANGERS.md) | Game changers list; Genie Magic; charts and graphs every run |
| [best-practices/INSTITUTIONAL_GRADE_BEST_PRACTICES_INDEX.md](best-practices/INSTITUTIONAL_GRADE_BEST_PRACTICES_INDEX.md) | Phase × role matrix; privilege, PI/PII, financial audit, eDiscovery |
| [.github/agents/my-agent.agent.md](../.github/agents/my-agent.agent.md) | Multi-agent specialization; privilege, contract, compliance; standards |
| [audits/REVIEW_AND_AUDIT_STAGES_IMPROVED.md](audits/REVIEW_AND_AUDIT_STAGES_IMPROVED.md) | Three pillars; Plan→Validate→Execute; MCP audit alignment |
| [NEVER_MISS_INSTRUCTIONS.md](NEVER_MISS_INSTRUCTIONS.md) | DevOps sequence; sync → route → verify → review → commit → push |

_Maintain at: docs/REVIEW_INDUSTRY_TERMS_BY_SPECIALIZATION_AND_DEVOPS.md. Update when adding specializations, game changers, or devops rules._
