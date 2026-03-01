# Legal Tech Stack Cost Calculation & Evaluation — Direct Cost, Add/Cut Features, Security-First

**Purpose:** Provide **whitepapers, repos, and industry-standard worksheets** to calculate the **cost of each stack** if paid direct to each related service; **work types** and **what can be done by LLM type** (by capability and to maximize cost efficiency) **in context of LitigationForce.AI (LitForce)**, **LexVault**, **OneWish OS**, and **Genie desktop**; and an evaluation sheet to cut cost or add/delete features and platforms—with **security as a top priority** in every decision.

**Governance:** [security.md](security.md) (RBAC, audit, PII/privilege); [constitution.md](constitution.md) (human-in-the-loop); [LAW_FIRM_ORG_CHARTS_AND_OUTSOURCED_SERVICES.md](LAW_FIRM_ORG_CHARTS_AND_OUTSOURCED_SERVICES.md) (§7–§8 stacks and legal tech list).

---

## 1. Security as top priority (non-negotiable)

**Security is a top priority.** Do not sacrifice security for cost. When calculating cost or evaluating add/cut, apply security criteria first; then optimize cost within security-compliant options.

### 1.1 Security-first checklist (vendor and platform)

Use this before cost or feature trade-offs. If a vendor or platform fails core security, do not select it regardless of price.

| Criterion | Requirement | Source / note |
|-----------|-------------|----------------|
| **Authentication** | MFA available and enforced for sensitive access; SSO where possible | Attorney at Work Legal Tech Security Checklist |
| **Encryption** | Data encrypted in transit and at rest | [security.md](security.md) §3 |
| **Access control** | RBAC; least privilege; audit trail for access and key actions | [security.md](security.md) §1, §2 |
| **Activity monitoring** | End-to-end user activity monitoring; audit trail for compliance | Attorney at Work; [security.md](security.md) §2 |
| **Vendor posture** | SOC 2 Type II and/or ISO 27001; routine security audits and testing | Industry standard; 54% of firms cite security as top barrier (Bloomberg Legal Ops Survey) |
| **Data privacy** | GDPR/CCPA alignment; data subject request handling; tenant isolation | [security.md](security.md) §3; Attorney at Work |
| **AI / GenAI** | Transparency and explainability; how client data is used and protected | Sedona AI Commentary; Attorney at Work AI transparency |
| **Backup & DR** | Data backups and disaster recovery; incident response plan | Attorney at Work; [security.md](security.md) |

