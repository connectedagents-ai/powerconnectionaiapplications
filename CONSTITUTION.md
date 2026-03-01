# CONSTITUTION.md - Universal AI Agent Constitution
# Connected Energy.AI / LitigationForce.AI
# Effective: 2026-02-20 | Last Amended: 2026-02-21

This document is the **binding constitution** for all AI agents, assistants, and dev tools
operating across the Connected Energy.AI ecosystem. Every tool (Claude Code, Cursor, Codex,
GitHub Copilot, Windsurf, etc.) MUST read and obey this file.

**DISCLAIMER**: All litigation outputs are **Simulation / Not Legal Advice**.

---

## Article I: Identity & Scope

### 1.1 The Platform
**Connected Energy.AI** is the parent enterprise. Its primary product is **LitigationForce.AI**,
a Social Agent Orchestration System for litigation intelligence.

### 1.2 Canonical Repos (post-consolidation)

| # | Repo | Purpose | Status |
|---|------|---------|--------|
| 1 | `Connected-Energy-AI/LitigationForce.AI` | Core platform: agents, models, MCP, graph, ontology | PRIMARY |
| 2 | `connectedagents-ai/litigationforce.nextjs-ai-chatbot` | Next.js chatbot UI | ACTIVE |
| 3 | `connectedagents-ai/ai-sdk-starter-xai-litforce` | AI SDK starter kit | ACTIVE |
| 4 | `connectedagents-ai/litigationagentskubernetis` | Kubernetes deployment | ACTIVE |

### 1.3 Accounts

| Account | Role |
|---------|------|
| `Connected-Energy-AI` | Organization (primary) |
| `connectedagents-ai` | Personal (Robert Bailey) |
| `NuTech-Ventures` | Organization (ventures) |

---

## Article II: Autonomous Operation Protocol

### 2.1 Default Behavior: Act, Don't Ask

All AI agents operating in this ecosystem SHALL:
- **Proceed immediately** when intent is clear
- **Follow existing patterns** in the codebase
- **Fix issues proactively** (failing tests, missing exports, lint errors)
- **Create tests** for new code automatically
- **Only pause** for irreversible or safety-critical actions

### 2.2 Decision Authority Matrix

| Action | Authority | Requires Confirmation |
|--------|-----------|----------------------|
| Create/modify files under `src/`, `tests/`, `examples/`, `docs/` | AUTONOMOUS | No |
| Add agents, models, scrapers, connectors | AUTONOMOUS | No |
| Add dependencies to `pyproject.toml` | AUTONOMOUS | No |
| Fix lint, type, formatting errors | AUTONOMOUS | No |
| Write and run tests | AUTONOMOUS | No |
| Create branches and commits | AUTONOMOUS | No |
| Push to feature branches | AUTONOMOUS | No |
| Change `simulation_mode` or `block_filing_directives` | REQUIRES APPROVAL | Yes |
| Modify MCP policy enforcement | REQUIRES APPROVAL | Yes |
| Force-push or rebase shared branches | REQUIRES APPROVAL | Yes |
| Modify ontology namespace URIs | REQUIRES APPROVAL | Yes |
| Delete production data or branches | REQUIRES APPROVAL | Yes |

### 2.3 Safety Guards (NEVER change without explicit approval)

```python
simulation_mode = True              # All external actions are simulated
block_filing_directives = True      # No real court filings
background_include_social = False   # No scraping without explicit consent
```

---

## Article III: Architecture

### 3.1 Dual Deployment Model

Every agent exists in two forms:
1. **Claude-native**: Runs inside Claude Code / Desktop via `.claude/commands/` + MCP
2. **Portable runtime**: Runs anywhere via `src/runtime/` with pluggable LLM adapters

### 3.2 Layer Model

```
Layer 4: DEV TOOLS (Claude Code, Cursor, Codex, Copilot)
         Read constitution, execute skills, push code
              |
Layer 3: AGENT ORCHESTRATION (src/orchestration/)
         CompositeAgent, ParallelAgent, ConditionalAgent
              |
Layer 2: PLATFORM SERVICES (src/mcp/, src/graph/, src/runtime/)
         MCP connectors, Neo4j, LLM adapters, agent registry
              |
Layer 1: DOMAIN LOGIC (src/agents/, src/models/, src/ontology/)
         Litigation agents, RICO models, Veritas ontology
              |
Layer 0: INFRASTRUCTURE (Docker, Celery, Redis, Neo4j)
         Task queues, graph DB, cache, message broker
```

### 3.3 Agent Hierarchy

