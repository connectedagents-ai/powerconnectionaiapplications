# LexVault — Secure Case File System & Knowledge Layer

> Source: Notion wiki "Lex Vault — OpenAI Responses API Integration", "DEVELOPER DOCS-LEXVAULT-AGENTS", "LEXVAULT-File System Ontology", Google Drive "lex-vault-litigation-swarm-prd.md"

## Overview

LexVault is the **system of record** for all litigation evidence, case files, and AI-generated artifacts. It provides:

- Canonical storage for raw source documents (PDFs, emails, photos)
- Extracted derivatives (OCR text, metadata, embeddings) — separately versioned and hashed
- Matter-scoped retrieval via OpenAI Responses API and vector search
- Structured extraction outputs as versioned, attributable, access-controlled artifacts
- Integration with Box (1.8TB+ enterprise storage) and Notion (case wikis)

## Architecture

```
┌─────────────────────────────────────────────────────────┐
│  LexVault                                               │
│                                                         │
│  ┌───────────┐  ┌──────────────┐  ┌─────────────────┐ │
│  │ Raw Store │  │ Derivatives  │  │ Vector Index    │ │
│  │ (immutable│  │ (OCR, meta,  │  │ (embeddings,    │ │
│  │  SHA-256) │  │  summaries)  │  │  semantic search)│ │
│  └─────┬─────┘  └──────┬───────┘  └────────┬────────┘ │
│        │               │                    │          │
│        └───────┬───────┘                    │          │
│                ▼                            │          │
│  ┌──────────────────┐    ┌─────────────────┘          │
│  │ Provenance Layer │    │                             │
│  │ (audit, chain-of-│    │                             │
│  │  custody, hashes) │◄──┘                             │
│  └──────────────────┘                                  │
│                                                         │
│  ┌──────────────────────────────────────────────────┐  │
│  │ Access Control (RBAC)                             │  │
│  │ Attorney > Paralegal > Admin > Client > Agent     │  │
│  └──────────────────────────────────────────────────┘  │
└─────────────────────────────────────────────────────────┘
```

## Core Responsibilities

### 1. Canonical Storage

- Raw source documents are immutable — SHA-256 locked at ingestion
- Derivatives (OCR text, extracted metadata, embeddings) are separately hashed
- Every artifact is versioned with full provenance chain
- Matter-scoped: all files belong to a specific case/matter

### 2. OpenAI Responses API Integration

- Matter-scoped retrieval using file_search tool
- Structured extraction via structured_output response format
- Agent-callable tools for case research workflows
- Output artifacts stored back into LexVault with attribution

### 3. Vector Search (Hybrid)

- Pre-computed embeddings for all text content
- Hybrid search: BM25 (keyword) + vector (semantic)
- Sharded by case for performance at 100K+ documents
- Supports similarity search, clustering, and document deduplication

### 4. Access Control

- RBAC: Attorney, Paralegal, Admin, Client, Agent (AI)
- Matter-level permissions (isolation between cases)
- Privilege-tagged documents restricted to privilege reviewer role
- All access logged in audit trail

## File System Ontology

> Source: Notion wiki "LEXVAULT-File System Ontology: Metadata Taxonomy & Syntax"

### Classification Schema

Compatible with:

- Palantir Foundry Object/Link Types
- Neo4j Property Graph Model
- Microsoft Graph API
- Box Content Graph
- Vector embeddings for semantic search

### Metadata Template

| Field              | Type   | Required | Description                                                                            |
| ------------------ | ------ | -------- | -------------------------------------------------------------------------------------- |
| `document_type`    | enum   | Yes      | contract, email, financial, corporate, filing, communication, deposition, photo, other |
| `matter_id`        | string | Yes      | Case identifier                                                                        |
| `custodian`        | string | Yes      | Source person/entity                                                                   |
| `date_created`     | date   | Yes      | Document creation date                                                                 |
| `date_collected`   | date   | Yes      | When collected into LexVault                                                           |
| `confidentiality`  | enum   | Yes      | public, internal, confidential, restricted                                             |
| `privilege_status` | enum   | Yes      | unknown, potentially_privileged, privileged, not_privileged                            |
| `rico_relevance`   | enum   | No       | critical, high, medium, low, not_relevant                                              |
| `sha256`           | string | Yes      | Hash of original file                                                                  |
| `tags`             | array  | No       | Free-form tags                                                                         |

### Naming Conventions

```
{MATTER}_{DOCTYPE}_{DATE}_{CUSTODIAN}_{SEQ}.{ext}

Examples:
  tesla_contract_20220916_rbailey_001.pdf
  tesla_email_20230115_ablair_042.eml
  tesla_financial_2023Q3_voltstreet_001.xlsx
```

### Folder Structure (LexVault Standard)

```
/MATTERS/
  /{MatterID}/
    /raw/                    # Immutable source files
    /derivatives/
      /ocr/                  # OCR text extracts
      /metadata/             # Extracted metadata JSON
      /embeddings/           # Vector embeddings
      /summaries/            # AI-generated summaries
    /productions/            # Production sets (Bates-stamped)
    /filings/                # Draft and final filings
    /work_product/           # Attorney work product (restricted)
    /privilege_log/          # Privilege determinations
    /audit/                  # Audit trail exports
```

## Integration with Master Repo

| LexVault Component     | Maps to Repo Artifact                      |
| ---------------------- | ------------------------------------------ |
| Evidence storage model | `docs/schemas/evidence-object.schema.json` |
| Metadata taxonomy      | This document + `docs/schemas/`            |
| Access control         | `.cursor/rules/security-evidence.mdc`      |
| Audit trail            | `docs/schemas/audit-event.schema.json`     |
| Provenance chain       | `docs/security.md`                         |
| Search/retrieval       | `config/mcp-servers/` (MCP router)         |

