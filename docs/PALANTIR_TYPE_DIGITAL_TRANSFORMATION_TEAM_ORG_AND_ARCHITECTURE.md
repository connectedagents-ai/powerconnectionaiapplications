# Palantir-Type Digital Transformation Team — Org Structure, Enterprise Roles & Architecture

**Purpose:** Define the **organizational structure** of a Palantir-style digital transformation team, the **related enterprise (client) employees** they work with, and each role’s **expertise and place in the architecture**. Use for staffing engagements, RACI, governance, and aligning OneWish OS / Foundry-style deployments with client orgs.

**Governance:** [GAME_CHANGERS.md](GAME_CHANGERS.md) (Palantir-style integration); [constitution.md](constitution.md); ontology/schema: [modules/ontology.md](modules/ontology.md), [modules/lexvault.md](modules/lexvault.md).

---

## 1. Transformation team (vendor / embedded side)

The **digital transformation team** is the vendor-side group embedded with the client. Roles are defined by function, not hierarchy; small pods work end-to-end on a single customer or mission.

### 1.1 Forward Deployed Software Engineer (FDSE)

| Attribute | Definition |
|-----------|------------|
| **Role** | Technical lead embedded at client site; builds and integrates the platform (e.g. Foundry, OneWish-style stack) into client systems and workflows. |
| **Expertise** | Full-stack and data engineering: Python, Java, TypeScript/JavaScript, C++; data pipelines, APIs, integrations; ontology and schema design; security and access model. Operates like a “startup CTO” for the engagement. |
| **Responsibilities** | Design and implement integrations; manage large-scale data ingestion and transformation; build custom applications and workflows on the platform; discuss architecture with client and fellow engineers; establish technical strategy for the engagement. |
| **Architecture** | Owns **integration layer**: source systems → platform (ETL/ELT, APIs, connectors). Defines **object/link types**, **pipelines**, and **application contracts**. Interfaces with client **Enterprise Data Architect** and **IT/Infrastructure**. |
| **Typical background** | 1+ years post-college; strong algorithms and systems; willingness to travel 25–75% to client sites. |

### 1.2 Deployment Strategist (DS)

| Attribute | Definition |
|-----------|------------|
| **Role** | Sits at the intersection of **business operations** and **platform**; translates real-world workflows and questions into data models, analytics, and training. |
| **Expertise** | Data modeling and analytics; operational process design; stakeholder facilitation; training and change management; demo and presentation to analysts and executives. |
| **Responsibilities** | Meet onsite with client analysts to capture critical questions and pain points; identify and scope datasets with FDSEs; design and build bespoke workflows for user groups; lead training and adoption; present results to analysts and executives; feed product requirements back to core product. |
| **Architecture** | Owns **semantic layer** and **use-case definition**: ontologies, controlled vocabularies, and “questions the platform must answer.” Interfaces with client **CDO**, **business analysts**, **domain owners**, and **power users**. |
| **Typical background** | Analytical or operational background; comfort with data and with speaking to both technical and non-technical audiences. |

### 1.3 Forward Deployed Infrastructure Engineer (FDIE) / Baseline

| Attribute | Definition |
|-----------|------------|
| **Role** | Ensures the platform runs reliably across client environments (cloud, on-prem, hybrid, air-gapped). Part of “Baseline” or reliability-focused deployment. |
| **Expertise** | Infrastructure, DevOps, SRE: monitoring, alerting, configuration management; deployment and migration; troubleshooting and performance; on-call and incident response. |
| **Responsibilities** | Environment operations (provisioning, config, patching); product support (monitoring, debugging, optimization); infrastructure projects (migrations, scaling, automation). Reduce toil so FDSEs and clients focus on outcomes. |
| **Architecture** | Owns **runtime and environment**: availability, performance, security posture of the platform at the client. Interfaces with client **IT/Infrastructure**, **Security**, **CTO/VP Engineering**. |
| **Typical background** | Systems/DevOps/SRE; experience across cloud and on-prem; comfortable with on-call and customer-facing escalation. |

### 1.4 Engagement Lead / Deployment Lead

