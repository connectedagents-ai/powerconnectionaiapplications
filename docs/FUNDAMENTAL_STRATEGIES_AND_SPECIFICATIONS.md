# Fundamental Strategies and Specifications — Agents, Modular Development, Design, MCP

> **Purpose**: Single reference for agent types, modular development strategies, rules, color schemes, design rules, and master MCP connectivity. Expanded and clarified for platform consistency.
>
> **Referenced by**: constitution, AGENTS.md, MASTER_INDEX, litigation-swarm-ui, mcp-router, AGENT_ARCHITECTURE_MASTER

---

## Part 1: Agent Types — Taxonomy and Roles

### 1.1 By Execution Mode

| Type               | Definition                                            | Temperature | Use Case                              | Examples                                                                                                              |
| ------------------ | ----------------------------------------------------- | ----------- | ------------------------------------- | --------------------------------------------------------------------------------------------------------------------- |
| **Deterministic**  | Fixed rules, repeatable outputs, zero variance        | 0.0         | Data integrity, consistency mandatory | Fact Checker, Citation Validator, Privilege Scanner, OCR, Metadata Normalizer, Dedup, Audit Trail, Compliance Monitor |
| **Expert Dynamic** | Judgment, reasoning, domain expertise                 | 0.1–0.3     | Legal analysis, strategy, drafting    | RICO Analyzer, Contract Analyst, Defense Assessor, Damages Modeler, Pattern Detector, Logic Auditor, Ethics Reviewer  |
| **Voice**          | Spoken interfaces, real-time                          | —           | Dictation, transcription, hands-free  | Legal Scribe, Deposition Transcriber, Case Research Voice Assistant                                                   |
| **Orchestrator**   | Coordinates subordinates; routes, escalates, approves | 0.1         | Multi-agent coordination              | Master Orchestrator, Chairman                                                                                         |

### 1.2 By Role (Multi-Agent Specialization)

| Role                          | Responsibility                                                             | Human Checkpoint | Gate              |
| ----------------------------- | -------------------------------------------------------------------------- | ---------------- | ----------------- |
| **Orchestrator**              | Plans, routes, enforces checkpoints; blocks high-stakes without approvals  | —                | Delegation        |
| **Privilege Agent**           | Flags privilege, work product, confidentiality risks; prepares review logs | Attorney         | Evaluator Swarm   |
| **Contract/Deal Agent**       | Parses agreements, obligations, amendments; extracts structured terms      | —                | Evaluator Swarm   |
| **Compliance Agent**          | Regulatory/retention; GDPR/CCPA; ISO control mapping                       | —                | Evaluator Swarm   |
| **Classification Agent**      | Doc type, custodianship, dedup, thread reconstruction                      | —                | Schema validation |
| **Evidence/Provenance Agent** | Evidence normalization, hashing, chain-of-custody                          | —                | Schema validation |
| **Evaluator Swarm**           | Fact, Citation, Logic, Ethics — ALL must pass                              | Attorney         | Blocking gate     |

### 1.3 By Work Phase

| Phase                   | Agents                                                         | Purpose                 |
| ----------------------- | -------------------------------------------------------------- | ----------------------- |
| **Phase 1: Foundation** | Intake, OCR, Metadata, Dedup, Classify                         | Evidence ingestion      |
| **Phase 2: Analysis**   | Entity Extract, Claim Mapper, RICO, Contract, Pattern Detector | Analysis and extraction |
| **Phase 3: Quality**    | Evaluator Swarm (4 gates)                                      | All must pass           |
| **Phase 4: Human**      | Attorney review, privilege determination                       | Mandatory checkpoint    |
| **Phase 5: Output**     | Excel, JSON, Dashboards, Bundles                               | Deliverables            |

### 1.4 Execution Patterns

| Pattern                 | When                                     | Diagram                                    |
| ----------------------- | ---------------------------------------- | ------------------------------------------ |
| **Individual**          | Single agent, focused task               | Input → Agent → Output                     |
| **Sequential Pipeline** | Each stage feeds next                    | Intake → Entity → Claim → Gate → Human     |
| **Parallel**            | Independent tasks simultaneously         | Input → [A,B,C] → Aggregator               |
| **Agent Swarm**         | Multi-expert review; synthesizer         | Output → [Fact,Cit,Logic,Ethics] → Verdict |
| **Chairman**            | Orchestrator coordinates; final decision | Chairman ← [A,B,C] → Decision              |

---

## Part 2: Modular Development Strategies

### 2.1 Single-Responsibility

- One agent = one tool/responsibility
- Reduces complexity; improves reliability
- Aligns with 12-Factor Agents "Small, Focused Agents"

### 2.2 Skill-Based Architecture

- `.cursor/skills/{name}/SKILL.md` — YAML frontmatter, Instructions, Examples
- Use when: new capability, new workflow, domain-specific logic
- Create skill per `create-skill/SKILL.md`; reference in NEW_CAPABILITY_CHECKLIST