```
BaseAgent (src/orchestration/base.py)
├── CompositeAgent     - Sequential multi-agent execution
├── ParallelAgent      - Concurrent execution with semaphore
├── ConditionalAgent   - Predicate-based branching
├── BaseLitigationAgent - All litigation domain agents
│   ├── ClaimMapperAgent, PatternAnalyzerAgent
│   ├── DamagesModelingAgent, DepositionPlannerAgent
│   ├── RiskMonitorAgent, DraftingAgent, ExpertPlanningAgent
│   └── ESIScopeAgent
├── ScraperAgent / MultiPlatformScraperAgent
├── ClaudeAnalysisAgent (+ 6 specialized subclasses)
├── KnowledgeGraphAgent
├── ThreadIntelligenceAgent
├── BrandVoiceAgent
├── LegalDiscoveryOrchestrator
├── ContractEnforcerAgent
└── DataValidationAgent
```

---

## Article IV: Cross-Tool Communication Protocol

### 4.1 Shared Vocabulary

All dev tools MUST use these terms consistently:

| Term | Definition |
|------|-----------|
| **Agent** | Autonomous unit of work with typed I/O, lifecycle, and audit trail |
| **Skill** | Claude Code slash command (`.claude/commands/*.md`) |
| **Worker** | Background Celery task for async processing |
| **Connector** | MCP connector for external data access |
| **Orchestrator** | Agent that coordinates other agents |
| **Pipeline** | Sequential chain of agents processing data |
| **Swarm** | Parallel execution of multiple agents |
| **Constitution** | This document - the binding rules for all tools |
| **Platform** | Reusable components shared across all applications |
| **Application** | Domain-specific logic (e.g., litigation, security) |

### 4.2 File-Based Communication

All dev tools communicate through these canonical files:

| File | Purpose | Read By |
|------|---------|---------|
| `CONSTITUTION.md` | Universal rules for all tools | ALL |
| `CLAUDE.md` | Claude Code specific instructions | Claude Code |
| `docs/AGENTS.md` | Agent & worker definitions | ALL |
| `.cursorrules` | Cursor-specific instructions | Cursor |
| `.github/copilot-instructions.md` | GitHub Copilot instructions | Copilot |
| `codex.md` | OpenAI Codex instructions | Codex |
| `.windsurfrules` | Windsurf-specific instructions | Windsurf |
| `docs/PLATFORM_ARCHITECTURE.md` | Architecture reference | ALL |
| `docs/MASTER_PLAN.md` | Development roadmap | ALL |
| `.mcp.json` | MCP server connections | Claude Code, Cursor |
| `plugin.json` | Claude Code plugin manifest | Claude Code |

### 4.3 Bilateral Push Protocol

When any dev tool makes changes, it MUST:

1. **Update the canonical source** (this repo)
2. **Propagate constitution changes** to all tool-specific config files
3. **Use conventional commits**: `type(scope): message`
4. **Run quality checks** before committing: `black`, `ruff`, `mypy`, `pytest`

### 4.4 Change Propagation Rules

```
CONSTITUTION.md (source of truth)
    |
    ├──> CLAUDE.md (auto-sync relevant sections)
    ├──> .cursorrules (auto-sync relevant sections)
    ├──> .github/copilot-instructions.md (auto-sync)
    ├──> codex.md (auto-sync)
    └──> .windsurfrules (auto-sync)
```

When CONSTITUTION.md changes, the `/sync-constitution` skill propagates updates
to all tool-specific files automatically.

---

## Article V: Code Standards

### 5.1 Mandatory

| Tool | Config |
|------|--------|
| Formatter | Black (line-length 100) |
| Linter | Ruff (rules: E, F, I, N, W, UP) |
| Type checker | mypy (strict: disallow_untyped_defs=true) |
| Docstrings | Google-style |
| Tests | pytest + pytest-asyncio (mode=auto) |
| Coverage | 80% minimum for new code |

### 5.2 Naming

| Element | Convention | Example |
|---------|-----------|---------|
| Files | snake_case | `claim_mapper_agent.py` |
| Classes | PascalCase | `ClaimMapperAgent` |
| Functions | snake_case | `map_claims_to_facts()` |
| Constants | UPPER_SNAKE | `MAX_RETRY_COUNT` |
| Private | _prefix | `_validate_request()` |
| Enums | UPPER_SNAKE values | `ClaimType.RICO_ENTERPRISE` |

### 5.3 Patterns

- **Async everything** for I/O operations
- **Pydantic v2** for all data models with full type hints
- **structlog** for all logging (JSON, context-bound)
- **tenacity** for all retry logic (3 attempts, exponential backoff)
- **Field(default_factory=...)** for mutable defaults
- **SecretStr** for all API keys in settings

### 5.4 Commits