| Attribute | Definition |
|-----------|------------|
| **Role** | Single point of accountability for the engagement: scope, timeline, stakeholder alignment, and escalation. |
| **Expertise** | Program and account management; scope and change control; executive communication; risk and dependency management. |
| **Responsibilities** | Align with client executive sponsor (CDO/CTO/COO); prioritize backlog with DS and FDSE; remove blockers; report status and outcomes; manage commercial and contractual boundaries. |
| **Architecture** | **Orchestration**: aligns transformation team and client org; owns governance and decision cadence. Interfaces with **Executive Sponsor**, **CDO**, **CTO**, and internal product/commercial. |

### 1.5 Core product / engineering (back office)

| Attribute | Definition |
|-----------|------------|
| **Role** | Platform product and engineering (e.g. Foundry core, OneWish OS core). Not typically co-located with client; receives input from FDSEs and DSs. |
| **Expertise** | Product management; platform architecture; core pipelines, ontology engine, and application framework; security and compliance at product level. |
| **Responsibilities** | Roadmap and platform capabilities; support deployment teams with tooling, patterns, and fixes; incorporate deployment feedback into product. |
| **Architecture** | **Platform core**: shared ontology, connectors, and product features used by all deployments. Interfaces with **Engagement Lead**, **FDSE**, **DS** via internal channels. |

---

## 2. Enterprise (client) roles — related employees

These are the **client-side roles** that the transformation team works with. Defining them ensures clear handoffs, RACI, and governance.

### 2.1 Executive sponsor

| Attribute | Definition |
|-----------|------------|
| **Role** | Senior leader who owns the digital transformation initiative and budget; resolves strategic and organizational conflicts. |
| **Expertise** | Business strategy; organizational change; budget and prioritization; executive communication. |
| **Responsibilities** | Charter the program; align CDO/CTO/COO and business units; approve major scope and spend; hold organization accountable for adoption. |
| **Interface with transformation team** | **Engagement Lead**; quarterly or major-milestone reviews; escalation path. |

### 2.2 Chief Data Officer (CDO)

| Attribute | Definition |
|-----------|------------|
| **Role** | Executive responsible for **data strategy**, **governance**, **quality**, and **value from data** across the enterprise. |
| **Expertise** | Data strategy and governance; analytics and BI; regulatory and compliance (e.g. GDPR, sector rules); data literacy and culture. |
| **Responsibilities** | Set data strategy and standards; own data governance and stewardship model; sponsor centralization and democratization of data; drive move from descriptive to predictive/prescriptive use. |
| **Interface with transformation team** | **Deployment Strategist** (semantic layer, use cases, governance); **Engagement Lead** (priorities, scope). Often **Executive Sponsor** or delegate. |

### 2.3 CTO / VP Engineering

| Attribute | Definition |
|-----------|------------|
| **Role** | Owns **technology strategy**, **architecture**, and **engineering** for the enterprise (or business unit). |
| **Expertise** | Enterprise architecture; integration and API strategy; security and infrastructure; engineering practices and talent. |
| **Responsibilities** | Align platform adoption with enterprise architecture; approve integration patterns and security posture; allocate client engineering for APIs and source systems. |
| **Interface with transformation team** | **FDSE** (integrations, architecture); **FDIE** (infrastructure, reliability); **Engagement Lead** (technical scope, risk). |

### 2.4 Enterprise Data Architect

| Attribute | Definition |
|-----------|------------|
| **Role** | Designs **enterprise data models**, **integration patterns**, and **data flows**; aligns IT assets with business strategy. |
| **Expertise** | Data modeling (conceptual, logical, physical); API-first and microservices; master data and canonical models; lineage and metadata. |
| **Responsibilities** | Define canonical entities and integration contracts; align platform ontology with enterprise model; govern data flows and lineage. |
| **Interface with transformation team** | **FDSE** (object types, pipelines, APIs); **DS** (semantic alignment with business terms). Critical for **ontology and schema** alignment (Palantir Foundry Object/Link Types, OneWish/LexVault-style models). |

### 2.5 Data stewards / domain owners

| Attribute | Definition |
|-----------|------------|
| **Role** | Own **data quality**, **definitions**, and **usage rules** for a domain (e.g. customer, product, finance, legal). |
| **Expertise** | Domain data; quality rules and remediation; business definitions and KPIs; stewardship processes. |
| **Responsibilities** | Certify datasets and definitions; resolve quality issues; approve use of sensitive or regulated data; represent domain in governance. |
| **Interface with transformation team** | **Deployment Strategist** (workflows, training, definitions); **FDSE** (source system and quality requirements). |

### 2.6 Business analysts / product owners

