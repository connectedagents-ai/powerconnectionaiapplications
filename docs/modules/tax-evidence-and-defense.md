# Tax Module — Historical Tax, OIC, QOZ, Fees & Evidence Prep (Defense)

> **Purpose:** Tax information architecture: historical tax by year and tags, fees/expenses calculator, IRS quick links (Qualified Opportunity Zones, Offer in Compromise), knowledge graph, timelines, and **evidence prep connected to Litigation Force** for defense prep.
>
> **Governance:** Constitution applies. Not legal or tax advice; use with qualified CPA/tax counsel.

---

## 1. Scope

| Area                     | Description                                                                                                                                                            |
| ------------------------ | ---------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| **Historical tax**       | Filings, notices, and docs by **year** (`TY-YYYY`) and **tags** (qoz, oic, litigation_defense, etc.)                                                                   |
| **Ontology & hierarchy** | Single source of truth: `docs/ontology/TAX_ONTOLOGY_AND_HIERARCHY.md`, `config/ontology/tax-ontology.yaml`                                                             |
| **Knowledge graph**      | Nodes: TaxYear, Filing, OIC, QOZInvestment, FeeOrExpense, TimelineEvent, Document; views for timeline, OIC status, QOZ, fees, **defense-evidence linkage**             |
| **Timelines**            | Master + by-year; schema: `docs/schemas/tax-timeline-event.schema.json`                                                                                                |
| **Fees & expenses**      | Calculator spec and schemas; aggregate by year/tag                                                                                                                     |
| **IRS quick links**      | QOZ, OIC, forms, publications: `docs/context/IRS_QUICK_LINKS_AND_QUALIFIED_OPPORTUNITY_ZONES.md`, `examples/tax/irs-links/index.yaml`                                  |
| **Agents**               | Tax review, OIC, tax planner, **tax evidence prep** (defense bundles → Litigation Force)                                                                               |
| **Defense prep**         | Tax evidence prep agent produces exhibit list and timeline slice; **linked to Litigation Force** matter(s) and exhibit index for defense narrative and deposition prep |

---

## 2. Connection to Litigation Force (Defense Prep)

- **Link file:** `examples/tax/evidence-prep/litigation-force-link.yaml` — matter_id(s), exhibit index path(s).
- **Flow:** Tax documents tagged `litigation_defense` → tax evidence prep agent → defense bundle (exhibit list, summaries, claim typing) → **Litigation Force** evidence_linker / litigation_prep for defense prep.
- **Standards:** Same claim typing (FACT / INFERENCE / OPINION) and evidence pointers as `docs/LITIGATION_EVIDENCE_AND_EXHIBITS.md`; attorney review required.

---

## 3. Key Paths

| Resource             | Path                                                                                                                |
| -------------------- | ------------------------------------------------------------------------------------------------------------------- |
| Ontology (narrative) | docs/ontology/TAX_ONTOLOGY_AND_HIERARCHY.md                                                                         |
| Ontology (YAML)      | config/ontology/tax-ontology.yaml                                                                                   |
| KG schema            | examples/tax/knowledge-graph/tax-kg-schema.json                                                                     |
| KG views             | examples/tax/knowledge-graph/views/\*.cypher                                                                        |
| IRS links            | docs/context/IRS_QUICK_LINKS_AND_QUALIFIED_OPPORTUNITY_ZONES.md, examples/tax/irs-links/index.yaml                  |
| Workflows            | config/workflows-tax-oic-evidence.yaml                                                                              |
| Playbooks            | docs/playbooks/tax-review-agent.md, oic-agent.md, tax-planner-agent.md, tax-evidence-prep-agent.md                  |
| Segment              | config/segment-lit-force-lexvault-connected.yaml (segment: tax; lit_force knowledge_paths include tax defense-prep) |

---

## 4. Related

- [MASTER_ONTOLOGY_AND_FOLDER_HIERARCHY.md](ontology/MASTER_ONTOLOGY_AND_FOLDER_HIERARCHY.md) — Litigation matter (BAILEY-TESLA); align tax evidence to same principles.
- [LITIGATION_EVIDENCE_AND_EXHIBITS.md](LITIGATION_EVIDENCE_AND_EXHIBITS.md) — KG views, exhibits, Lit Force evidence standards.