```
type(scope): brief imperative summary

Types: feat, fix, docs, style, refactor, test, chore, perf
Scopes: agents, models, scrapers, mcp, graph, ontology, orchestration,
        evaluations, config, cli, utils, runtime, constitution
```

---

## Article VI: MCP Integration Map

### 6.1 Platform as MCP Server (others connect to us)

```json
{
  "connected-energy": {
    "command": "python",
    "args": ["-m", "src.mcp.stdio_server"],
    "note": "Master Platform: litigation, graph, agents"
  }
}
```

### 6.2 Platform as MCP Client (we connect to others)

| Server | Purpose | Protocol |
|--------|---------|----------|
| GitHub | PRs, issues, code reviews | HTTP MCP |
| Sentry | Error monitoring | HTTP MCP |
| Slack | Team communication | HTTP MCP |
| Notion | Documentation, case files | HTTP MCP |
| Linear | Issue tracking | HTTP MCP |
| Context7 | Library docs for AI | HTTP MCP |
| Neo4j | Graph database | Custom (stdio) |

---

## Article VII: Security

1. **Never commit secrets.** Use `.env` + `SecretStr`
2. **Simulation mode stays on.** Always.
3. **MCP policy enforcement is sacred.** No bypassing audit, terms, or purpose.
4. **Rate limiting is mandatory.** Every external request through `RateLimiter.acquire()`
5. **Audit everything.** `AuditLogEntry` for all MCP requests.
6. **Platform ToS compliance.** `background_include_social = False` by default.

## Article VII-A: Infrastructure & One-Shot Terminal Operations

### 7A.1 Docker Services (Layer 0)

`docker-compose up` starts the full stack:

| Service | Image | Port | Purpose |
|---------|-------|------|---------|
| **neo4j** | neo4j:5-community | 7474, 7687 | Graph DB (social graph, relationships) |
| **redis** | redis:7-alpine | 6379 | Task queue broker + cache |
| **app** | Dockerfile:dev | 8000 | Python application server |
| **worker** | Dockerfile:worker | — | Celery worker (4 queues: scraping, analysis, litigation, graph) |

Docker containers are the **bottom layer** of the system. MCP connectors and agents
run inside the `app` container and talk to Neo4j and Redis through Docker's internal network.

### 7A.2 MCP Connection Map

```
AI Dev Tool (Claude Code, Cursor, etc.)
    │
    ├── connected-energy (stdio) ─── python -m src.mcp.stdio_server
    │     ├── litigation_docket_search    → DocketConnector    (60/min)
    │     ├── litigation_corporate_lookup → CorporateConnector (60/min)
    │     ├── litigation_news_search      → NewsConnector      (30/min)
    │     ├── litigation_patent_search    → PatentConnector    (60/min)
    │     ├── litigation_social_scan      → SocialConnector    (10/min)
    │     ├── litigation_storage_enumerate→ StorageConnector   (60/min)
    │     └── litigation_sanctions_check  → SanctionsConnector (60/min)
    │         ALL simulation stubs until explicitly switched to live
    │
    ├── github (HTTP)   → PR/issue/review management
    ├── sentry (HTTP)   → Error monitoring
    ├── slack (HTTP)    → Team notifications
    ├── notion (HTTP)   → Documentation/case files
    ├── linear (HTTP)   → Issue tracking
    └── context7 (HTTP) → Library docs for AI
```

Data flow: MCP tool call → MCPServer validates/rate-limits → Connector executes →
Results cached (15 min TTL) → Audit log entry written.

### 7A.3 GitHub Authentication (Required for One-Shot Operations)

For any dev tool to create PRs, manage issues, or sync repos from the terminal,
GitHub authentication MUST be configured. Do this once:

```bash
# Option 1: Interactive (recommended for Mac)
gh auth login

# Option 2: Token-based (for CI/servers)
echo "ghp_YOUR_TOKEN" | gh auth login --with-token

# Option 3: Environment variable (for .env)
export GITHUB_TOKEN=ghp_YOUR_TOKEN
```

Without this, `gh pr create`, `gh issue create`, and cross-repo sync will fail with 401.
Git push/pull may still work if SSH keys are configured or the repo uses a local proxy.

### 7A.4 One-Shot Terminal Commands

After Docker + gh auth are set up, any dev tool can run these directly:

| Task | Command |
|------|---------|
| Start all services | `docker-compose up -d` |
| Run tests | `make quality` (lint + type + test) |
| Create PR | `gh pr create --title "..." --body "..."` |
| Check PR status | `gh pr status` |
| Cross-repo sync | `python scripts/cross_repo_sync.py push` |
| Start Celery worker | `make worker` |
| Seed test data | `python scripts/seed_data.py` |
| Full dev setup | `./scripts/setup.sh` |