| Attribute | Definition |
|-----------|------------|
| **Role** | Represent **business use cases** and **requirements**; own backlog for analytics and workflows. |
| **Expertise** | Process design; requirements and user stories; acceptance criteria; UAT and adoption. |
| **Responsibilities** | Define questions and outcomes; prioritize features and datasets; validate workflows and reports; drive adoption in business units. |
| **Interface with transformation team** | **Deployment Strategist** (primary); **FDSE** (data and feature feasibility). |

### 2.7 IT / Infrastructure & Security

| Attribute | Definition |
|-----------|------------|
| **Role** | Own **networks**, **identity**, **cloud/on-prem**, and **security controls** that the platform runs on. |
| **Expertise** | Network, identity (SSO, RBAC), cloud and on-prem ops; security and compliance (e.g. SOC2, FedRAMP). |
| **Responsibilities** | Provision environments; manage access and secrets; ensure connectivity and compliance; respond to incidents. |
| **Interface with transformation team** | **FDIE** (environment, monitoring, incidents); **FDSE** (integration endpoints, auth). |

### 2.8 Power users / analysts

| Attribute | Definition |
|-----------|------------|
| **Role** | Day-to-day users who run analyses, build workflows, and consume the platform. |
| **Expertise** | Domain analysis; tool usage; self-serve reporting and exploration. |
| **Responsibilities** | Use platform for decisions; report issues and enhancement requests; adopt new workflows and data. |
| **Interface with transformation team** | **Deployment Strategist** (training, demos, support); **FDSE** (bugs, performance). |

---

## 3. Architecture — how roles connect

### 3.1 Layered view

```
                    ┌─────────────────────────────────────────────────────────┐
                    │                  EXECUTIVE SPONSOR                       │
                    │            (CDO / CTO / COO — charter, budget)            │
                    └─────────────────────────────┬───────────────────────────┘
                                                  │
         ┌────────────────────────────────────────┼────────────────────────────────────────┐
         │                                        │                                        │
         ▼                                        ▼                                        ▼
┌─────────────────┐                   ┌─────────────────┐                   ┌─────────────────┐
│   CDO            │                   │   CTO / VP Eng   │                   │   Engagement    │
│   Data strategy  │◄──────────────────│   Architecture  │──────────────────►│   Lead          │
│   Governance     │                   │   Integration   │                   │   (vendor)     │
└────────┬────────┘                   └────────┬────────┘                   └────────┬────────┘
         │                                      │                                      │
         │         ┌────────────────────────────┼────────────────────────────┐         │
         │         │                            │                            │         │
         ▼         ▼                            ▼                            ▼         ▼
┌─────────────────┐  ┌─────────────────┐  ┌─────────────────┐  ┌─────────────────┐  ┌─────────────────┐
│ Data stewards /  │  │ Enterprise Data │  │ FDSE            │  │ FDIE (Baseline) │  │ Deployment      │
│ domain owners    │  │ Architect       │  │ Integrations    │  │ Infra / SRE     │  │ Strategist      │
└────────┬────────┘  └────────┬────────┘  └────────┬────────┘  └────────┬────────┘  └────────┬────────┘
         │                     │                    │                    │                    │
         │                     │                    │                    │                    │
         └─────────────────────┴────────────────────┴────────────────────┴────────────────────┘
                                                  │
                    ┌─────────────────────────────┼─────────────────────────────┐
                    │                             │                             │
                    ▼                             ▼                             ▼
         ┌─────────────────┐            ┌─────────────────┐            ┌─────────────────┐
         │ Business        │            │ IT / Infra /    │            │ Power users /   │
         │ analysts / PO   │            │ Security        │            │ analysts        │
         └─────────────────┘            └─────────────────┘            └─────────────────┘
                                                  │
                                                  ▼
                    ┌─────────────────────────────────────────────────────────┐
                    │   PLATFORM (Foundry / OneWish-style)                     │
                    │   Ontology • Pipelines • Apps • Governance • Connectors   │
                    └─────────────────────────────────────────────────────────┘
```

### 3.2 Ownership by layer

