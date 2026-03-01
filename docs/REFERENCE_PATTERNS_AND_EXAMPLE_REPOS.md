# Reference Patterns & Example Repos — What New Repos Should Emulate

> **Purpose**: Canonical inventory of modules, patterns, and repos that new platform repos are meant to copy or emulate. Ensures constitution, LexVault, and other standards propagate.

**Referenced by**: constitution §6, NEW_CAPABILITY_CHECKLIST, sync-all-repos-and-review.sh, CROSS_PLATFORM_UPDATE_CHECKLIST

---

## 1. Module Specs (docs/modules/) — Design Patterns to Emulate

These are **reference specifications** synced to all child repos. New repos handling file systems, evidence, UI, or ontology should follow them.

| Module                                          | File                                                        | Emulate When                                                                               |
| ----------------------------------------------- | ----------------------------------------------------------- | ------------------------------------------------------------------------------------------ |
| **LexVault**                                    | `docs/modules/lexvault.md`                                  | Case file storage, evidence ontology, Box/metadata integration, naming conventions         |
| **Ontology**                                    | `docs/modules/ontology.md`                                  | Entity types, naming conventions, RICO directory structure, cross-platform schema          |
| **Voice Agents**                                | `docs/modules/voice-agents.md`                              | Legal Scribe, transcription, voice-driven research                                         |
| **Litigation Swarm UI**                         | `docs/modules/litigation-swarm-ui.md`                       | Web app design, component library, page architecture                                       |
| **OneWish architecture (website/UI/marketing)** | `docs/modules/onewish-architecture-website-ui-marketing.md` | Rules, skills, knowledge, submodules; Foundry sync; repos/starred search and enhance (§10) |
| **Module Architecture**                         | `docs/MODULE_ARCHITECTURE_AND_PLATFORM_STACK.md`            | Vercel/v0 module selection, design tokens, platform integration                            |

**Source**: Notion wikis, Google Drive PRDs, Box. Synced via `scripts/sync-all-repos-and-review.sh`. **Module selection**: `config/module-selection.yaml`.

---

## 2. Example Repos — Templates & Patterns

| Repo                              | Role                                    | Sync Status                 | Emulate For                               |
| --------------------------------- | --------------------------------------- | --------------------------- | ----------------------------------------- |
| **slack-agent-template**          | Nitro Slack agents                      | ✅ In ALL_REPOS (bootstrap) | New Slack bots, agent templates           |
| **connected-agents-platform**     | Platform core, constitution, ontology   | ✅ ROUTES                   | New platform agents, shared ontology      |
| **LitigationForce.AI**            | Full ADK, scrapers, MCP, case workflows | ✅ ROUTES                   | Litigation agents, Pydantic models, Neo4j |
| **file-management-toolkit**       | Desktop/file org, cloud dedup           | ✅ ROUTES                   | File operations, AI clerk patterns        |
| **powerconnectionaiapplications** | Power Connection AI apps                | ✅ ROUTES                   | Vertical-specific apps                    |
| **nextjs-ai-chatbot**             | Base template (Lovable, Vercel)         | GitHub-only                 | AI chat UIs, Next.js + Vercel             |
| **adk-python**                    | Google ADK agent framework              | GitHub-only                 | Agent implementation patterns             |
| **demo-repository**               | GitHub demo template                    | GitHub-only                 | Quick-start demos                         |

---

## 3. LexVault-Specific Integration

LexVault (`docs/modules/lexvault.md`) defines:

- **File ontology** — Metadata taxonomy, naming conventions, SHA-256 provenance
- **OpenAI Responses API** — Matter-scoped retrieval, structured extraction
- **Access control** — RBAC (Attorney > Paralegal > Admin > Client > Agent)
- **Box integration** — 1.8TB+ enterprise storage patterns

**Used by**: `scripts/cloud_file_ops.py` (generate_lexvault_name), evidence-processor, evidence-ingest, evidence-search skills.

---

## 4. Sync Coverage

| Item                                              | Synced To Child Repos       | When                                              |
| ------------------------------------------------- | --------------------------- | ------------------------------------------------- |
| constitution.md                                   | ✅ (via route-constitution) | Every sync                                        |
| NEW_CAPABILITY_CHECKLIST, UNIVERSAL_INSTRUCTIONS  | ✅ (via route-constitution) | Every sync                                        |
| docs/modules/\*.md (LexVault, ontology, etc.)     | ✅ (via sync script)        | Every sync                                        |
| SUPER_DEVELOPER_PRINCIPLES, ALL_REPO_REVIEW, etc. | ✅                          | Every sync                                        |
| my-agent.agent.md, master-orchestrator.md         | ✅                          | Every sync                                        |
| nextjs-ai-chatbot, adk-python                     | —                           | Clone from GitHub when creating new chatbot/agent |

---

## 5. New Repo Checklist (from Constitution §6 + This Doc)

When creating a new repo that handles:

- **Case files / evidence** → Read `docs/modules/lexvault.md` first
- **Entity schemas / naming** → Read `docs/modules/ontology.md`
- **Web app / UI** → Read `docs/MODULE_ARCHITECTURE_AND_PLATFORM_STACK.md`, use `config/module-selection.yaml`
- **Website / UI / Marketing (multi-site, design system, content map)** → Read `docs/modules/onewish-architecture-website-ui-marketing.md`, `docs/UI_UX_AND_MARKETING_TURNKEY_GUIDE_SOURCES_AND_ORGANIZATION.md`; search all repos and starred/reference per STARRED_AND_REFERENCE_REPOS
- **v0 / Vercel components** → Read `docs/V0_SETUP_AND_INSTRUCTIONS.md`, follow module selection methodology
- **Slack agents** → Clone `slack-agent-template`, run bootstrap
- **AI chat UI** → Clone `nextjs-ai-chatbot`, add constitution
- **Agent framework** → Reference `adk-python` patterns
- **Voice agents** → Read `docs/modules/voice-agents.md`
- **Website / webapp / components / design ingestion** → Use **website-webapp-component** repo (sibling to VoiceAgent.AI): design ingestion from URLs/repos/chat → design-concepts filing → trigger UI/UX build in parallel to voice; resource catalog (repos, docs, white papers, podcasts, Next/v0/Replit/HF/Lovable/Figma); modular flows (quick create, demo, component, integrated, production); phone apps and UI/UX deep-dive. See that repo’s `docs/DESIGN_INGESTION_AND_FILING_SYSTEM.md`, `docs/RESOURCE_CATALOG_AND_INTEGRATIONS.md`, `docs/MODULAR_FLOWS_QUICK_CREATE_DEMO_PRODUCTION.md`, `docs/PHONE_APPS_AND_UI_UX_DEEP_DIVE.md`.

---

_Maintain at: docs/REFERENCE_PATTERNS_AND_EXAMPLE_REPOS.md. Update when adding modules or example repos._