### 7A.5 Makefile Quick Reference

```
make setup       # Full dev environment setup
make quality     # lint + typecheck + test (pre-commit equivalent)
make docker-up   # Start Neo4j + Redis + App
make docker-down # Stop all services
make test        # pytest
make lint-fix    # Auto-fix linting issues
make format-fix  # Auto-format with Black
```

---

## Article VIII: Learnings & Best Practices

These are hard-won lessons from building and consolidating this codebase. All AI agents
MUST internalize these before making changes.

### 8.1 Repository Hygiene

- **Keep the root clean.** Only `README.md`, `CLAUDE.md`, `CONSTITUTION.md`, `CONTRIBUTING.md`,
  `codex.md`, and `pyproject.toml` belong in root. Everything else goes in `docs/` or `src/`.
- **One source of truth per concept.** If agent instructions exist in CLAUDE.md, don't duplicate
  them in AGENT_INSTRUCTIONS.md. Reference, don't repeat.
- **Archive, don't delete.** Move outdated files to `docs/archive/` so history is preserved.
- **No copy-paste from other projects.** The README once had Google ADK/Gemini examples copied
  from `google/adk-python`. Every code example must use OUR actual imports and patterns.

### 8.2 Branch Management

- **Never let 50+ branches accumulate.** Merge or close branches within 1 week.
- **Branch consolidation recipe** (proven with 79 branches):
  1. Sort branches oldest-to-newest
  2. Merge with `git merge -X theirs --allow-unrelated-histories`
  3. Verify every file reference exists after merge
  4. Use `--allow-unrelated-histories` when branches have no common ancestor
- **The `master` branch may not exist on remote.** Always check with `git branch -r` before
  assuming `origin/master` exists.

### 8.3 Simplicity Over Sophistication

- **A beginner must be able to understand the system in 10 minutes.** If they can't,
  it's overcomplicated.
- **Fewer files > more files.** 5 well-organized docs beat 20 scattered ones.
- **Code examples must actually work.** Every snippet in README or docs should use real
  imports from `src/` and match the actual API.
- **Don't add governance files proactively.** Only create new `.md` files when there's a
  clear unmet need. Most information belongs in CLAUDE.md or CONSTITUTION.md.

### 8.4 Agent Development

- **Always inherit from BaseAgent.** This gives you lifecycle, timeout, retry, and logging for free.
- **Every agent returns AgentResult.** Never return raw data — wrap it so callers get
  `success`, `error`, `duration_ms`, and `logs`.
- **Use ParallelAgent for I/O-bound work.** Scraping 6 platforms sequentially is 6x slower
  than parallel.
- **Rate limiting is not optional.** Every HTTP call goes through `RateLimiter.acquire()`.
  Getting IP-banned breaks the whole system.
- **Test agents with mock data.** Don't require real API keys for unit tests.

### 8.5 Data Model Discipline

- **All models use Pydantic v2.** No dataclasses for data that crosses module boundaries.
- **Scores are always 0.0-1.0.** Use `Field(ge=0.0, le=1.0)`.
- **IDs use `Field(default_factory=lambda: str(uuid4()))`.** Never generate IDs manually.
- **Datetime fields use `Field(default_factory=datetime.utcnow)`.** Never use `datetime.now()`.
- **Mutable defaults use `Field(default_factory=list)`.** Never use `= []` as a default.

### 8.6 Cross-Tool Coordination

- **CONSTITUTION.md is the single source of truth.** All tool configs derive from it.
- **Run `/sync-constitution` after editing CONSTITUTION.md.** This propagates changes to
  `.cursorrules`, `copilot-instructions.md`, `codex.md`, and `.windsurfrules`.
- **Every dev tool should produce the same output for the same task.** If Claude Code and
  Cursor produce different code for "add a new agent", the instructions are ambiguous.
- **Conventional commits everywhere.** `type(scope): message` — this enables automated
  changelogs and cross-repo sync triggers.

### 8.7 Reliability Principles

- **Async context managers for all clients.** `async with scraper:` ensures cleanup.
- **Structured logging with context.** `logger.bind(agent=name)` so you can trace any
  operation across the system.
- **Fail fast, recover gracefully.** Validate inputs early with Pydantic. Catch errors
  at agent boundaries and return `AgentResult(success=False, error=...)`.
- **Never silence exceptions.** Always log with `logger.error(...)` before re-raising or
  returning failure.
- **Timeouts on everything.** `asyncio.wait_for(task, timeout=300)` — no agent should
  run forever.

### 8.8 Agent Tools & Skills Registry

The following tools, skills, and techniques have been proven effective across sessions and are
the canonical approaches for this project.

