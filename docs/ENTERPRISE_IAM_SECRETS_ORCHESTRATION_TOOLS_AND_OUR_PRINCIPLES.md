# Enterprise IAM, Secrets, Orchestration Tools — How Their Principles Mirror Ours and Best Practices We Adopt

**Purpose:** (1) Catalog **top-level dev tools, orchestration tools, auth, SSH, and similar tools** that manage systems, passwords, connections, and names by **entity** and **multi-entity** across the enterprise (Okta, JumpCloud, HashiCorp Vault, Teleport, BeyondTrust, CyberArk, 1Password, etc.). (2) Map **how their principles mirror ours**. (3) Capture **best practices we adopt** for **architecture**, **naming**, and **ontology** so we stay aligned to industry standards while keeping our single source of truth and product-that-builds-the-product tenet.

**Governance:** [ONEWISHOS_ARCHITECTURE_AND_METHODS.md](ONEWISHOS_ARCHITECTURE_AND_METHODS.md); [SOURCES_AND_EMULATION_INDEX.md](SOURCES_AND_EMULATION_INDEX.md); [1PASSWORD_VAULT_ORGANIZATION.md](1PASSWORD_VAULT_ORGANIZATION.md); [config/ontology/entity-account-master.yaml](../config/ontology/entity-account-master.yaml).

---

## 1. Enterprise tools (catalog)

| Category | Tools | What they manage | Entity / multi-entity |
|----------|-------|------------------|------------------------|
| **Identity & access (IAM)** | **Okta**, **JumpCloud**, Auth0, Azure AD / Entra, Ping Identity | Users, groups, SSO, MFA, RBAC, app access, directory | Users and groups by org/tenant; multi-tenant and B2B; per-entity policies |
| **Secrets & credentials** | **HashiCorp Vault**, **1Password** (Teams/Business), CyberArk Vault, AWS Secrets Manager, Doppler | Passwords, API keys, certs, tokens; vault taxonomy; namespace/path structure | Namespaces per tenant/team; paths by app/service/entity; naming taxonomy |
| **SSH & privileged access** | **Teleport**, **BeyondTrust**, **CyberArk** (PAM), ScaleFT (Okta) | SSH keys, server access, just-in-time (JIT) access, session recording, zero standing access | Labels/tags by environment, team, entity; role-based SSH; audit by resource |
| **Orchestration & config** | Terraform, Ansible, Kubernetes (RBAC, namespaces), GitOps (Flux, Argo) | Infrastructure and config as code; propagation; single source (repo) | Namespaces per tenant/team; naming conventions; canonical repo |
| **Dev / IDE tooling** | Cursor, Claude Code, Codex, VS Code, Windsurf, Warp | Repos, MCPs, connectors, env; same governance and entry points | Canonical list; config-driven; cross-tool execution (our [DEV_TOOLS_CANONICAL_LIST_AND_AUDIT](DEV_TOOLS_CANONICAL_LIST_AND_AUDIT.md)) |

**Representative vendors (short):**
- **Okta:** Cloud IAM, SSO, MFA, lifecycle, Zero Trust; architectural factors (availability, reliability, security, compliance, maintainability).
- **JumpCloud:** Cross-OS device identity, SSO, LDAP/RADIUS, MFA, device management, server access; Zero Trust, JIT/least privilege.
- **HashiCorp Vault:** Secrets, PKI, SSH CA, namespaces (multi-tenant), path-based policies, audit logging.
- **Teleport:** SSH/kube/db access, certificate-based auth, RBAC with labels, default-deny, IaC (Terraform, K8s operator).
- **BeyondTrust / CyberArk:** Privileged access management (PAM), credential vaulting, session isolation, approval workflows.
- **1Password (Teams/Business):** Vaults, collections, RBAC, CLI (`op`), SSO, item taxonomy (we use: [1PASSWORD_VAULT_ORGANIZATION.md](1PASSWORD_VAULT_ORGANIZATION.md)).

---

## 2. How their principles mirror ours

