# Lifecycle Stages & Checkpoints — When to Run Super Developer Checklist

> **Purpose**: Define at which stages the Super Developer checklist applies and how architecture, workflows, automations, and debugging are managed at each stage.
>
> **Referenced by**: SUPER_DEVELOPER_PRE_EXECUTION_CHECKLIST, SOURCES_AND_EMULATION_INDEX, sync-all-repos-and-review.sh

---

## Stage Overview

| Stage                 | When                         | Checklist Focus                                   | Triggers                 |
| --------------------- | ---------------------------- | ------------------------------------------------- | ------------------------ |
| 1. Planning / Design  | Before picking up work       | Governance, Architecture, Sources, Scope          | New task, new capability |
| 2. Pre-Execution      | Before each action           | All 22 categories (weighted)                      | Every significant action |
| 3. During Execution   | Mid-task boundaries          | Efficiency, Tools, Human-in-loop                  | Subtask boundaries       |
| 4. Post-Execution     | After each action            | Verification, Testing, Improvement, Observability | Action complete          |
| 5. Review / Handoff   | Before PR, before delivery   | Docs, Compliance, Human                           | PR, delivery             |
| 6. Failure / Incident | When something breaks        | Postmortem, Observability, Rollback               | Error, incident          |
| 7. Recurring Cadence  | Weekly / Monthly / Quarterly | Cost, Sources, SOURCES_REVIEWED                   | Calendar, sync           |

---

## Per-Stage: Architecture, Workflows, Automations, Debugging

### Stage 1: Planning / Design

| Dimension        | How Managed                                                                          | Sources                                    |
| ---------------- | ------------------------------------------------------------------------------------ | ------------------------------------------ |
| **Architecture** | Confirm schema-first; one evidence base; router-first MCP; config in connectors.yaml | docs/architecture.md, docs/modules/        |
| **Workflows**    | Select playbook from config/playbooks.yaml; decide delegation                        | playbooks/, master-orchestrator            |
| **Automations**  | Check existing hooks (pre-commit, pre-push), workflows, scheduled jobs               | .githooks/, .github/workflows/             |
| **Debugging**    | Plan baseline; ensure traceable flow; define observability                           | RECURSIVE_IMPROVEMENT "Eval Before Change" |

**Checklist items**: 1.1–1.6 (governance), 4.1–4.4 (sources), 6.1–6.5 (architecture), 21.1–21.5 (scope)

---

### Stage 2: Pre-Execution

| Dimension        | How Managed                                                 | Sources                                    |
| ---------------- | ----------------------------------------------------------- | ------------------------------------------ |
| **Architecture** | Per-check alignment with schema-first, MCP, config          | SUPER_DEVELOPER_PRE_EXECUTION_CHECKLIST §6 |
| **Workflows**    | Per-check: playbook exists? delegate? Evaluator gate?       | SUPER_DEVELOPER_PRE_EXECUTION_CHECKLIST §8 |
| **Automations**  | Use --dry-run for sync/routing; prefer idempotent scripts   | route-constitution, sync-all-repos         |
| **Debugging**    | Audit trail sufficient (constitution §3); actionable errors | checklist §20                              |

**Checklist items**: All 22 categories; execution order: critical → emulation → platform → improvement → verify

---

### Stage 3: During Execution

| Dimension        | How Managed                                                         | Sources                            |
| ---------------- | ------------------------------------------------------------------- | ---------------------------------- |
| **Architecture** | No mid-flow redesign; stay within current schema and data contracts | GUARDRAILS                         |
| **Workflows**    | One task per step; pause for human approval on high-stakes          | constitution §1, my-agent.agent.md |
| **Automations**  | Do not add automations mid-run; finish current flow                 | AGENTS_EFFICIENCY                  |
| **Debugging**    | Structured logging; clear failures; no silent drops                 | checklist §20, security.md         |

**Checklist items**: 3.1–3.8 (efficiency), 7.1–7.5 (tools), 22.1–22.5 (human-in-loop)

---

### Stage 4: Post-Execution