### 2.3 Schema-First

- Define contracts in `docs/schemas/` before implementation
- Evidence, Claim, Timeline, Bundle, Pattern-Score
- Validate with `validate_schemas.sh`

### 2.4 Externalized Prompts

- Prompts in `config/playbooks.yaml`, not hardcoded
- Per-agent templates in `docs/playbooks/`
- Version prompts; run evals before deploy

### 2.5 Router-First MCP

- Progressive discovery: model sees small router tool set
- `discover_server_actions` → `get_action_details` → `execute_action`
- Reduces context overload; scales tool catalogs

### 2.6 Deterministic + LLM Hybrid

- Most products: deterministic code with LLM steps at key points
- Not pure "prompt + tools + loop"
- Per 12-Factor Agents: modular concepts incorporated into existing product

---

## Part 3: Rules Hierarchy

| Layer                    | File                                       | Scope                      | Precedence |
| ------------------------ | ------------------------------------------ | -------------------------- | ---------- |
| **Constitution**         | docs/constitution.md                       | Non-negotiable principles  | Highest    |
| **Master rules**         | .cursor/rules/master-project-rules.mdc     | Always-apply Cursor        | 1          |
| **Security/privilege**   | .cursor/rules/security-evidence.mdc        | Cases, evidence, privilege | 2          |
| **Compliance**           | .cursor/rules/litigation-compliance.mdc    | Legal standards            | 3          |
| **Agent efficiency**     | .cursor/rules/agent-efficiency-context.mdc | Execute, persist, scope    | 4          |
| **Constant improvement** | .cursor/rules/constant-improvement.mdc     | One-line capture           | 5          |
| **Expert prompting**     | .cursor/rules/expert-prompting.mdc         | Prompts, playbooks         | Glob       |
| **Platform bootstrap**   | .cursor/rules/platform-bootstrap.mdc       | New repos                  | Sync       |

---

## Part 4: Color Schemes and Design Tokens

### 4.1 Litigation Swarm Visual Identity

| Token                  | Hex       | Use                            |
| ---------------------- | --------- | ------------------------------ |
| **Primary background** | `#0A0E27` | Dark navy; app background      |
| **Accent cyan**        | `#00E5FF` | Lean take; secondary accent    |
| **Accent green**       | `#39FF14` | Strong take; positive; success |
| **Accent amber**       | `#F59E0B` | Borderline; caution; deadlines |
| **Accent red**         | `#EF4444` | Decline; alert; urgent         |
| **Accent purple**      | `#8B5CF6` | Decision metric; special       |
| **Neutral**            | `#94A3C8` | Muted; secondary text          |

### 4.2 Track Color Coding (Litigation)

| Track               | Color  | Hex       |
| ------------------- | ------ | --------- |
| **CA (California)** | Blue   | `#3B82F6` |
| **TX (Texas)**      | Orange | `#F59E0B` |
| **Federal RICO**    | Red    | `#EF4444` |

### 4.3 Verdict Signal Colors

| Signal                | Color                | Icon  |
| --------------------- | -------------------- | ----- |
| STRONG_TAKE, TAKE     | `#39FF14`            | ▲▲, ▲ |
| LEAN_TAKE             | `#00E5FF`            | △     |
| BORDERLINE            | `#F59E0B`            | ◆     |
| LEAN_DECLINE, DECLINE | `#F59E0B`, `#EF4444` | ▽, ▼  |
| STRONG_DECLINE        | `#EF4444`            | ▼▼    |

### 4.4 Deadline Urgency

| Days Remaining | Color     | Icon |
| -------------- | --------- | ---- |
| &lt; 0         | `#EF4444` | 🚨   |
| ≤ 60           | `#EF4444` | ⚠️   |
| ≤ 180          | `#F59E0B` | ⏳   |
| &gt; 180       | `#39FF14` | ✅   |

### 4.5 CSS Variables (Recommended)

```css
:root {
  --lf-bg-primary: #0a0e27;
  --lf-accent-cyan: #00e5ff;
  --lf-accent-green: #39ff14;
  --lf-accent-amber: #f59e0b;
  --lf-accent-red: #ef4444;
  --lf-track-ca: #3b82f6;
  --lf-track-tx: #f59e0b;
  --lf-track-rico: #ef4444;
  --lf-neutral: #94a3c8;
}
```

---

## Part 5: Design Rules

### 5.1 Principles (litigation-swarm-ui)

| Rule                           | Specification                                   |
| ------------------------------ | ----------------------------------------------- |
| **Dark-mode first**            | Reduce eye strain for long review               |
| **Data-dense layouts**         | Attorneys need information density              |
| **Color-coded tracks**         | Blue (CA), Orange (TX), Red (RICO) consistently |
| **Interactive visualizations** | Timelines, knowledge graphs, damages charts     |
| **Mobile-responsive**          | Key features on phone for court access          |
| **Accessibility**              | WCAG 2.1 AA minimum                             |

