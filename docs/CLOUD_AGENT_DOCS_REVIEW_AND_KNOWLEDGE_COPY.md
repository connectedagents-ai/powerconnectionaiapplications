# Cloud Agent Docs Review and Knowledge Copy — End-to-End Instructions, Methods, Tools, Scripts

**Purpose:** End-to-end instructions, methods, tools, and scripts to **command a cloud agent** to run a **review**, **fully copy** entire **developer docs**, **LLM dev docs**, and **application docs**, then **save** to **relevant knowledge** and/or **extract relevant knowledge** for **agent knowledge** and/or **combined knowledge**.

**Governance:** [constitution.md](constitution.md) §6.6 (every-response suggestions); [AGENTS_ROLES_SWARMS_AND_CONTINUOUS_LEARNING.md](AGENTS_ROLES_SWARMS_AND_CONTINUOUS_LEARNING.md) §3 (knowledge gathering, domain corpus); [SOURCES_AND_EMULATION_INDEX.md](SOURCES_AND_EMULATION_INDEX.md) §11b (top LLMs and applications). **Sources config:** `config/docs-sources-for-knowledge-copy.yaml`.

---

## 1. End-to-end flow (summary)

1. **Command** — Trigger a cloud-agent **review** (Full Review or dedicated docs-review run).
2. **Scope** — Read `config/docs-sources-for-knowledge-copy.yaml` for **developer docs**, **LLM dev docs**, and **application docs** URLs/bases to copy.
3. **Copy / crawl** — Use **Firecrawl** (Scrape, Crawl, or Agent) or equivalent to **fully copy** the content of each source (or site section) to raw artifacts.
4. **Save to relevant knowledge** — Write full or chunked content to:
   - **General knowledge:** `docs/knowledge/` (one file or folder per source or topic).
   - **Agent-specific knowledge:** `docs/knowledge/agent/` (per-agent or per-domain extracts).
   - **Combined knowledge:** `docs/knowledge/combined/` (merged index or single curated doc for cross-agent use).
5. **Extract relevant knowledge** (optional) — From the copied content, **extract** sections or summaries that are relevant to:
   - **Agent knowledge** — Instructions, schemas, patterns, or examples for a specific agent (e.g. orchestrator, entity-extractor, drafting); write to `docs/knowledge/agent/<agent_or_domain>.md` or to the agent’s skill/playbook context.
   - **Combined knowledge** — Cross-cutting best practices, API contracts, or shared concepts; write to `docs/knowledge/combined/` or to a single `docs/knowledge/combined/COMBINED_KNOWLEDGE_INDEX.md` that links or embeds the extracts.
6. **Review and checklist** — Complete Full Review mandatory checklist (including commit review and final decision when touching master files); add at least one suggestion per constitution §6.6.

---

## 2. Methods

| Step | Method | Description |
|------|--------|-------------|
| **Command cloud agent review** | Run Full Review or a dedicated “docs review” pipeline so the agent has current repo state and checklist. | `./scripts/run-full-review.sh` and complete `docs/audits/full-review-summary.md` mandatory checklist; or run `./scripts/run-cloud-agent-docs-review-and-copy.sh` which can invoke review + copy flow. |
| **Load source list** | Read config so the copy step is data-driven. | Load `config/docs-sources-for-knowledge-copy.yaml`: sections `developer_docs`, `llm_dev_docs`, `applications_docs` (each: `name`, `url` or `base_url`, optional `crawl_depth`, `destination`). |
| **Full copy** | For each source: scrape or crawl entire doc site/section. | Use Firecrawl **Scrape** (single page) or **Crawl** (whole site) or **Agent** (gather from multiple pages); output Markdown or JSON; persist to `data/docs-copy/raw/<source_slug>/` with timestamp. |
| **Save to relevant knowledge** | Map copied content to knowledge paths. | **General:** `docs/knowledge/<topic_or_source>.md` (e.g. `docs/knowledge/ANTHROPIC_DEVELOPER_DOCS.md`). **Agent:** `docs/knowledge/agent/<agent_or_domain>.md`. **Combined:** `docs/knowledge/combined/<name>.md` or append to `COMBINED_KNOWLEDGE_INDEX.md`. Naming: slug from config `name`; one file per source or one folder per source with chunked files. |
| **Extract for agent / combined knowledge** | Optionally run extraction so only relevant parts feed agent or combined knowledge. | **Criteria:** Sections that match agent domain (e.g. “tool use” for orchestrator, “prompting” for drafting), or that are cross-cutting (e.g. “safety”, “rate limits”). **Tool:** LLM-based extract (e.g. “extract sections relevant to [agent/domain]”) or rule-based (headings, keywords). **Output:** Append or write to `docs/knowledge/agent/<agent>.md` and/or `docs/knowledge/combined/`. |
| **Provenance and review** | Record what was copied and when; run review. | Write `data/docs-copy/manifest.json` (sources, URLs, timestamps, paths). Run Full Review if master files or knowledge structure changed; complete commit review and final decision per [MASTER_FILE_COMMIT_REVIEW_AND_FINAL_DECISION_SYSTEM.md](MASTER_FILE_COMMIT_REVIEW_AND_FINAL_DECISION_SYSTEM.md). |