| Dimension        | How Managed                                                    | Sources                       |
| ---------------- | -------------------------------------------------------------- | ----------------------------- |
| **Architecture** | Verify output matches schemas; compare to intended design      | validate_schemas.sh, evals.md |
| **Workflows**    | Run verify-routing, sync if governance changed                 | sync-all-repos-and-review.sh  |
| **Automations**  | Decide: new automation vs one-off; add to sync/route if needed | NEW_CAPABILITY_CHECKLIST      |
| **Debugging**    | Verify logs, trace, audit trail; run validation scripts        | run-all-verifications.sh      |

**Checklist items**: 10.1–10.6 (improvement), 13.1–13.5 (verification), 15.1–15.5 (testing), 17.1–17.5 (idempotency), 20.1–20.5 (observability)

---

### Stage 5: Review / Handoff

| Dimension        | How Managed                                                  | Sources                                   |
| ---------------- | ------------------------------------------------------------ | ----------------------------------------- |
| **Architecture** | Update architecture docs; capture decisions in ADRs          | docs/architecture.md                      |
| **Workflows**    | CROSS_PLATFORM_UPDATE_CHECKLIST; ALL_REPO_REVIEW             | docs/ALL_REPO_REVIEW.md                   |
| **Automations**  | Pre-push triggers routing verify; CI runs full verifications | .githooks/pre-push, run-all-verifications |
| **Debugging**    | Ensure postmortem path documented; error handling reviewed   | RECURSIVE_IMPROVEMENT                     |

**Checklist items**: 19.1–19.5 (docs), 12.1–12.5 (compliance), 22.1–22.5 (human)

---

### Stage 6: Failure / Incident

| Dimension        | How Managed                                                  | Sources                            |
| ---------------- | ------------------------------------------------------------ | ---------------------------------- |
| **Architecture** | Document architecture-related causes in postmortem           | postmortem-{date}.md template      |
| **Workflows**    | Postmortem → anti-pattern; update playbooks if needed        | RECURSIVE_IMPROVEMENT              |
| **Automations**  | Add automation to prevent recurrence; document in postmortem | SOURCES_AND_EMULATION_INDEX        |
| **Debugging**    | Full trace; root-cause analysis; update observability        | RECURSIVE_IMPROVEMENT, security.md |

**Checklist items**: 10.2 (postmortem), 17.1–17.5 (rollback), 20.1–20.5 (observability)

---

### Stage 7: Recurring Cadence

| Dimension        | How Managed                                                                     | Sources                      |
| ---------------- | ------------------------------------------------------------------------------- | ---------------------------- |
| **Architecture** | Architecture review; schema evolution; align with reference patterns            | Quarterly                    |
| **Workflows**    | Sync; lessons consolidation; playbook updates from lessons                      | sync-all-repos-and-review.sh |
| **Automations**  | sync-all-repos-and-review.sh; route-constitution; verify-skills; scheduled jobs | scripts/                     |
| **Debugging**    | Review error patterns; improve logging; update runbooks                         | SOURCES_REVIEWED, lessons.md |

**Cadence**:

- **After prompt**: 1-line capture (pattern or postmortem)
- **Weekly**: Consolidate lessons; sync instructions
- **Monthly**: Research 1 topic; multi-agent review 2 rules
- **Quarterly**: Full audit; refresh SOURCES_REVIEWED; re-review expert docs

---

## Automation Triggers by Stage

| Stage     | Script / Trigger                      | Purpose           |
| --------- | ------------------------------------- | ----------------- |
| Planning  | None (manual)                         | Design decisions  |
| Pre-Exec  | verify-routing, --dry-run             | Pre-flight        |
| Post-Exec | run-all-verifications.sh              | Full verification |
| Review    | pre-push, CI                          | Block bad commits |
| Failure   | postmortem template                   | Capture lessons   |
| Cadence   | sync-all-repos-and-review.sh --review | Weekly sync       |

---

_Maintain at: docs/LIFECYCLE_STAGES_AND_CHECKPOINTS.md_