### 5.2 Component Conventions

- Split-panel document viewer: original | extracted text + annotations
- Properties panel: Type, RICO, Custodian, Privilege, Confidence
- Action buttons: Approve, Flag Privilege, Escalate, Annotate
- Verdict indicator: giant, colored, top of screen

### 5.3 Typography

- Modern monospace + clean sans-serif
- Source: litigation-swarm-ui; Tailwind + shadcn/ui

---

## Part 6: Master MCP Server and Automated Connectivity

### 6.1 Architecture

| Layer                  | Purpose                                                            |
| ---------------------- | ------------------------------------------------------------------ |
| **Master MCP Router**  | Single entry; progressive discovery; privilege guard               |
| **Private LLM**        | Ollama/local for privilege-flagged content; NEVER external         |
| **External LLM**       | Anthropic, OpenAI, Google, Blackbox for non-privileged             |
| **Vendor connections** | Microsoft, AWS, Zoom, Box, Legal (Relativity, Everlaw, Clio, etc.) |
| **Router tools**       | `discover_server_actions`, `get_action_details`, `execute_action`  |

### 6.2 Automated Connectivity Strategy

| Integration            | Config                       | Auto-Connect                     | Notes                                  |
| ---------------------- | ---------------------------- | -------------------------------- | -------------------------------------- |
| **1Password**          | op:// refs in .env.mcp       | Via agent-1password-index-env.sh | Credentials never in code              |
| **Connectors**         | config/connectors.yaml       | Env vars; platform-connections   | Per-vendor capabilities                |
| **MCP servers**        | config/mcp-servers/          | Cursor MCP config; stdio/HTTP    | Supabase, Notion, Linear, GitHub, etc. |
| **GitHub**             | GITHUB_PERSONAL_ACCESS_TOKEN | Repos, PRs, webhooks             | Constitution sync                      |
| **Linear**             | LINEAR_API_KEY               | Projects, issues                 | Buildout automation                    |
| **Notion**             | NOTION_API_KEY               | Wiki, case notes                 | sync-notion-to-repo                    |
| **Neo4j**              | NEO4J_URI, credentials       | Knowledge graph                  | Entity relationships                   |
| **Box/Drive**          | BOX*\*, GOOGLE*\*            | LexVault storage                 | 1.8TB+ patterns                        |
| **Relativity/Everlaw** | Per vendor                   | e-discovery                      | Document review                        |

### 6.3 Integration Categories

| Category    | Apps/APIs                                                    |
| ----------- | ------------------------------------------------------------ |
| **LLM**     | Anthropic, OpenAI, Google, Blackbox, xAI                     |
| **Search**  | Brave, DuckDuckGo                                            |
| **CRM**     | Attio, HubSpot, Airtable                                     |
| **Comms**   | Slack, Zoom                                                  |
| **Storage** | Supabase, Box, AWS S3                                        |
| **Legal**   | Relativity, Everlaw, Clio, Spellbook, Briefpoint, LexisNexis |
| **Design**  | Figma                                                        |
| **Dev**     | GitHub, Linear, Docker, Hugging Face                         |

### 6.4 Master MCP Config (config/mcp-servers/master-mcp.yaml)

- **discovery**: progressive
- **audit_logging**: true
- **privilege_guard**: true
- **private_llm**: Ollama for privilege_scan, privilege_determination, attorney_client_analysis
- **external_llm**: Routing per task type (rico→anthropic, damages→openai, etc.)
- **vendors**: Microsoft, AWS, Zoom, Box, Replit, Lovable, etc.

See: `docs/MASTER_MCP_CONNECTORS_APIS.md`, `config/connectors.yaml`, `config/mcp-servers/`, `docs/mcp-router.md`.

---

## Part 7: Quick Reference

```
AGENT TYPES: Deterministic (0.0) | Expert Dynamic (0.1-0.3) | Voice | Orchestrator
ROLES: Orchestrator, Privilege, Contract, Compliance, Classification, Evidence, Evaluator Swarm
MODULAR: Single-responsibility; skill-based; schema-first; externalized prompts; router-first MCP
COLORS: #0A0E27 bg | #39FF14 green | #00E5FF cyan | #F59E0B amber | #EF4444 red
TRACKS: CA=blue, TX=orange, RICO=red
DESIGN: Dark-mode; data-dense; WCAG 2.1 AA
MCP: Master router; progressive discovery; private LLM for privilege; connectors.yaml
```

---

_Maintain at: docs/FUNDAMENTAL_STRATEGIES_AND_SPECIFICATIONS.md. Update when agent types, design tokens, or MCP config changes._