**Import & Module Resolution:**
- Use Python AST parsing (`ast.parse`) to build ground-truth maps of class definitions across files
- When fixing broken imports: scan ALL model files first, then rewrite `__init__.py` in one pass
- Never import a name without verifying it exists in the source file
- Python 3.11: use `X | None` instead of `Optional[X]`, `list[str]` instead of `List[str]`
- `callable` (builtin) cannot use `|` syntax — always use `Callable` from `typing`

**Testing:**
- Run `pytest tests/ -q` for quick validation; `-x` to stop on first failure
- When a Pydantic model has `Field(max_length=N)`, test data MUST respect that constraint
- For settings tests that depend on environment: explicitly set values in the test constructor
- Never rely on CI environment variables matching local development defaults

**Budget/Framework Pattern:**
- `CaseStateManager.create_framework()` creates empty framework shells
- Business logic (e.g., `BudgetManager.create_budget()`) must initialize collections
  before iterating over them — the framework won't do it for you
- UTBMS phases (L100-L700) with task codes must be pre-populated before cost estimation

**Intent Parsing:**
- Natural language patterns must account for articles: "create a budget" not just "create budget"
- Test commands should match what users actually type, not just keyword substrings
- Always add the most common phrasing variants to intent parsers

**Proven Session Skills:**
- `/whats-next` — determine highest-priority next action based on current state
- `/sync-constitution` — propagate CONSTITUTION.md changes to all dev tool configs
- `/cross-repo-sync` — propagate changes across all Connected Energy.AI repos
- `/setup-check` — verify development environment is properly configured
- `/run-quality-checks` — run linting, formatting, and type checking
- `/session-review` — end-of-session knowledge capture (see 8.9)

**Commit Discipline:**
- Commit after each logical unit of work, not at end of session
- Use `type(scope): message` conventional format
- Pre-commit: `black src tests && ruff check src tests --fix && pytest`
- Session progression: fix imports → fix tests → add features → memorialize learnings

### 8.9 Session Review Protocol (Mandatory)

Every AI agent MUST run `/session-review` (or follow its protocol) before ending any session
that involved code changes or lasted more than 30 minutes.

**The 5-step protocol:**

1. **Inventory** — `git log --oneline --since="8 hours ago"` to see what changed
2. **Extract** — Identify new learnings in 5 categories:
   - Agent skills & knowledge
   - Tools, CLIs & terminal commands
   - MCP & API connections
   - Infrastructure & Docker
   - Code patterns & bug fixes
3. **Memorialize** — Write learnings to the appropriate file:
   - Universal rules → CONSTITUTION.md Article VIII
   - Code patterns → CLAUDE.md
   - Infrastructure → CONSTITUTION.md Article VII-A
   - New skill → `.claude/commands/<name>.md`
4. **Propagate** — Run `/sync-constitution` and `/cross-repo-sync` if constitution changed
5. **Summarize** — Commit with session summary in the message

**connectedagents.ai learning loop:**
The downstream repos (`litigationforce.nextjs-ai-chatbot`, `ai-sdk-starter-xai-litforce`,
`litigationagentskubernetis`) in the `connectedagents-ai` account are part of the continuous
learning cycle. Changes to models, MCP, API, or infrastructure propagate to them via
`/cross-repo-sync`. Changes from those repos propagate back via bilateral sync.

**Built-in memory system (`src/memory/`):**
The codebase includes a persistent memory system for runtime knowledge:
- `ConversationOrchestrator` — manages session lifecycle with Neo4j persistence
- `ConversationManager` — stores messages, context, facts across sessions
- `MemoryAwareAgent` — wraps agents to inject prior context automatically
- `ProjectMemory` — project-level shared knowledge across conversations
- `src/evals/` — benchmarks and evaluation runners for measuring quality over time

This means knowledge is captured at TWO levels:
1. **Constitution level** (this file) — rules, patterns, skills for AI dev tools
2. **Runtime level** (`src/memory/`) — facts, findings, context for running agents

**Efficiency rule:** Only memorialize things that would save time if known next session.
One line per learning beats a paragraph. If it's file-specific, put it in that file's
docstring, not the constitution.

---

## Article VIII-B: Complete Module Registry

Every module under `src/` and its purpose. **All AI tools MUST know these exist.**

### Core Platform Modules

