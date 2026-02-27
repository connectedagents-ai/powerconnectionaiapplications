# All-Repo Review Protocol

> **Purpose**: Comprehensive review of architecture, workflows, actions, automations, constitutions, multi-agent/tool/MCP, and super developer principles across all codebases.
>
> **Run via**: `scripts/sync-all-repos-and-review.sh`
>
> **Cadence**: Run immediately on setup; then weekly or when adding repos.

---

## 1. Scope (Repos Included)

| Repo                          | Path                                                                     | Source    |
| ----------------------------- | ------------------------------------------------------------------------ | --------- |
| CURSOR CLOUD AGENTS (master)  | This repo                                                                | Canonical |
| connected-agents-platform     | ~/Documents/connected-agents-platform                                    | ROUTES    |
| LitigationForce.AI            | ~/Documents/LitigationForce-Parent/01-Litigation-Core/LitigationForce.AI | ROUTES    |
| file-management-toolkit       | ~/file-management-toolkit                                                | ROUTES    |
| slack-agent-template          | ~/.cursor/bootstrap-work/slack-agent-template                            | Bootstrap |
| powerconnectionaiapplications | ~/Documents/powerconnectionaiapplications                                | ROUTES    |

Add repos to `scripts/sync-all-repos-and-review.sh` ALL_REPOS and `route-constitution-to-repos.sh` ROUTES when new first-class repos are created.

---

## 2. Review Checklist (Per Repo)

### Architecture

- [ ] Architecture doc exists and is current
- [ ] Data contracts (schemas) defined
- [ ] Integration points documented
- [ ] References `docs/architecture.md` or equivalent

### Workflows

- [ ] `.github/workflows/` reviewed; no broken or orphaned workflows
- [ ] Actions use current patterns (e.g., checkout v4)
- [ ] Secrets referenced (not hardcoded)
- [ ] Triggers appropriate (push, PR, schedule)

### Actions & Automations

- [ ] GitHub Actions, pre-commit hooks, scripts documented
- [ ] Route constitution / sync scripts in ROUTES
- [ ] Verify-routing, verify-connections run
- [ ] No redundant or conflicting automations

### Constitution & Governance

- [ ] `docs/constitution.md` (or `agents/constitution.md`) present
- [ ] `NEW_CAPABILITY_CHECKLIST.md` present
- [ ] `UNIVERSAL_INSTRUCTIONS.md` present
- [ ] AGENTS.md / CLAUDE.md have READ FIRST block
- [ ] References CONSOLIDATION_AND_REPO_STATUS

### Multi-Agent / Tool / MCP

- [ ] MCP config current; router-first if applicable
- [ ] Agent specs (AGENTS.md, workers) align with architecture
- [ ] Tool registry or connector config current
- [ ] No stale or duplicate MCP entries

### Super Developer Principles

- [ ] `docs/SUPER_DEVELOPER_PRINCIPLES.md` present (or linked from master)
- [ ] `docs/SOURCES_REVIEWED.md` present (repos/LLMs reviewed; full review confirmed)
- [ ] Rules: agent-efficiency-context, guardrails-beginner, constant-improvement
- [ ] Skills: efficient-context-management, beginner-guardrails, recursive-improvement, constant-improvement
- [ ] lessons.md, patterns-that-work.md exist
- [ ] CLAUDE.md present (Claude Code context)
- [ ] docs/SUPER_DEVELOPER_PRE_EXECUTION_CHECKLIST.md present
- [ ] Skills referenced exist (run verify-skills.sh)

---

## 3. Super Developer Principles Review

During each all-repo review:

1. **Read** `docs/SUPER_DEVELOPER_PRINCIPLES.md`
2. **For each principle**: Is it still accurate? Implemented? Any gaps?
3. **Update** principles with additions, removals, refinements
4. **Sync** updates to architecture.md, AGENTS.md, routed docs
5. **Commit** changes

---

## 4. Output (Review Report)

After `sync-all-repos-and-review.sh` runs:

- Sync status per repo (success / skipped / error)
- Review checklist summary (optional; run with `--review` for full checklist)
- Suggested updates to SUPER_DEVELOPER_PRINCIPLES (if run with `--review`)

---

## 5. Consolidation Alignment

Ensure alignment with `docs/CONSOLIDATION_AND_REPO_STATUS.md`:

- [ ] ROUTES match route-constitution-to-repos.sh
- [ ] Canonical repo map current
- [ ] Merged/archived status correct
- [ ] New repo checklist followed for any new additions

---

## 6. Document Reference

| Doc                                   | Purpose                                               |
| ------------------------------------- | ----------------------------------------------------- |
| docs/architecture.md                  | System design; references SUPER_DEVELOPER_PRINCIPLES  |
| docs/SUPER_DEVELOPER_PRINCIPLES.md    | Canonical principles; reviewed during all-repo review |
| docs/SOURCES_REVIEWED.md              | Repos/LLMs reviewed; full review confirmed            |
| docs/ALL_REPO_REVIEW.md               | This protocol                                         |
| docs/CONSOLIDATION_AND_REPO_STATUS.md | Repo map, routing                                     |
| scripts/sync-all-repos-and-review.sh  | Execution script                                      |

---

_Maintain at: docs/ALL_REPO_REVIEW.md_