**References:** [Legal Tech Security Checklist — Attorney at Work](https://www.attorneyatwork.com/legal-tech-security-checklist/); [security.md](security.md).

---

## 2. Whitepapers, repos, and industry worksheets — stack cost (direct to each service)

Use these **sources** to populate or sanity-check **direct cost** of each service in your stack (what you pay each vendor if paid direct).

### 2.1 Cost calculators and ROI tools

| Source | What it provides | URL / location |
|--------|-------------------|----------------|
| **Brightflag ROI Calculator** | Legal e-billing ROI; input annual legal spend, attorneys, paralegals, admin; outputs savings across financial planning, productivity, spend reduction | https://brightflag.com/roi-calculator/ |
| **Uptime Practice — Cloud Cost Comparator** | On-prem vs private/cloud for law firms; pre-populated average tech costs; customizable | https://uptimepractice.com/resources/on-premise-vs-private-cloud-calculator/ |
| **InvestCEE Legal Technology Costs Report** | Licensing models, onboarding fees, advisory costs; monthly/annual cost ranges; ROI guidance; 5-step investment strategy | https://investcee.hu/legal-technology-costs-report/ |

### 2.2 Buying guides and budget worksheets

| Source | What it provides | URL / location |
|--------|-------------------|----------------|
| **Centerbase 2025 Legal Technology Buyer's Guide** | Five-step process; setting realistic budget; prioritizing outcomes; vendor comparison | Centerbase (PDF): 2025 Legal Technology Buyers Guide |
| **LawVu Legal Tech Buying Guide** | Cost of delay (e.g. 3.16 hrs/team member/week; ~$89K/year for 5-person team); quantifies value of adoption | https://lawvu.com/resources/legal-tech-buying-guide/ |
| **Cimphony Legal Tech Assessment Guide 2024** | Assessment framework; KPIs; data migration; vendor support models | https://www.cimphony.ai/insights/legal-tech-assessment-guide-2024 |
| **Osprey — How to Reduce the Cost of Legal Software** | Downloadable guide for reducing software spend | https://ospreyapproach.com/download-guide-how-to-reduce-the-cost-of-legal-software/ |
| **MyLegalSoftware — Plan Your Firm's Tech Budget** | Inventory current costs; set priorities; estimate TCO; stagger purchases; budget for adoption/training | https://mylegalsoftware.com/legal-tech-budget-planning-for-law-firms/ |

### 2.3 TCO (total cost of ownership) templates

| Source | What it provides | URL / location |
|--------|-------------------|----------------|
| **AllCaps TCO Analysis Template** | Total cost of ownership analysis template for software lifecycle | https://www.allcapsinc.com/resources/ (TCO template) |
| **TCO factors (case management)** | Acquisition, implementation, operational, indirect costs; lifecycle view beyond purchase price | Zigpoll / legal tech TCO articles |

### 2.4 Vendor pricing models (illustrative — verify with vendor)

| Category | Example vendors | Typical pricing model | Use for direct-cost worksheet |
|----------|------------------|------------------------|------------------------------|
| **eDiscovery** | Everlaw, Lexbe, Logikcull | Per GB uploaded/hosted; often unlimited users; AI add-ons usage-based | Estimate: annual GB × $/GB + add-ons |
| **Case / practice mgmt** | Prevail, Clio, MyCase, Filevine | Per user/month or tiered; some one-time + support | Users × $/user/month or tier price |
| **DMS** | iManage, NetDocuments | Per seat or per matter; enterprise agreements | Seats or matters × rate |
| **Research** | Lexis, Westlaw, Casetext | Per seat or flat; practice-area bundles | Seats × rate or bundle price |
| **Billing** | Elite, Aderant, Clio, Bill4Time | Per seat or % of collections; modules | Seats or % + modules |
| **Microsoft 365 (Teams, Planner)** | Microsoft | Per user/month (E3/E5); Planner included in most plans | Users × license tier |

**Note:** Pricing changes frequently. Use vendor quotes and the worksheets below to record **your** direct cost per service.

### 2.5 Internal repo — matter-level cost (hours and rates)

For **matter-level** cost (hours × rates, sensitivities, optimization levers), use the existing cost estimator — not direct vendor stack cost, but complementary:

| Item | Purpose |
|------|---------|
| [cost-estimator.md](cost-estimator.md) | Hours per matter by phase/role; rates; sensitivity; optimization ranking (e.g. TAR, privilege workflow, ESI scope) to reduce hours/cost |
| `config/cost-estimator.yaml` | Rates, phases, optimization levers |
| `scripts/cost-estimator.py` | Run matter cost and fact-check |

---

## 3. Worksheet: direct cost of each stack (paid direct to each service)

Use this structure to **calculate cost of each stack** if paid direct to each related service. Fill per firm size and stack (see [LAW_FIRM_ORG_CHARTS_AND_OUTSOURCED_SERVICES.md](LAW_FIRM_ORG_CHARTS_AND_OUTSOURCED_SERVICES.md) §7–§8).

### 3.1 Direct-cost worksheet (per service)

| Service / platform | Vendor | Pricing unit (e.g. per user, per GB) | Your quantity | Unit price | Annual direct cost | Notes (e.g. term, add-ons) |
|--------------------|--------|--------------------------------------|---------------|------------|---------------------|-----------------------------|
| Case / matter mgmt | | | | | | |
| DMS | | | | | | |
| eDiscovery | | | | | | |
| Legal research | | | | | | |
| Billing & time | | | | | | |
| Collaboration (Teams, Planner, etc.) | | | | | | |
| CRM / BD | | | | | | |
| Conflicts / intake | | | | | | |
| Contract / CLM | | | | | | |
| Compliance / risk | | | | | | |
| AI / drafting assist | | | | | | |
| Court / filing | | | | | | |
| Other (list) | | | | | | |
| **Total annual (direct)** | | | | | **Sum** | |

### 3.2 TCO categories (beyond direct license/subscription)

When comparing or cutting cost, include **full TCO** so hidden costs are visible:

| TCO category | Examples | Worksheet column or section |
|--------------|----------|-----------------------------|
| **Acquisition** | License/subscription; one-time purchase; onboarding fee | Direct cost (above) |
| **Implementation** | Installation; customization; training; data migration; consulting | One-time; allocate by year if multi-year |
| **Operational** | Annual renewal; maintenance; support; hosting; upgrades; extra seats | Recurring; add to annual direct |
| **Indirect** | Downtime; productivity loss during rollout; compliance penalties if breach | Risk buffer; document assumptions |

**Formula (simplified):**  
`Annual TCO (year 1) ≈ Direct annual + (Implementation / N years) + Operational + Risk buffer`

---

## 4. Evaluation sheet: cut cost / add or delete features and platforms

Use this **evaluation process** when deciding to **cut cost** or **add/delete features or platforms**. Security remains the top priority; then cost and fit.

### 4.1 Decision order (security first)

1. **Security gate** — For any vendor or platform (existing or new), run the [§1.1 Security-first checklist](#11-security-first-checklist-vendor-and-platform). If it fails, do not add; plan to replace if already in use.
2. **Must-have vs nice-to-have** — Classify each feature/platform as required for practice, compliance, or client obligation vs optional.
3. **Cost vs value** — For required items, minimize cost within security-compliant options. For optional items, explicitly decide add/keep/cut based on value and total budget.

### 4.2 How to cut cost (without compromising security)

| Lever | Action | Security note |
|-------|--------|----------------|
| **Consolidate vendors** | Reduce overlapping tools (e.g. one DMS, one practice mgmt); negotiate volume | Ensure consolidated vendor meets §1.1 |
| **Right-size seats** | Remove unused seats; use tiered licensing (e.g. view-only vs full) | Preserve RBAC and audit |
| **Usage-based where beneficial** | Prefer per-GB or per-matter for variable workload (e.g. eDiscovery) vs over-licensing | Confirm data handling and encryption unchanged |
| **Renewal timing** | Align renewals; multi-year for discount only after security and terms verified | Lock in only after security audit |
| **Training and adoption** | Reduce churn and rework; use [cost-estimator.md](cost-estimator.md) levers (TAR, privilege workflow, etc.) to lower matter hours | Human checkpoints and oversight unchanged |
| **Open or built-in where viable** | Use Microsoft 365 (Teams, Planner) where already licensed; reduce point solutions | M365 security and compliance config required |
| **De-scope features** | Turn off unused modules or add-ons (e.g. AI assist if not required) | Do not disable security or audit features |

### 4.3 How to choose to add or delete features and platforms

| Question | Use to |
|----------|--------|
| Does it pass the security checklist (§1.1)? | **Add:** Only if yes. **Delete:** If current platform fails, plan replacement before exit. |
| Is it required for practice, ethics, or client obligation? | **Add:** If gap. **Delete:** Only if not required and not relied upon. |
| What is the full TCO (acquisition + implementation + operational)? | **Add:** Compare TCO to value and to budget. **Delete:** Compare savings to migration and risk. |
| Does it duplicate another tool we already have? | **Add:** Prefer extending existing (e.g. Planner + Teams) over new vendor. **Delete:** Prefer consolidating to one. |
| What is the impact on audit, privilege, and confidentiality? | **Add:** Ensure audit trail and access control. **Delete:** Ensure no loss of required retention or audit. |

### 4.4 Add/keep/cut matrix (example)

| Platform / feature | Security pass? | Required? | TCO (annual) | Decision (example) |
|--------------------|----------------|------------|---------------|--------------------|
| Practice mgmt | Yes | Yes | $X | Keep; right-size seats |
| DMS | Yes | Yes | $Y | Keep |
| eDiscovery (vendor A) | Yes | Yes | $Z | Keep; consider usage-based tier |
| AI drafting add-on | Yes | No | $W | Cut if low usage; else keep with usage cap |
| Redundant research tool | Yes | No | $V | Cut; standardize on one |

---

## 5. References (whitepapers, worksheets, security)

| Type | Item | Purpose |
|------|------|---------|
| **Security** | [security.md](security.md) | RBAC, audit, PII/privilege, simulation enforcement |
| **Security** | [Attorney at Work — Legal Tech Security Checklist](https://www.attorneyatwork.com/legal-tech-security-checklist/) | MFA, SSO, encryption, RBAC, vendor certs, backup/DR |
| **Cost / ROI** | [Brightflag ROI Calculator](https://brightflag.com/roi-calculator/) | Legal e-billing ROI |
| **Cost** | [Uptime Practice — Cloud Cost Comparator](https://uptimepractice.com/resources/on-premise-vs-private-cloud-calculator/) | On-prem vs cloud law firm |
| **Cost** | [InvestCEE Legal Technology Costs Report](https://investcee.hu/legal-technology-costs-report/) | Licensing, fees, cost ranges, 5-step strategy |
| **Buying / budget** | Centerbase 2025 Legal Technology Buyer's Guide | Budget and prioritization |
| **Buying** | [LawVu Legal Tech Buying Guide](https://lawvu.com/resources/legal-tech-buying-guide/) | Cost of delay; value of adoption |
| **TCO** | AllCaps TCO Analysis Template | Total cost of ownership |
| **Reduce cost** | [Osprey — Reduce Cost of Legal Software](https://ospreyapproach.com/download-guide-how-to-reduce-the-cost-of-legal-software/) | How to reduce spend |
| **Budget** | [MyLegalSoftware — Tech Budget Planning](https://mylegalsoftware.com/legal-tech-budget-planning-for-law-firms/) | Inventory; TCO; adoption budget |
| **Internal** | [cost-estimator.md](cost-estimator.md) | Matter-level hours/rates; optimization levers |
| **Stack context** | [LAW_FIRM_ORG_CHARTS_AND_OUTSOURCED_SERVICES.md](LAW_FIRM_ORG_CHARTS_AND_OUTSOURCED_SERVICES.md) §7–§8 | Dev/tech stack by firm size; legal tech list |

---

**Simulation disclaimer:** Cost figures and vendor examples are illustrative. Not legal or financial advice. Verify pricing and security with vendors and your counsel. Always prioritize security over cost.