| Module | Path | Purpose | Key Exports |
|--------|------|---------|-------------|
| **Agents** | `src/agents/` | 70+ specialized AI agents across 8 categories | All agent classes |
| **Agents/Athena** | `src/agents/athena/` | Budget management, dossier generation, UTBMS frameworks | `AthenaAgent`, `BudgetManager` |
| **Agents/Litigation** | `src/agents/litigation/` | 15 litigation-specific agents (RICO, evidence, drafting) | `ClaimMapperAgent`, `DamagesModelingAgent`, etc. |
| **Models** | `src/models/` | 100+ Pydantic v2 models for entire litigation lifecycle | All model classes + enums |
| **Orchestration** | `src/orchestration/` | Agent lifecycle, pipelines, patterns, swarm coordination | `BaseAgent`, `Pipeline`, `AutonomousControlOrchestrator` |
| **Config** | `src/config/` | Pydantic BaseSettings singleton, all env vars | `get_settings()`, `Settings` |

### Litigation Domain Modules

| Module | Path | Purpose | Key Exports |
|--------|------|---------|-------------|
| **Litigation** | `src/litigation/` | Full litigation domain: 7 agents, models, orchestration | `LitigationForceAgent`, `CivilRICOAgent`, `LitigationOrchestrator` |
| **LitOS** | `src/litos/` | Litigation Operating System: case management, playbooks, export | `LitOS`, `EarlyCaseAssessment`, `DecisionTreeAnalysis`, `LitigationBudget`, `BoardApprovalPackage`, `TrialLifecycle` |
| **Enforcement** | `src/enforcement/` | Contract enforcement, damages calculation, argument generation | `ContractEnforcer`, `DamagesCalculator`, `CaseBuilder`, `ArgumentGenerator` |
| **Cases** | `src/cases/` | Case builders and loaders (including Mullins v. Connected Solar) | `CaseBuilder`, `CaseLoader` |
| **Documents** | `src/documents/` | Document classification, naming, date extraction | `DocumentClassifier`, `DocumentNamer`, `DateExtractor` |
| **Parsers** | `src/parsers/` | Document parsing and text extraction | `DocumentParser` |

### Intelligence & Analysis Modules

| Module | Path | Purpose | Key Exports |
|--------|------|---------|-------------|
| **Scrapers** | `src/scrapers/` | 6 platform scrapers (Twitter, LinkedIn, Facebook, Instagram, YouTube, Website) + Apify | `BaseScraper`, all platform scrapers |
| **Evaluations** | `src/evaluations/` | Social evaluation orchestration | `SocialEvaluator` |
| **Swarm** | `src/swarm/` | Multi-agent swarm: registry, message bus, 4 force agents | `LitigationSwarmOrchestrator`, `SwarmRegistry`, `SwarmMessageBus` |
| **Validation** | `src/validation/` | AI-powered data validation with Claude reasoning | `ValidationPipeline`, `ReasoningValidator`, `SyntheticDataGenerator` |

### Data & Knowledge Modules

| Module | Path | Purpose | Key Exports |
|--------|------|---------|-------------|
| **Graph** | `src/graph/` | Neo4j async client + 8 repository types | `Neo4jClient`, all repositories |
| **Ontology** | `src/ontology/` | Veritas LegalTech ontology (8 types) | `OntologyRegistry`, type definitions |
| **Ingestion** | `src/ingestion/` | **Palantir-style** enterprise data ingestion: ontology-driven, semantic understanding, schema governance, knowledge graph integration, 3D visualization, 5 pre-built workflows | `IngestionPipeline`, `SemanticLayer`, `KnowledgeGraphPipeline`, `WorkflowEngine`, `Graph3DExporter` |
| **Memory** | `src/memory/` | Persistent conversation memory with Neo4j | `ConversationOrchestrator`, `ConversationManager`, `MemoryAwareAgent` |
| **Services/GraphRAG** | `src/services/graphrag.py` | Graph-augmented retrieval: hybrid vector+graph search with citations | `GraphRAGService`, `RetrievalMode` (VECTOR_ONLY, GRAPH_ONLY, HYBRID) |
| **Services/Embeddings** | `src/services/embeddings.py` | Multi-provider vector embeddings (OpenAI, Anthropic, Cohere, SentenceTransformers) | `EmbeddingService`, `EmbeddingConfig` |

### AI/ML Modules

| Module | Path | Purpose | Key Exports |
|--------|------|---------|-------------|
| **ML** | `src/ml/` | Model registry, feature store, training pipelines, inference | `ModelRegistry`, `FeatureStore`, `TrainingPipeline`, `InferenceEngine` |
| **MLOps** | `src/mlops/` | Experiment tracking, deployment, A/B testing, drift detection | `ExperimentTracker`, `DeploymentManager`, `ModelMonitor`, `DriftDetector` |
| **Evals** | `src/evals/` | Benchmark runner and evaluation framework | `BenchmarkRunner`, `EvalRunner` |
| **Tools** | `src/tools/` | Tool metadata, schema generation (OpenAI/Claude), golden prompt testing | `ToolRegistry`, `generate_claude_schema`, `GoldenPromptSet` |

