# OneWish Omni Mac — Data Model, Commands, Workflows & Fail-Safe

**Purpose:** Define the **rules that command** (1) the **initial terminal command** for automated review, (2) **inventory, dedupe, and rename** of all Mac-controlled assets (passwords, apps, dev tools, contacts, documents, photos, accounts, emails, aliases, workflows, forward/send/groups), (3) the **data model, naming conventions, and defined terms** driving those workflows, and (4) **natural-language devops**: commands, actions, workflows, and syncs that run **behind the scenes in the cloud** unless the user is **specifically working in the dev terminal** (which is the current case when running from Cursor/Claude Code/Codex). **Fail-safe:** This sequence is never missed (trigger: quarterly; before commit when scope includes life/data domains).

**Governance:** Constitution §8, §8.5; [NEVER_MISS_INSTRUCTIONS.md](NEVER_MISS_INSTRUCTIONS.md) §4; [AUTOMATIC_CONSOLIDATION_NEXTTECH_OS.md](AUTOMATIC_CONSOLIDATION_NEXTTECH_OS.md); [EXPONENTIAL_LEARNING_AND_PREBUILT_DELIVERY.md](EXPONENTIAL_LEARNING_AND_PREBUILT_DELIVERY.md). Full Review mandatory checklist item #9 references this doc.

---

## 1. Initial terminal command (automated review entry point)

The **single initial terminal command** that kicks off the full automated review, inventory, and comprehensive eval is:

```bash
./scripts/run-omni-audit-and-never-miss.sh
```

Optional: `./scripts/run-omni-audit-and-never-miss.sh --connections-optional` to run connection verification in advisory mode.

**What it runs (in order):**

| Step | Script | What it does |
|------|--------|--------------|
| 1 | `connect-and-configure-onewishos.sh` | Route constitution → sync all repos → refresh workspace → (optional) verify-all-connections → Full Review |
| 2 | `run-comprehensive-eval-and-cleanup.sh --skip-full-review` | 1Password review (recommendations JSON) → connections verify (JSON) → aggregate MERGE/ARCHIVE/DELETE/FIX recommendations |

**When to run:** Quarterly; before commit when scope includes life/data domains (passwords, contacts, emails, documents, accounts); when adding or changing repos/MCPs/connectors; on demand. **Fail-safe:** Full Review mandatory checklist item #9 requires this sequence so the omni inventory and dedupe is never missed.

---

## 2. Automated review and inventory scope (everything controlled from a Mac)

Scope of **inventory, dedupe, and rename** is **everything controlled from a Mac** that OneWish OS now governs. Data model and workflows below are driven by this scope.

| Domain | What is inventoried, deduped, renamed | Doc / script |
|--------|---------------------------------------|--------------|
| **Passwords / 1Password** | Vault items, duplicates, vault moves, dedup extras; naming and vault taxonomy | [BROWSER_TABS_AND_1PASSWORD_IMPORT_PLAN.md](BROWSER_TABS_AND_1PASSWORD_IMPORT_PLAN.md); [1PASSWORD_VAULT_ORGANIZATION.md](1PASSWORD_VAULT_ORGANIZATION.md); `scripts/1password-organize-vaults.sh`, `scripts/1password-execute-changes.sh`, `scripts/audit-1password-for-integrations.sh` |
| **Apps** | Installed apps, MAC_APP_INTEGRATION_AUDIT; tiering by integration status | [MAC_APP_INTEGRATION_AUDIT.md](MAC_APP_INTEGRATION_AUDIT.md); [EXPONENTIAL_LEARNING_AND_PREBUILT_DELIVERY.md](EXPONENTIAL_LEARNING_AND_PREBUILT_DELIVERY.md) §2 |
| **Dev tools** | Cursor, Claude Code, Copilot, Codex, v0, VS Code, Windsurf, Warp, Goose; entry points, sync path | [DEV_TOOLS_CANONICAL_LIST_AND_AUDIT.md](DEV_TOOLS_CANONICAL_LIST_AND_AUDIT.md); no-fail audit §3 |
| **Contacts** | Mac, iCloud, Outlook, Zoom, Clay, LinkedIn, Folk, Attio; merge and dedupe into one master list | [CONTACTS_CLEANUP_AND_DEDUP_PLAN.md](CONTACTS_CLEANUP_AND_DEDUP_PLAN.md); script: `contacts-merge-and-dedup.py` |
| **Documents** | Repos, docs, playbooks, case matter content; dev files on Mac (audit, sort, dedup; never upload .env) | [MAC_DEV_FILES_AUDIT_AND_GITHUB.md](MAC_DEV_FILES_AUDIT_AND_GITHUB.md); [AUTOMATIC_CONSOLIDATION_NEXTTECH_OS.md](AUTOMATIC_CONSOLIDATION_NEXTTECH_OS.md) |
| **Photos** | Photo libraries and evidence assets; naming and folder hierarchy per ontology | [SOCIAL_POST_AND_PHOTO_DOCUMENT_EVIDENCE_WORKFLOWS.md](workflows/SOCIAL_POST_AND_PHOTO_DOCUMENT_EVIDENCE_WORKFLOWS.md); docs/modules/lexvault.md |
| **Accounts** | Entity, DBA, bank/credit/personal accounts, EIN/TIN, filings, document repositories | [entity-account-master-file.schema.json](schemas/entity-account-master-file.schema.json); config/ontology/entity-account-master.yaml; [CONSOLIDATION_AND_REPO_STATUS.md](CONSOLIDATION_AND_REPO_STATUS.md) |
| **Emails** | Email accounts, aliases, workflows, forward/send/groups; inbox/thread exports per connector | [MESSAGING_EMAIL_SENTIMENT_TIMELINE_WORKFLOW.md](workflows/MESSAGING_EMAIL_SENTIMENT_TIMELINE_WORKFLOW.md); [AUTOMATIC_CONSOLIDATION_NEXTTECH_OS.md](AUTOMATIC_CONSOLIDATION_NEXTTECH_OS.md) §2; archives: RB-001-domain-email-migration |
| **Repos / GitHub** | Repo list, merge/archive recommendations, single-account + dev-tools alignment | [GITHUB_CONSOLIDATION_AND_DEVTOOLS_OPTIMIZATION_PLAN.md](GITHUB_CONSOLIDATION_AND_DEVTOOLS_OPTIMIZATION_PLAN.md); [CONSOLIDATION_AND_REPO_STATUS.md](CONSOLIDATION_AND_REPO_STATUS.md) |
| **CRM / financial** | NDD, Monday, Proforma, Zoho, HubSpot, Excel, financial/damage model, entity consolidation | [CRM_AND_FINANCIAL_CONSOLIDATION_MASTER_PLAN.md](CRM_AND_FINANCIAL_CONSOLIDATION_MASTER_PLAN.md) |

