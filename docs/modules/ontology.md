# Ontology — Naming Conventions, Schema Standards & Taxonomy

> Source: Notion wikis "LEXVAULT-File System Ontology", "CRM Ontology / Schema / Syntax / Taxonomy", "Master Guide: Naming Conventions", "ONTOLOGY-CONNECTED COMPANIES STRUCTURE NAMING CONVENTIONS", "Ontology-RICO Case Master Directory Structure"

## Overview

The ontology system defines the shared language, structure, and naming conventions used across all LitigationForce.AI components — ensuring consistency between LexVault, Neo4j, Attio CRM, Box, Notion, and the agent pipeline.

## Cross-Platform Compatibility

The ontology is designed to work across:

| Platform             | Model Type                     | Integration                   |
| -------------------- | ------------------------------ | ----------------------------- |
| Neo4j                | Property Graph (nodes + edges) | Knowledge Graph Builder agent |
| Palantir Foundry     | Object/Link Types              | Enterprise analytics          |
| Microsoft Graph API  | Entity/Relationship            | Office 365 integration        |
| Box Content Graph    | File metadata                  | LexVault storage layer        |
| Attio CRM            | Objects/Attributes             | Entity profiles               |
| HubSpot / Salesforce | Objects/Properties             | Sales pipeline                |
| Supabase Postgres    | Relational tables              | Web application               |
| Vector DB            | Embeddings + metadata          | Semantic search               |

## Data Type Suffixes (Standard)

| Suffix  | Type             | Example                                  |
| ------- | ---------------- | ---------------------------------------- |
| `_id`   | UUID/identifier  | `evidence_id`, `claim_id`                |
| `_txt`  | Text/string      | `custodian_txt`, `description_txt`       |
| `_int`  | Integer          | `page_count_int`, `act_count_int`        |
| `_dec`  | Decimal          | `confidence_dec`, `amount_dec`           |
| `_bool` | Boolean          | `is_privileged_bool`, `gate_passed_bool` |
| `_json` | JSON data        | `metadata_json`, `entities_json`         |
| `_dt`   | Date/datetime    | `collected_dt`, `reviewed_dt`            |
| `_enum` | Enumerated value | `track_enum`, `status_enum`              |

## Entity Types (RICO Case Master)

> Source: Notion "Ontology-RICO Case Master Directory Structure"

### Person Entities

- Plaintiff individuals (Robert Bailey, etc.)
- Defendant individuals (Angela Blair, Carson Blair, Ryan Wuerch, etc.)
- Witnesses, experts, attorneys, judges

### Organization Entities

- Plaintiff entities (Connected Solar LLC, Power Connection, NetZero Lending, Connected Energy Services)
- Defendant entities (Tesla Inc., Vikta Energy, Volt Street, KPost, etc.)
- Courts, regulatory bodies, financial institutions

### Document Entities

- Contracts (EPC agreements, NDAs, installer agreements)
- Communications (emails, texts, social media posts)
- Financial records (invoices, payments, bank statements)
- Corporate records (formation docs, board minutes, filings)
- Court filings (complaints, motions, orders)

### Event Entities

- Contract events (signing, modification, breach, termination)
- Communication events (meetings, calls, emails)
- Financial events (payments, transfers, invoicing)
- Legal events (filings, hearings, orders, depositions)
- Predicate acts (wire fraud, mail fraud, extortion, etc.)

## RICO Case Master Directory Structure

```
/RICO_CASE_MASTER/
├── /Parsed_Documents/
│   ├── /Raw_Extracts/
│   ├── /Processed_Text/
│   └── /Metadata_Tables/
├── /Entity_Maps/
│   ├── /Person_Profiles/
│   ├── /Organization_Profiles/
│   └── /Relationship_Matrices/
├── /Timeline_Data/
│   ├── /Master_Timeline/
│   ├── /Track_A_CA/
│   ├── /Track_B_TX/
│   └── /Track_C_RICO/
├── /Pattern_Analysis/
│   ├── /Predicate_Acts/
│   ├── /Enterprise_Structure/
│   └── /Continuity_Evidence/
├── /Financial_Modeling/
│   ├── /Damages_Calculations/
│   ├── /Lost_Profits/
│   └── /Treble_Damages/
├── /Legal_Claims_Logs/
│   ├── /Claim_Matrix/
│   └── /Evaluator_Results/
└── /Production_Sets/
    ├── /Privilege_Log/
    ├── /Bates_Stamped/
    └── /Redaction_Log/
```

## CRM Ontology (Attio/HubSpot/Salesforce)

| Object           | Fields                                              | Purpose                   |
| ---------------- | --------------------------------------------------- | ------------------------- |
| **Person**       | name, role, affiliation, track, risk_level          | Litigation party tracking |
| **Organization** | name, type, jurisdiction, formation_date            | Entity tracking           |
| **Matter**       | matter_id, title, tracks, status, lead_attorney     | Case management           |
| **Relationship** | from_entity, to_entity, type, evidence_ids          | Entity linking            |
| **Event**        | date, type, actors, evidence_ids, track             | Timeline building         |
| **Claim**        | claim_type, text, sources, track, evaluator_results | Assertion tracking        |

## Integration with Master Repo

| Ontology Component | Maps to Repo Artifact                                           |
| ------------------ | --------------------------------------------------------------- |
| Entity types       | `docs/schemas/evidence-object.schema.json` (entities_extracted) |
| Event types        | `docs/schemas/timeline-event.schema.json` (category enum)       |
| RICO directory     | `docs/schemas/pattern-score.schema.json`                        |
| Naming conventions | `.cursor/rules/master-project-rules.mdc`                        |
| CRM mapping        | `docs/cross-system-index.md` → Attio integration                |
| File metadata      | `docs/modules/lexvault.md` → Metadata Template                  |

## Notion References

| Wiki                           | URL                                                              | Content                               |
| ------------------------------ | ---------------------------------------------------------------- | ------------------------------------- |
| LexVault File System Ontology  | [Notion](https://www.notion.so/cbce73bf1d914b94ac027a91a7f2a567) | Metadata taxonomy, extraction agents  |
| CRM Ontology / Schema / Syntax | [Notion](https://www.notion.so/a6a70649972c4dd7b9f9b98869d61698) | Cross-platform consistency            |
| Master Naming Conventions      | [Notion](https://www.notion.so/1d20221dea1f41b9a9c288dd74014f60) | Unified naming guide                  |
| Connected Companies Naming     | [Notion](https://www.notion.so/299ec5c813ef8000be7ff00e091d499b) | Data type suffixes, field conventions |
| RICO Case Master Directory     | [Notion](https://www.notion.so/1daec5c813ef802d9f2ecaf9d4c51acb) | Case file organization structure      |