### Infrastructure Modules

| Module | Path | Purpose | Key Exports |
|--------|------|---------|-------------|
| **API** | `src/api/` | FastAPI REST API with routers (health, scraping, investigation, evaluation, github) | `create_app()` |
| **MCP** | `src/mcp/` | Multi-Connector Platform with policy enforcement, 8 connector stubs | `MCPServer`, all connectors |
| **Apify** | `src/apify/` | Apify MCP integration for web scraping actors | `ApifyClient`, `ApifyMCPServer` |
| **Runtime** | `src/runtime/` | **Portable agent kernel**: run ANY agent on ANY LLM (Claude, OpenAI, Ollama, vLLM) via ANY transport (REST, MCP, WebSocket, gRPC) | `AgentKernel`, `BaseLLMAdapter`, `ClaudeAdapter`, `OllamaAdapter` |
| **Storage** | `src/storage/` | S3-compatible storage (AWS, R2, B2) + Dropbox | `S3Client`, `S3Repository`, `DropboxClient` |
| **Integrations** | `src/integrations/` | CRM integrations: Attio, Airtable, Odoo | `AttioClient`, `AirtableClient`, `OdooClient` |

### UI & Export Modules

| Module | Path | Purpose | Key Exports |
|--------|------|---------|-------------|
| **Vault** | `src/vault/` | Obsidian-compatible export: markdown notes with wikilinks, frontmatter, formatters | `Vault`, `VaultExporter`, `InvestigationFormatter` |
| **Bases** | `src/bases/` | Plugin view system (Obsidian-style): BasesView, Component, Plugin architecture | `BasesView`, `BasesViewController`, `App`, `Plugin` |
| **CLI** | `src/cli.py` | argparse CLI: scrape, evaluate, graph commands | `main()` |
| **Utils** | `src/utils/` | structlog setup, text/URL helpers, search | `setup_logging()`, `helpers` |

### Module Count Summary

| Category | Modules | Files | Key Classes |
|----------|---------|-------|-------------|
| Core Platform | 6 | ~50 | BaseAgent, Pipeline, Settings |
| Litigation Domain | 6 | ~40 | LitOS, ContractEnforcer, DocumentParser |
| Intelligence | 4 | ~30 | SwarmOrchestrator, ValidationPipeline |
| Data & Knowledge | 6 | ~45 | GraphRAG, SemanticLayer, MemoryAwareAgent |
| AI/ML | 4 | ~20 | ModelRegistry, DriftDetector, ToolRegistry |
| Infrastructure | 6 | ~25 | AgentKernel, S3Client, ApifyClient |
| UI & Export | 4 | ~15 | Vault, BasesView, CLI |
| **TOTAL** | **36** | **~225** | |

---

## Article IX: Autonomous Control Protocol

### 9.1 Vision: AI-First OS

AI controls and orchestrates everything except the power button. The human provides direction, strategy, and the on/off switch. All other operations — code, tests, deployments, reviews, monitoring, documentation, cross-repo sync, knowledge capture — are autonomous.

### 9.2 Autonomous Control Loop

The `AutonomousControlOrchestrator` (`src/orchestration/autonomous_control.py`) executes:

| Step | Action | Agent | Output |
|------|--------|-------|--------|
| 1 | **INVENTORY** | `InventoryAgent` | Complete catalog of agents, models, scrapers, connectors, skills, configs |
| 2 | **HEALTH CHECK** | Built-in | Constitution present, tests passing, tool configs synced |
| 3 | **INGEST** | `IngestionAgent` | Data from CRM, email, docs, GitHub, Slack, Notion, Linear |
| 4 | **CONFIGURE** | `AutoConfigureAgent` | All AI tools configured from CONSTITUTION.md |
| 5 | **SYNC** | Cross-repo sync | Changes propagated to all downstream repos |
| 6 | **CAPTURE** | Session review | Knowledge persisted to constitution + runtime memory |

### 9.3 ConnectedAgents.AI Bridge

The `ConnectedAgentsBridge` connects LitigationForce.AI to the `connectedagents-ai` ecosystem:

```
LitigationForce.AI (agents learn)
    → session review (capture knowledge)
    → constitution update (memorialize patterns)
    → cross-repo sync (propagate to downstream)
    → downstream repos apply changes
    → bilateral feedback flows back
    → evals measure quality improvement
    → repeat (continuous learning loop)
```

### 9.4 Ingestion Sources