**Naming and rename:** Use **data model and defined terms** (§3) for consistent naming across 1Password items, vaults, contact lists, document folders, account labels, and email aliases/workflows. Dedupe and rename actions follow docs and scripts above; no destructive execution without approval (dry-run first).

---

## 3. Data model, naming conventions, defined terms

The **final data model** driving inventory, dedupe, and rename is expanded from the aforementioned domains and aligned with:

| Concept | Definition / convention | Where defined |
|---------|-------------------------|---------------|
| **Entity** | Legal or operational entity (person, org, DBA); one canonical name per entity | config/ontology/entity-account-master.yaml; docs/schemas/entity-account-master-file.schema.json |
| **Account** | Login, API, or service account; naming: `{ServiceOrApp}_{Purpose}` or 1Password item title per vault taxonomy | docs/1PASSWORD_VAULT_ORGANIZATION.md; PLATFORMS_1PASSWORD_MAPPING.md |
| **Vault** | 1Password vault; taxonomy: DevOps, Executive, Employee, Finance, Legal, etc. | docs/1PASSWORD_VAULT_ORGANIZATION.md; scripts/1password-organize-vaults.sh |
| **Contact** | Unified contact record; one master list; dedupe by email/phone/canonical id | CONTACTS_CLEANUP_AND_DEDUP_PLAN.md |
| **Workflow** | Predefined process (sync, route, eval, dedupe); trigger + scope + destination | AUTOMATIC_CONSOLIDATION_NEXTTECH_OS.md §3; config/workflows-*.yaml |
| **Email identity** | Email account, alias, send-as, group, forward rule; named per role or domain | MESSAGING_EMAIL_SENTIMENT_TIMELINE_WORKFLOW; RB-001-domain-email-migration (archives) |
| **Document / evidence** | File or artifact; naming per LexVault and module ontology; no .env in version control | docs/modules/lexvault.md; MAC_DEV_FILES_AUDIT_AND_GITHUB.md |
| **Repo (canonical)** | Master, ROUTES, all_repos; single source config/repos.yaml | CONSOLIDATION_AND_REPO_STATUS.md; config/repos.yaml |

**Defined terms** for natural language commands (§4) use the same vocabulary so that "inventory 1Password," "dedupe contacts," "rename vault items," and "sync email workflows" map to the scripts and docs above.

---

## 4. Natural language devops: commands, actions, workflows, syncs

**Game changer:** Natural language devops commands, actions, workflows, and syncs that run **behind the scenes in the cloud** (or on a schedule) unless the user is **specifically working in the dev terminal** (e.g. Cursor, Claude Code, Codex). When in dev terminal, the user runs the initial command or individual scripts explicitly.