## Connectors & MCP — Photos, Files, Records, Timelines

LexVault ingests **photos**, **files**, and **records** from the following sources. Each can be wired via **connectors** (config/connectors.yaml) and/or **MCP** (agent-mcp-function-matrix.yaml). Outputs (evidence objects, timeline events) can be written back to Notion, Airtable, and timeline schemas.

| Source               | Type                           | Connector / MCP                                                                     | Use for                                                                                     |
| -------------------- | ------------------------------ | ----------------------------------------------------------------------------------- | ------------------------------------------------------------------------------------------- |
| **Box.com**          | Files, photos, records         | `box` connector (BOX_CLIENT_ID/SECRET); LexVault primary storage                    | Enterprise evidence, 1.8TB+; sync/copy into LexVault raw/derivatives                        |
| **iCloud.com**       | Files, photos                  | File paths (iCloud Drive); `search_roots` in workflow configs                       | ~/Library/Mobile Documents/com~apple~CloudDocs; photos via export or path                   |
| **OneDrive**         | Files, photos                  | `microsoft_365` / MS Graph; or local path if synced                                 | ~/OneDrive; Graph API for list/download when not mounted                                    |
| **SharePoint sites** | Files, lists, records          | Microsoft Graph API (same as OneDrive; SharePoint drive endpoints)                  | Site libraries, list data; matter wikis                                                     |
| **Desktop / Mac**    | Files, photos, local records   | Local paths; `file_search.search_roots` (HOME, ~/Documents, ~/Downloads, ~/Desktop) | PST, EML, MSG, PDF, images; scripts/cloud_file_ops.py                                       |
| **Notion**           | Records, case wikis, timelines | MCP `plugin-Notion-notion`; litigation_prep agent                                   | Case wikis, RICO matrix, checklists, timeline tables                                        |
| **Airtable**         | Records, tables, timelines     | MCP `user-airtable`; litigation_prep agent                                          | Case data, scrape results, timeline tables, contact lists                                   |
| **LLMs**             | Derived artifacts              | Orchestrator routing (Vertex, Gemini, private LLM); structured_output               | Summaries, entity extraction, privilege routing; store outputs in LexVault with attribution |
| **Timelines**        | Structured events              | Schemas: timeline-event, comprehensive-review-and-timeline; Notion/Airtable/Neo4j   | Chronological events; link to evidence objects; human checkpoints                           |

### Photo and file handling

- **Photos:** Ingest as raw assets; run OCR/vision for document-photos; metadata template includes `document_type: photo`. Use photo-document evidence playbook and `docs/schemas/photo-document-evidence.schema.json`.
- **Files:** All supported types (contract, email, financial, corporate, filing, communication, deposition, photo, other) from any connector; SHA-256 at ingest; derivatives (OCR, metadata, embeddings) in LexVault.
- **Records:** Structured rows from Notion, Airtable, or SharePoint lists → map to evidence or timeline rows; store references in LexVault provenance.

### MCP and config references

- **Connectors:** `config/connectors.yaml` — box, microsoft_365 (OneDrive/SharePoint), file_search roots (iCloud, OneDrive, desktop).
- **Agent × MCP matrix:** `config/agent-mcp-function-matrix.yaml` — notion, airtable, scrape_workflow; add lexvault_sources for intake.
- **Workflow search roots:** `config/workflows-messaging-sentiment-timeline.yaml` (example) — iCloud Drive, OneDrive, Google Drive, Dropbox, Desktop.
- **Instructions:** `docs/instructions/AGENT_MCP_FUNCTION_INSTRUCTIONS.md` — file/photo/record sources and timeline output.

---

## Box Integration (Enterprise Storage)

> Source: Notion "DEVELOPER DOCS-LEXVAULT-AGENTS"

### Configuration

- Primary storage: Box (1.8TB+ capacity)
- Identity: `rbailey@connectedenergyservices.com` (primary)
- Classification: 4-level (Public, Internal, Confidential, Restricted)

### Box Agent Cards

| Agent                              | Purpose                                                    |
| ---------------------------------- | ---------------------------------------------------------- |
| **Identity Consolidation Agent**   | Unify logins across Box/Notion, normalize profiles         |
| **Box Security Hardening Agent**   | 2FA, sharing defaults, session controls, DLP               |
| **Information Architecture Agent** | Collections, metadata templates, naming conventions        |
| **Governance & Review Agent**      | Quarterly access reviews, stale link cleanup, KPI tracking |

### Security Baseline

- 2-Step Verification (authenticator app, not SMS)
- Default sharing: "People in your company" (no public links)
- External collaboration: allowlist domains only
- Link expiration: required for all shared links
- Quarterly access review: external collaborators, shared links, sensitive folders

## Notion References

| Wiki                             | URL                                                              | Content                                       |
| -------------------------------- | ---------------------------------------------------------------- | --------------------------------------------- |
| LexVault OpenAI Integration      | [Notion](https://www.notion.so/07c119568abd4ccb9c3155ce939dc981) | Responses API, artifact storage, retrieval    |
| LexVault File System Ontology    | [Notion](https://www.notion.so/cbce73bf1d914b94ac027a91a7f2a567) | Metadata taxonomy, extraction agents          |
| Developer Docs - LexVault Agents | [Notion](https://www.notion.so/2d3ec5c813ef80598683d07b25133294) | Storage optimization, agent cards, governance |