| Their principle | Where they say it | Our mirror |
|-----------------|-------------------|------------|
| **Single source of truth** | Vault: one path per secret; Okta: one identity store; GitOps: one repo for desired state | One canonical file per category: repos → config/repos.yaml; MCPs/connectors → config/canonical-mcp-connectors.yaml, platform-connections; dev tools → DEV_TOOLS_CANONICAL_LIST_AND_AUDIT; vaults → 1Password taxonomy |
| **Least privilege** | Okta, JumpCloud, Teleport: lowest level of access needed; JIT where possible | Human checkpoint for high-stakes outputs; no destructive execution without approval; dry-run default for codify; guardrails (GUARDRAILS.md) |
| **Zero Trust** | Okta, JumpCloud, Teleport: never trust by default; verify every request | Verify before execute; Plan→Validate→Execute; connections and env verified in Full Review; no skip of targets (never-miss) |
| **RBAC / role-based access** | Okta, Vault, Teleport: roles and policies; labels/tags for scoping | Agent roles (orchestrator, specialists); phase×role matrix (INSTITUTIONAL_GRADE_BEST_PRACTICES_INDEX); vault taxonomy by function (DevOps, Legal, Finance, etc.) |
| **Audit trail & provenance** | Okta System Log; Vault audit devices; Teleport session recording; compliance logging | Constitution §3 (audit trail); chain-of-events.jsonl; eval-after-run; full-review-summary; standards-compliance |
| **Availability, reliability, scalability** | Okta architectural factors: redundancy, backup, monitoring, recovery, SLA | Never-miss propagation so no target skipped; no-fail Comprehensive Review; route then sync; fixed verification order |
| **Naming & taxonomy** | Vault: namespace/path structure; 1Password: vaults/collections; Teleport: labels | Vault taxonomy (1PASSWORD_VAULT_ORGANIZATION); entity-account-master (entity, DBA, accounts); config-driven naming (platform-connections, canonical-mcp-connectors) |
| **Multi-tenant / multi-entity** | Vault namespaces; Okta orgs/tenants; Teleport labels by env/team | Entity-account-master schema; vaults by domain (DevOps, Legal, Finance, etc.); repos and ROUTES by sub-OS / org |
| **Config / IaC** | Terraform Okta/Vault providers; Teleport Terraform/K8s; GitOps | Route-constitution, sync-all-repos from config/repos.yaml; scripts as executable spec; COMMANDS_AND_SCRIPTS_INDEX |
| **No standing access where avoidable** | JumpCloud, Teleport: JIT, short-lived certs, no long-lived keys | Pre-commit no secrets; .env.example only in repo; 1Password/op for runtime; human approval for destructive |

---

## 3. Best practices we adopt (architecture, naming, ontology)

### 3.1 Architecture

| Practice | Source | How we use it |
|----------|--------|----------------|
| **Path / namespace structure** | Vault (namespaces, mount paths); Okta (org/app hierarchy) | Layered scope: OneWish OS → systems → repos → logic → workflows → MCPs → core features (waterfall). config/repos.yaml (ROUTES, all_repos); config/canonical-mcp-connectors.yaml; docs/ as single doc tree. |
| **High availability / no single point of failure** | Okta architectural factors | Never-miss propagation (every target gets sync); no-fail Comprehensive Review; multiple dev tools (Cursor, Claude Code, Codex) can run same scripts. |
| **Validate every input; never assume success** | Okta reliability | run-all-verifications before summary; Phase 1 then Phase 2; eval after each run; commands-and-architecture review after each review. |
| **Modularize; document design** | Okta maintainability | Bite-size modular (GAME_CHANGERS); COMMANDS_AND_SCRIPTS_INDEX; ONEWISHOS_ARCHITECTURE_AND_METHODS; MASTER_INDEX. |
| **Zero Trust in design** | Okta, JumpCloud, Teleport | Verify connections and env; human checkpoint for privilege/production/damages; guardrails; no secrets in repo. |

### 3.2 Naming