| Intent (natural language) | Command / action | Where it runs |
|---------------------------|------------------|---------------|
| **Run full automated review** | `./scripts/run-omni-audit-and-never-miss.sh` | Dev terminal (initial command); or CI/cron in cloud |
| **Route and sync everything** | `./scripts/connect-and-configure-onewishos.sh` | Dev terminal or cloud |
| **Inventory and dedupe passwords** | 1Password review → 1password-recommendations.json → approve → 1password-execute-changes.sh | Dev terminal (review/approve); execute can be cloud after approval |
| **Inventory and dedupe contacts** | CONTACTS_CLEANUP_AND_DEDUP_PLAN; contacts-merge-and-dedup.py | Dev terminal or scheduled job |
| **Rename and organize vaults** | 1password-organize-vaults.sh; vault taxonomy in 1PASSWORD_VAULT_ORGANIZATION | Dev terminal or cloud (with dry-run first) |
| **Sync all repos and review** | `./scripts/sync-all-repos-and-review.sh` | Dev terminal or cloud |
| **Full Review** | `./scripts/run-full-review.sh` | Dev terminal or cloud |
| **Comprehensive eval (1P + connections + MERGE/ARCHIVE/DELETE/FIX)** | `./scripts/run-comprehensive-eval-and-cleanup.sh` | Dev terminal or cloud |

**Behind the scenes in the cloud:** Triggers (e.g. quarterly, on push to main) can run the same scripts via CI (e.g. GitHub Actions) or cron so that inventory, dedupe, and sync run without the user in the dev terminal. **When specifically in dev terminal:** User runs `run-omni-audit-and-never-miss.sh` or the steps in NEVER_MISS_INSTRUCTIONS manually. Commands and workflows use the **data model and defined terms** (§3) so naming and scope stay consistent across dev terminal and cloud.

---

## 5. Fail-safe: never miss omni inventory and dedupe

To ensure the comprehensive inventory, dedupe, and rename is **never missed** across all OneWish OS:

| Mechanism | What it does |
|-----------|--------------|
| **Full Review mandatory checklist item #9** | Requires running the omni inventory/dedupe sequence per this doc; trigger: quarterly; before commit when scope includes life/data domains. See docs/audits/full-review-summary.md (generated by run-full-review.sh). |
| **Initial terminal command** | `./scripts/run-omni-audit-and-never-miss.sh` is the single entry point; documented in NEVER_MISS_INSTRUCTIONS §4 and in this doc §1. |
| **NEVER_MISS_INSTRUCTIONS §4** | References this doc for fail-safe and omni scope; checklist item #9 points here. |
| **Quarterly and pre-commit** | Run `run-omni-audit-and-never-miss.sh` quarterly and before commit when changes touch passwords, contacts, emails, documents, accounts, or apps. |

**Checklist (omni inventory and dedupe):**

- [ ] Run `./scripts/run-omni-audit-and-never-miss.sh`.
- [ ] Complete Full Review mandatory checklist (including item #9).
- [ ] Review docs/audits/comprehensive-eval-and-cleanup-recommendations.md (MERGE/ARCHIVE/DELETE/FIX).
- [ ] Apply 1Password recommendations (review 1password-recommendations.json → edit to 1password-approved.json → dry-run → execute per 1PASSWORD_VAULT_ORGANIZATION and 1PASSWORD_EXECUTE_AND_NOTIFY).
- [ ] When scope includes contacts/emails/documents: run CONTACTS_CLEANUP_AND_DEDUP_PLAN and MAC_DEV_FILES_AUDIT_AND_GITHUB (and related workflows) per their docs.

---

## 6. Cross-references

| Doc | Purpose |
|-----|--------|
| [NEVER_MISS_INSTRUCTIONS.md](NEVER_MISS_INSTRUCTIONS.md) | Sequence, single source of truth, fail-safe reference to this doc |
| [AUTOMATIC_CONSOLIDATION_NEXTTECH_OS.md](AUTOMATIC_CONSOLIDATION_NEXTTECH_OS.md) | Consolidation by function and class; predefined workflows |
| [EXPONENTIAL_LEARNING_AND_PREBUILT_DELIVERY.md](EXPONENTIAL_LEARNING_AND_PREBUILT_DELIVERY.md) | Omni-channel Mac review; apps, content, tiering |
| [BROWSER_TABS_AND_1PASSWORD_IMPORT_PLAN.md](BROWSER_TABS_AND_1PASSWORD_IMPORT_PLAN.md) | Passwords consolidation; dedup and archive |
| [CONTACTS_CLEANUP_AND_DEDUP_PLAN.md](CONTACTS_CLEANUP_AND_DEDUP_PLAN.md) | Contacts merge and dedupe |
| [MAC_DEV_FILES_AUDIT_AND_GITHUB.md](MAC_DEV_FILES_AUDIT_AND_GITHUB.md) | Mac dev files; audit and optional GitHub stage |
| [1PASSWORD_VAULT_ORGANIZATION.md](1PASSWORD_VAULT_ORGANIZATION.md) | Vault taxonomy; organize and rename |
| [audits/comprehensive-eval-and-cleanup-recommendations.md](audits/comprehensive-eval-and-cleanup-recommendations.md) | MERGE/ARCHIVE/DELETE/FIX output |

_Maintain at: docs/ONEWISH_OMNI_MAC_DATA_MODEL_AND_COMMANDS.md. Update when adding domains, scripts, or triggers._