| Layer | Owner (vendor) | Owner (client) | Main handoffs |
|-------|----------------|----------------|----------------|
| **Strategy & governance** | Engagement Lead | Executive Sponsor, CDO | Charter, scope, priorities, governance model |
| **Data strategy & semantics** | Deployment Strategist | CDO, Enterprise Data Architect, Data stewards | Ontology, definitions, use cases, training |
| **Integration & pipelines** | FDSE | Enterprise Data Architect, IT | Source systems, APIs, object/link types, pipelines |
| **Runtime & infrastructure** | FDIE | IT, Security | Environments, monitoring, access, incidents |
| **Product & platform core** | Core product / engineering | — | Roadmap, connectors, product features |
| **Usage & adoption** | Deployment Strategist | Business analysts, Power users | Workflows, demos, training, feedback |

### 3.3 RACI (high level)

| Activity | Engagement Lead | DS | FDSE | FDIE | CDO | CTO | Data Architect | Stewards | BA / PO |
|----------|-----------------|----|-----|------|-----|-----|----------------|----------|---------|
| Program charter & scope | A | C | C | I | R | R | I | I | I |
| Ontology & semantics | I | A/R | C | I | A | I | R | C | C |
| Integrations & pipelines | I | C | A/R | C | I | R | R | C | I |
| Environment & reliability | I | I | C | A/R | I | R | I | I | I |
| Training & adoption | I | A | C | I | R | I | I | C | R |
| Governance & compliance | A | C | C | I | R | C | C | R | I |

*A = Accountable, R = Responsible, C = Consulted, I = Informed.*

---

## 4. Expertise summary table

| Role | Primary expertise | Secondary | Architecture focus |
|------|-------------------|-----------|--------------------|
| **FDSE** | Integrations, data engineering, ontology/schema | Full-stack, APIs, security | Integration layer; object/link types; pipelines |
| **Deployment Strategist** | Data modeling, analytics, change management | Process design, training, demos | Semantic layer; use cases; adoption |
| **FDIE / Baseline** | Infra, DevOps, SRE, reliability | Security, monitoring, migration | Runtime; environments; incidents |
| **Engagement Lead** | Program/account management, stakeholder alignment | Scope, risk, commercial | Orchestration; governance; escalation |
| **CDO** | Data strategy, governance, value from data | Analytics, compliance, culture | Strategy; governance; sponsorship |
| **CTO / VP Eng** | Enterprise architecture, tech strategy | Security, engineering org | Architecture alignment; integration approval |
| **Enterprise Data Architect** | Data models, integration patterns, lineage | API design, canonical models | Ontology alignment; contracts; lineage |
| **Data stewards** | Domain data, quality, definitions | Governance, remediation | Quality; definitions; domain approval |
| **Business analysts / PO** | Requirements, use cases, adoption | UAT, backlog | Use-case definition; prioritization |
| **IT / Infra / Security** | Networks, identity, cloud, security | Compliance, incidents | Environment; access; compliance |
| **Power users** | Domain analysis, tool usage | Reporting, exploration | Usage; feedback; adoption |

---

## 5. Alignment with OneWish OS and game changers

When running a **Palantir-style** digital transformation using OneWish OS and related game changers:

- **Ontology, syntax, schema, orchestration** (GAME_CHANGERS Palantir-style) are owned jointly by **FDSE** + **Deployment Strategist** with **Enterprise Data Architect** and **Data stewards**.
- **Conversion / translation / adapters** for heterogeneous data are owned by **FDSE** with **FDIE** for runtime.
- **Enterprise employees** (CDO, CTO, Data Architect, stewards, BAs, IT, users) are the **related roles** above; the transformation team embeds and aligns with them per the RACI and architecture.
- **Governance and human-in-the-loop** (constitution) apply: high-stakes outputs (e.g. privilege, compliance, production decisions) route through appropriate **client roles** (e.g. CDO, Legal, Data stewards) and **Engagement Lead** for escalation.

---

## 6. References

| Doc | Purpose |
|-----|---------|
| [GAME_CHANGERS.md](GAME_CHANGERS.md) | Palantir-style integration; ontology, schema, orchestration |
| [modules/ontology.md](modules/ontology.md) | Object/link types; enterprise analytics patterns |
| [modules/lexvault.md](modules/lexvault.md) | Evidence and document models; Foundry-style references |
| [constitution.md](constitution.md) | Human-in-the-loop; claim typing; audit; governance |

---

_Maintain at: docs/PALANTIR_TYPE_DIGITAL_TRANSFORMATION_TEAM_ORG_AND_ARCHITECTURE.md. Update when adding roles, changing RACI, or aligning to new client org patterns._