---

## 3. Tools

| Tool | Use | Notes |
|------|-----|------|
| **Firecrawl** | Scrape (single URL), Crawl (site), Agent (multi-page gather). | API: `https://api.firecrawl.dev`; env: `FIRECRAWL_API_KEY` (1Password DevOps). See [FIRECRAWL_API_AND_INTEGRATIONS.md](FIRECRAWL_API_AND_INTEGRATIONS.md). MCP: `firecrawl-mcp` in `.cursor/mcp.json`. CLI: `npx -y firecrawl-cli`. |
| **run-cloud-agent-docs-review-and-copy.sh** | Single entry to run review + load config + trigger copy flow. | Reads `config/docs-sources-for-knowledge-copy.yaml`; invokes Full Review (or skip with `--copy-only`); delegates actual scrape/crawl to Firecrawl (script prints instructions or calls Firecrawl CLI/API if available). |
| **config/docs-sources-for-knowledge-copy.yaml** | Authoritative list of developer docs, LLM dev docs, application docs to copy. | Sections: `developer_docs`, `llm_dev_docs`, `applications_docs`. Each entry: `name`, `url` or `base_url`, optional `crawl_depth`, `destination` (e.g. `knowledge`, `knowledge/agent/orchestrator`). |
| **Cursor / Claude Code / Codex** | Run the script; use Firecrawl MCP to scrape/crawl when the script delegates to the agent. | From any dev tool: open master repo, run `./scripts/run-cloud-agent-docs-review-and-copy.sh`; if script outputs “use Firecrawl MCP to scrape …”, agent performs the scrape and writes to the paths specified in config. |

---

## 4. Scripts

| Script | Purpose |
|--------|---------|
| **scripts/run-cloud-agent-docs-review-and-copy.sh** | (1) Optionally run Full Review. (2) Load `config/docs-sources-for-knowledge-copy.yaml`. (3) For each source: output copy instruction (URL, destination path) or call Firecrawl CLI/API. (4) Write manifest to `data/docs-copy/manifest.json`. (5) Remind to run extraction (optional) and to save to `docs/knowledge/`, `docs/knowledge/agent/`, `docs/knowledge/combined/`. |
| **scripts/run-full-review.sh** | Standard Full Review; complete before or after the copy run when master files or knowledge are touched. |
| **scripts/run-scrape-with-screenshot.sh** | Matter-scoped scrape with screenshot; use for evidence/party scrape, not for bulk docs copy. Reference only. |

**Extraction script (optional):** A separate script or agent step can read `data/docs-copy/raw/<source_slug>/` and extract relevant sections into `docs/knowledge/agent/<agent>.md` and `docs/knowledge/combined/`. Document in this file when added.

---

## 5. Destinations (where to save)