| Source | Connector | Data Types |
|--------|-----------|-----------|
| GitHub | MCP (github) | PRs, issues, commits, discussions |
| Slack | MCP (slack) | Messages, channels, threads |
| Notion | MCP (notion) | Pages, databases, comments |
| Linear | MCP (linear) | Issues, projects, cycles |
| CRM | Attio/Airtable/Odoo | Contacts, deals, activities |
| Email | Email API | Inbox, sent, flagged (legal relevance analysis) |
| Documents | Local FS + S3 + Dropbox | PDFs, contracts, filings, discovery |
| Calendar | Calendar API | Events, deadlines, court dates |

### 9.5 Auto-Configuration Targets

| Tool | Config File | Auto-Synced |
|------|------------|-------------|
| Claude Code | `CLAUDE.md` | Yes — via `/sync-constitution` |
| Cursor | `.cursorrules` | Yes |
| GitHub Copilot | `.github/copilot-instructions.md` | Yes |
| OpenAI Codex | `codex.md` | Yes |
| Windsurf | `.windsurfrules` | Yes |
| Claude AI | `CLAUDE.md` | Yes |
| Computer Control | `.claude/commands/auto-control.md` | Yes |

---

## Article X: Design System Governance

### 10.1 Binding Design Standards

All applications, websites, reports, social media, presentations, and documentation across the Connected Energy.AI ecosystem MUST follow the design system defined in `docs/DESIGN_SYSTEM.md`.

### 10.2 Design Philosophy

**Deloitte-grade institutional quality** meets **modern legal technology**. The aesthetic is the intersection of Big Four consulting rigor and cutting-edge AI/legal tech. Substantially similar to modern Deloitte graphics, charts, reports, and digital presence — combined with modern legal tech and institutional multinational litigation team aesthetics.

### 10.3 Brand Color Palette (Binding)

**Dark Mode (default for all digital):**
- Backgrounds: `#0A0E27` / `#0D1233` / `#131940` / `#1A2050`
- Accents: `#00D4FF` (cyan) / `#FF6B35` (orange) / `#8B5CF6` (purple) / `#10B981` (green)
- Text: `#FFFFFF` / `#B8BCC8` / `#6B7280`

**Light Mode (reports, print):**
- Backgrounds: `#FFFFFF` / `#F9FAFB` / `#F3F4F6`
- Accents: `#0891B2` / `#EA580C` / `#7C3AED` / `#059669`
- Text: `#111827` / `#374151` / `#6B7280`

### 10.4 Typography (Binding)

| Usage | Font | Fallback |
|-------|------|----------|
| Display/Headlines | Orbitron | system-ui, sans-serif |
| Body/UI | Inter | system-ui, sans-serif |
| Code/Data | JetBrains Mono | monospace |
| Legal/Formal | Source Serif Pro | Georgia, serif |

### 10.5 Consistency Rules

1. **No hardcoded colors** — All colors via CSS custom properties or design tokens
2. **No custom fonts** — Only the 4 approved font families
3. **Spacing scale only** — 4, 8, 12, 16, 24, 32, 48, 64, 96px
4. **Component library first** — No ad-hoc UI elements
5. **WCAG 2.1 AA** — Minimum accessibility standard
6. **60fps** — All animations must maintain 60fps
7. **Lighthouse 90+** — Performance and accessibility scores

### 10.6 Pattern Variation Framework

These elements are **FIXED** (never change):
- Color palette, typography scale, spacing scale, logo usage, accessibility requirements

These elements are **VARIABLE** (change within framework):
- Layout composition, hero treatment, chart types, animation choreography, content density

### 10.7 Application Standards

| Application | Stack | Reference |
|-------------|-------|-----------|
| Marketing website | Next.js + Framer + Three.js | `docs/DESIGN_SYSTEM.md` §8.1 |
| Web application | Next.js + React + Tailwind | `docs/DESIGN_SYSTEM.md` §8.2 |
| Reports (PDF) | React-PDF / WeasyPrint | `docs/DESIGN_SYSTEM.md` §8.3 |
| Social media | Figma templates | `docs/DESIGN_SYSTEM.md` §8.4 |
| Presentations | Figma/Keynote templates | `docs/DESIGN_SYSTEM.md` §8.5 |

### 10.8 Frontend Repository Structure

All frontend repos MUST follow this structure:
```
app/           — Next.js App Router pages
components/    — ui/ (primitives), charts/, layout/, marketing/, shared/
lib/tokens/    — Design token definitions (colors, typography, spacing, motion)
styles/        — globals.css (reset + tokens), tokens.css (custom properties)
public/        — fonts/, icons/, images/
```

---

## Article XI: Amendments

This constitution may only be amended by:
1. Explicit human approval from the repository owner
2. A commit message containing `constitution(amend): <description>`
3. Automatic propagation to all tool-specific config files

---

*Ratified: 2026-02-20 | Last Amended: 2026-02-21 | Owner: Robert Bailey | Enterprise: Connected Energy.AI*