| Practice | Source | How we use it |
|----------|--------|----------------|
| **Taxonomy by function/domain** | 1Password vaults; Vault path by team/app | 1PASSWORD_VAULT_ORGANIZATION (DevOps, CRM-Sales, Finance, Legal, Productivity, File-Storage, AI-LLM, Archive). platform-connections: applications, mcps, clis, llms, agents. |
| **Canonical list per category** | Vault mounts; Okta app catalog; Teleport resources | canonical-mcp-connectors.yaml (add here only); DEV_TOOLS_CANONICAL_LIST_AND_AUDIT (all 9 dev tools); COMMANDS_AND_SCRIPTS_INDEX (every script). |
| **Entity-scoped naming** | Vault entities; Okta users/groups; entity-account schemas | config/ontology/entity-account-master.yaml; entity, DBA, bank/credit/personal accounts, EIN/TIN, filings; naming by entity and timeline. |
| **Reserved names / prohibitions** | Vault (identity, sys, root, etc.) | We avoid reserved paths in config; document reserved keys in schema and ontology. |
| **Labels/tags for filtering** | Teleport (static/dynamic labels); Vault path segments | Vault names as tags (DevOps, Legal, etc.); repo and ROUTE names in config/repos.yaml; agent and workflow names in config. |

### 3.3 Ontology

| Practice | Source | How we use it |
|----------|--------|----------------|
| **Hierarchical namespaces** | Vault parent/child namespaces (e.g. A/B/C) | OneWish OS → NextTech OS → sub-OSes (GAME_CHANGERS; ONEWISHOS_CRYSTAL_CLEAR_ARCHITECTURE); entity → accounts → timeline. |
| **Self-service within guardrails** | Vault (team mounts); Okta (group admin) | Teams manage their vaults/collections per taxonomy; add MCP/connector only via canonical then sync; add script then add to COMMANDS_AND_SCRIPTS_INDEX. |
| **Audit and compliance in design** | Okta compliance; Vault audit devices; PAM session logs | chain-of-events; eval-after-run; full-review-summary; standards-compliance; ABA/EDRM/Sedona/ISO refs in constitution and my-agent.agent.md. |
| **Multi-entity isolation** | Vault namespaces; Okta orgs | Entity-account-master (entity, DBA, accounts); vaults per domain; ROUTES and all_repos per sub-OS / org. |

---

## 4. Where we implement these (our artifacts)

| Our artifact | Enterprise analogue | Principle / practice |
|--------------|---------------------|----------------------|
| **config/canonical-mcp-connectors.yaml** | Vault canonical mounts; Okta app catalog | Single source for MCPs/connectors; add here only; sync propagates. |
| **config/platform-connections.yaml** | Connector/identity store view | Applications, MCPs, CLIs, LLMs, agents; used by verify-all-connections and agent menu. |
| **config/repos.yaml** | Repo/tenant list; GitOps source of truth | ROUTES and all_repos; route-constitution and sync-all-repos use this. |
| **docs/1PASSWORD_VAULT_ORGANIZATION.md** | 1Password / Vault taxonomy | Vault taxonomy (DevOps, Legal, Finance, etc.); when to use which vault; rules for new credentials. |
| **config/ontology/entity-account-master.yaml** + **entity-account-master-file.schema.json** | Entity/account master; multi-entity naming | Entity, DBA, accounts (bank/credit/personal), EIN/TIN, filings, document repositories; naming by entity. |
| **docs/DEV_TOOLS_CANONICAL_LIST_AND_AUDIT.md** | Dev tool registry; no-fail audit | All 9 dev tools; same governance and entry points; never omit one. |
| **docs/COMMANDS_AND_SCRIPTS_INDEX.md** | Script/command registry | Every script in scripts/ listed by category; “organize in place” after each review. |
| **docs/NEVER_MISS_INSTRUCTIONS.md** | Runbook; exact sequence | sync → route → verify → review → commit → push; single point of truth = master repo. |
| **chain-of-events.jsonl / eval-after-run-latest.*** | Audit log; compliance trail | One event per run; outcome and metrics; persist after every review. |
| **run-commands-and-architecture-review.sh** | Post-change consistency check | After each review: commands organized; architecture reviewed per CS/repos/best practices. |