| Destination | Purpose | Format |
|-------------|---------|--------|
| **docs/knowledge/** | General, topic-level or source-level knowledge (e.g. one doc per LLM vendor). | Markdown; one file per source or topic (e.g. `ANTHROPIC_DEVELOPER_DOCS.md`, `OPENAI_PLATFORM_DOCS.md`). |
| **docs/knowledge/agent/** | Per-agent or per-domain extracted knowledge for agent context. | Markdown; one file per agent or domain (e.g. `orchestrator.md`, `drafting.md`); referenced from playbooks or skills. |
| **docs/knowledge/combined/** | Cross-agent combined knowledge index or merged doc. | Markdown; `COMBINED_KNOWLEDGE_INDEX.md` (links or embeds key extracts); optional per-topic files. |
| **data/docs-copy/raw/<source_slug>/** | Raw copied content before extraction (optional). | Markdown or JSON per page/section; timestamped; referenced by manifest. |

---

## 6. Extraction criteria (for agent knowledge and combined knowledge)

When **extracting** from the full copy into agent or combined knowledge:

- **Agent knowledge:** Include sections that (1) describe APIs, schemas, or patterns the agent uses; (2) give instructions or examples for the agent’s domain (e.g. tool use for orchestrator, prompting for drafting); (3) are cited in [AGENT_FUNCTION_SOURCES_WHITEPAPERS_CONSTITUTIONS_REPOS.md](AGENT_FUNCTION_SOURCES_WHITEPAPERS_CONSTITUTIONS_REPOS.md) for that agent.
- **Combined knowledge:** Include (1) cross-cutting best practices (safety, rate limits, auth); (2) shared concepts (MCP, 12-Factor, TRiSM); (3) glossary or definitions used by more than one agent.
- **Provenance:** Each extracted file should note **source** (URL, doc name) and **date copied** so review and refresh are traceable.

---

## 7. Triggers and cadence

| Trigger | Action |
|---------|--------|
| **Quarterly** | Run full flow: review → copy all sources in config → save to knowledge → extract for agent and combined. |
| **New source added to config** | Copy the new source only; save to relevant knowledge; optionally re-run extraction for affected agents. |
| **On demand** | Run `./scripts/run-cloud-agent-docs-review-and-copy.sh` (or `--copy-only` to skip Full Review). |

---

## 8. References

| Doc | Purpose |
|-----|---------|
| [config/docs-sources-for-knowledge-copy.yaml](../config/docs-sources-for-knowledge-copy.yaml) | Source list: developer docs, LLM dev docs, application docs. |
| [FIRECRAWL_API_AND_INTEGRATIONS.md](FIRECRAWL_API_AND_INTEGRATIONS.md) | Firecrawl API, MCP, CLI. |
| [SOURCES_AND_EMULATION_INDEX.md](SOURCES_AND_EMULATION_INDEX.md) §11b | Top LLMs and applications — URLs and dev docs. |
| [AGENT_FUNCTION_SOURCES_WHITEPAPERS_CONSTITUTIONS_REPOS.md](AGENT_FUNCTION_SOURCES_WHITEPAPERS_CONSTITUTIONS_REPOS.md) | Per-agent sources; use for extraction targeting. |
| [AGENTS_ROLES_SWARMS_AND_CONTINUOUS_LEARNING.md](AGENTS_ROLES_SWARMS_AND_CONTINUOUS_LEARNING.md) §3 | Knowledge gathering, domain corpus, cloud agents. |
| [MASTER_FILE_COMMIT_REVIEW_AND_FINAL_DECISION_SYSTEM.md](MASTER_FILE_COMMIT_REVIEW_AND_FINAL_DECISION_SYSTEM.md) | When knowledge or master files change, run commit review and Claude Code final decisions. |

---

## 9. Voice agent platforms (no-miss extraction)

**Voice-specific** extraction for **ElevenLabs, Vapi, Retell, Bland, Deepgram** (and related white papers/repos) is governed by:

- **Config:** `config/docs-sources-for-knowledge-copy.yaml` section **voice_agent_docs** (base_urls and slugs).
- **VoiceAgent.AI repo:** [docs/VOICE_AGENT_NO_MISS_WORKFLOWS_AND_ARCHITECTURE.md](https://github.com/.../voiceagent.ai/blob/main/docs/VOICE_AGENT_NO_MISS_WORKFLOWS_AND_ARCHITECTURE.md) — no-miss workflow, architecture (Node.js, Replit, database, voice APIs, UI/UX), and **report-back runbook** for Cursor, Codex, and Claude Code.

**Extract:** features, benefits, rules, knowledge bases, sequences, harnesses, UI/UX components; map to Node.js, Replit, DB, and all dev connections to voice APIs. **Report back:** run the report-back runbook (§5 in that doc) and write `docs/audits/voice-agent-docs-extraction-report-YYYY-MM-DD.md` in voiceagent.ai (or in this repo if running from master). When running the general cloud-agent docs review, include **voice_agent_docs** sources so voice platform docs are copied and saved to `docs/knowledge/` alongside other sources.

_Maintain at: docs/CLOUD_AGENT_DOCS_REVIEW_AND_KNOWLEDGE_COPY.md. Update when adding sources, destinations, or scripts._