---

## 5. Taking their best practices into our architecture, naming, ontology

- **Architecture:** We already align to single source of truth, canonical lists, route-then-sync, fixed verification order, and no-fail review (ONEWISHOS_ARCHITECTURE_AND_METHODS). We **adopt** from Okta/Vault/Teleport: explicit availability/reliability wording in our architecture docs; “validate every input” in verification and eval steps; Zero Trust and least privilege called out in guardrails and constitution.
- **Naming:** We **adopt** from Vault/1Password/Teleport: (1) one canonical taxonomy per domain (we have it for vaults and platform-connections); (2) document reserved or prohibited names in each schema/ontology; (3) use labels/tags (vault names, repo names, agent names) consistently so filtering and RBAC-by-scope stay simple.
- **Ontology:** We **adopt** from Vault/Okta: (1) hierarchical structure (OneWish → NextTech → sub-OS; entity → accounts) documented in crystal-clear architecture and entity-account-master; (2) multi-entity isolation via entity-account schema and vault-by-domain; (3) audit and compliance baked in (chain-of-events, eval-after-run, standards-compliance) and referenced in SOURCES_AND_EMULATION_INDEX and REVIEW_AND_AUDIT_STAGES_IMPROVED.

**Cadence:** When we add a new connector, repo, vault, or entity type, we (1) add to the **canonical** list for that category, (2) run **sync/propagation** (route-constitution, sync-all-repos, or sync-canonical-mcp-connectors as applicable), (3) run **Full Review** and **commands-and-architecture review** so naming and ontology stay consistent and documented.

---

## 6. References

| Doc | Purpose |
|-----|--------|
| [ONEWISHOS_ARCHITECTURE_AND_METHODS.md](ONEWISHOS_ARCHITECTURE_AND_METHODS.md) | Our alignment to leading methods; single source of truth; canonical lists |
| [SOURCES_AND_EMULATION_INDEX.md](SOURCES_AND_EMULATION_INDEX.md) | Top sources to emulate per action; add enterprise IAM/secrets refs here when we adopt more |
| [1PASSWORD_VAULT_ORGANIZATION.md](1PASSWORD_VAULT_ORGANIZATION.md) | Our vault taxonomy; rules for new credentials; sync instructions |
| [PRODUCT_THAT_BUILDS_THE_PRODUCT_AND_ARCHITECTURE_TENET.md](PRODUCT_THAT_BUILDS_THE_PRODUCT_AND_ARCHITECTURE_TENET.md) | Architecture as core tenet; commands organized in place; architecture reviewed after each review |
| [config/ontology/entity-account-master.yaml](../config/ontology/entity-account-master.yaml) | Entity and account ontology; multi-entity naming |
| [NEVER_MISS_INSTRUCTIONS.md](NEVER_MISS_INSTRUCTIONS.md) | Exact sequence; single point of truth; when to use each script |

**External (examples):**
- Okta: [IAM overview / architectural factors](https://developer.okta.com/docs/concepts/iam-overview-architectural-factors) (availability, reliability, security, compliance, maintainability).
- HashiCorp Vault: [Namespace structure](https://developer.hashicorp.com/vault/docs/enterprise/namespaces/namespace-structure), [best practices for namespaces and mount paths](https://developer.hashicorp.com/vault/docs/enterprise/namespaces/namespace-structure).
- Teleport: [RBAC](https://goteleport.com/docs/zero-trust-access/rbac-get-started), [labels](https://goteleport.com/docs/ver/16.x/zero-trust-access/management/admin/labels).
- JumpCloud: Zero Trust, JIT/least privilege, [hardening cloud through least privilege](https://jumpcloud.com/blog/the-end-of-standing-access-hardening-cloud-infrastructure-through-least-privilege).

_Maintain at: docs/ENTERPRISE_IAM_SECRETS_ORCHESTRATION_TOOLS_AND_OUR_PRINCIPLES.md. Update when adding new enterprise tools or adopting new practices._
