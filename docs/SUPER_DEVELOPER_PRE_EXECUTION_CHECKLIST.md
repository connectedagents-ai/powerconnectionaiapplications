# Super Developer Pre-Execution Checklist — All Checks Before Acting

> **Purpose**: Comprehensive list of checks, principles, and rules a super developer employs before executing any action—big or small. Run through this mentally or explicitly before significant work.

**Referenced by**: constitution, UNIVERSAL_INSTRUCTIONS, AGENTS.md, SOURCES_AND_EMULATION_INDEX

**Scope**: 22 categories, 110+ checks (governance, safety, efficiency, sources, repo, architecture, tools, agent, prompt, improvement, skills, compliance, verification, cost, testing, security, idempotency, dependencies, docs, observability, scope, human-in-loop)

---

## 1. Governance & Constitution

| #   | Check                                                         | Source          | Before                        |
| --- | ------------------------------------------------------------- | --------------- | ----------------------------- |
| 1.1 | Is this high-stakes? (privilege, filing, production, damages) | constitution §1 | Human checkpoint required     |
| 1.2 | Do I need claim typing? (FACT/INFERENCE/OPINION/LEGAL)        | constitution §2 | Every assertion               |
| 1.3 | Will I preserve audit trail? (prompts, tool calls, outputs)   | constitution §3 | Every transformation          |
| 1.4 | Have I considered bias and safety?                            | constitution §4 | Sensitive inferences          |
| 1.5 | Does output need simulation disclaimer?                       | constitution §5 | Legal/litigation context      |
| 1.6 | Is this a new capability? (tool, agent, skill)                | constitution §6 | Full NEW_CAPABILITY_CHECKLIST |

---

## 2. Safety & Guardrails

| #   | Check                                                     | Source        | Before                  |
| --- | --------------------------------------------------------- | ------------- | ----------------------- |
| 2.1 | Is this destructive? (rm -rf, force push, overwrite prod) | GUARDRAILS    | Confirm with user       |
| 2.2 | Will I commit secrets?                                    | Pre-commit    | Never—.env.example only |
| 2.3 | Have I read the target file before editing?               | GUARDRAILS    | Validate patterns       |
| 2.4 | Is output format valid? (JSON, YAML, etc.)                | GUARDRAILS    | Check schema            |
| 2.5 | Am I overwriting user data without backup?                | Best practice | Copy first or confirm   |

---

## 3. Efficiency & Context

| #   | Check                                              | Source               | Before                 |
| --- | -------------------------------------------------- | -------------------- | ---------------------- |
| 3.1 | Am I announcing instead of executing?              | AGENTS_EFFICIENCY    | Execute immediately    |
| 3.2 | Do I have multiple tasks in one message?           | AGENTS_EFFICIENCY    | Split; one task only   |
| 3.3 | Have I specified output path?                      | AGENTS_EFFICIENCY    | Persist to disk        |
| 3.4 | Will I persist immediately after producing?        | Persistence protocol | No holding in context  |
| 3.5 | Am I in a verification loop?                       | AGENTS_EFFICIENCY    | Verify once, move on   |
| 3.6 | Is my API/MCP query too broad?                     | AGENTS_EFFICIENCY    | Paginate; limit fields |
| 3.7 | Can I reuse data already on disk?                  | Self-correction      | Read file vs re-fetch  |
| 3.8 | Is my plan inefficient? (4+ tasks, no output path) | Self-correction      | Refactor first         |

---

## 4. Sources & Emulation

| #   | Check                                                                                 | Source                      | Before                  |
| --- | ------------------------------------------------------------------------------------- | --------------------------- | ----------------------- |
| 4.1 | Have I checked SOURCES_AND_EMULATION_INDEX for this action type?                      | SOURCES_AND_EMULATION_INDEX | Any significant action  |
| 4.2 | Am I emulating reference patterns? (LexVault for file/evidence, ontology for schemas) | REFERENCE_PATTERNS          | New file/entity systems |
| 4.3 | Do I know which canonical files govern this?                                          | CONSTITUTION_ROUTING_DESIGN | Cross-repo work         |
| 4.4 | Have I read lessons.md and patterns-that-work?                                        | RECURSIVE_IMPROVEMENT       | Session start           |

---

## 5. Repo & Platform

| #   | Check                                                            | Source                          | Before                   |
| --- | ---------------------------------------------------------------- | ------------------------------- | ------------------------ |
| 5.1 | Am I using the canonical repo?                                   | CONSOLIDATION_AND_REPO_STATUS   | No archived/merged repos |
| 5.2 | Is this repo in ROUTES / ALL_REPOS?                              | route-constitution, sync script | New repo additions       |
| 5.3 | Do I need to update indexes? (cross-system-index, CONSOLIDATION) | NEW_CAPABILITY_CHECKLIST        | New repo/agent/skill     |
| 5.4 | Does the child repo have AGENTS.md, CLAUDE.md?                   | CROSS_PLATFORM_UPDATE_CHECKLIST | Agent context            |
| 5.5 | Have I run sync after governance changes?                        | sync-all-repos-and-review       | Propagation              |

---

## 6. Architecture & Design

| #   | Check                                                         | Source       | Before             |
| --- | ------------------------------------------------------------- | ------------ | ------------------ |
| 6.1 | Does this align with schema-first? (docs/schemas/, examples/) | architecture | Data contracts     |
| 6.2 | Am I using router-first MCP? (progressive discovery)          | mcp-router   | Tool-heavy work    |
| 6.3 | Is there one evidence base for multi-track?                   | architecture | Litigation outputs |
| 6.4 | Do I need Evaluator Swarm gate?                               | constitution | Pre-human output   |
| 6.5 | Does config exist for this? (connectors, playbooks)           | config/      | Before hardcoding  |

---

## 7. Tool Calls & MCP

| #   | Check                                   | Source                     | Before                |
| --- | --------------------------------------- | -------------------------- | --------------------- |
| 7.1 | One tool per step?                      | SUPER_DEVELOPER_PRINCIPLES | Coordination          |
| 7.2 | Paginating? (limit 10–25)               | AGENTS_EFFICIENCY          | Large datasets        |
| 7.3 | Using minimal fields?                   | API efficiency             | Reduce payload        |
| 7.4 | Persisting between tool steps?          | Orchestration              | No cross-tool context |
| 7.5 | Have I fetched schema only when needed? | mcp-router                 | Progressive discovery |

---

## 8. Agent & Orchestration

| #   | Check                                        | Source                | Before                     |
| --- | -------------------------------------------- | --------------------- | -------------------------- |
| 8.1 | Should I delegate to specialist agent?       | master-orchestrator   | Complex tasks              |
| 8.2 | Does a playbook exist for this?              | config/playbooks.yaml | Before ad-hoc              |
| 8.3 | Am I blocking high-stakes without approval?  | my-agent.agent.md     | Orchestrator role          |
| 8.4 | Do I need Evaluator Swarm before delivery?   | constitution          | Fact/Citation/Logic/Ethics |
| 8.5 | Is there a skill for this? (.cursor/skills/) | create-skill          | Use or create              |

---

## 9. Prompt & LLM Best Practices

| #   | Check                                                    | Source                   | Before                                |
| --- | -------------------------------------------------------- | ------------------------ | ------------------------------------- |
| 9.1 | Instructions at start? Delimiters (###, """)?            | OpenAI, SOURCES_REVIEWED | Prompt structure                      |
| 9.2 | Am I specific? (context, outcome, format)                | OpenAI, Google           | No vague goals                        |
| 9.3 | Output format via examples?                              | OpenAI                   | Show, don't tell                      |
| 9.4 | GOLDEN applied? (Goal, Output, Limits, Data, Eval, Next) | promptbuilder.cc         | Complex prompts                       |
| 9.5 | Explore → Plan → Code?                                   | Anthropic                | Separate research from implementation |
| 9.6 | Self-verification path? (tests, expected output)         | Anthropic                | Before delivery                       |
| 9.7 | Course-correct early if diverging?                       | Anthropic                | Redirect immediately                  |

---

## 10. Recursive Improvement

| #    | Check                                             | Source                 | Before             |
| ---- | ------------------------------------------------- | ---------------------- | ------------------ |
| 10.1 | Have I noted baseline before change?              | RECURSIVE_IMPROVEMENT  | Eval before change |
| 10.2 | Will I capture failure as postmortem?             | RECURSIVE_IMPROVEMENT  | On failure         |
| 10.3 | Will I append success to patterns-that-work?      | RECURSIVE_IMPROVEMENT  | On success         |
| 10.4 | Will I append session to lessons.md?              | RECURSIVE_IMPROVEMENT  | Session end        |
| 10.5 | Did I notice waste? Add to anti-pattern?          | AGENTS_EFFICIENCY      | Before continuing  |
| 10.6 | After prompt: 1-line capture only? (no heavy ops) | CONTINUOUS_IMPROVEMENT | Cost guardrail     |

---

## 11. Skills & Ontology

| #    | Check                                               | Source                   | Before              |
| ---- | --------------------------------------------------- | ------------------------ | ------------------- |
| 11.1 | Do I need ontology-schema-syntax? (schemas, naming) | NEW_CAPABILITY_CHECKLIST | Schema work         |
| 11.2 | Do I need lists-todos-projects?                     | NEW_CAPABILITY_CHECKLIST | Task lists          |
| 11.3 | Do I need names-and-connections?                    | NEW_CAPABILITY_CHECKLIST | Entity names        |
| 11.4 | Does a skill exist for this? Check .cursor/skills/  | create-skill             | Before reinventing  |
| 11.5 | Should I create a skill? (new capability)           | NEW_CAPABILITY_CHECKLIST | Per constitution §6 |
| 11.6 | Are referenced skills present?                      | verify-skills.sh         | Dead references     |

---

## 12. Compliance & Standards

| #    | Check                                     | Source               | Before             |
| ---- | ----------------------------------------- | -------------------- | ------------------ |
| 12.1 | ABA Model Rule 1.1 (tech competence)?     | standards-compliance | Attorney oversight |
| 12.2 | EDRM alignment? (TAR, transparency)       | standards-compliance | Discovery          |
| 12.3 | Sedona 2023 AI (transparency, oversight)? | standards-compliance | AI outputs         |
| 12.4 | ISO/IEC 42001? (governance, risk)         | standards-compliance | AI management      |
| 12.5 | GDPR/CCPA if handling PII?                | standards-compliance | Data handling      |

---

## 13. Connection & Verification

| #    | Check                                         | Source                  | Before            |
| ---- | --------------------------------------------- | ----------------------- | ----------------- |
| 13.1 | Have I run verify-routing?                    | verify-routing.sh       | Constitution refs |
| 13.2 | Are connections configured? (connectors.yaml) | platform-connections    | External APIs     |
| 13.3 | Is env documented in .env.example?            | verify-env-example-sync | Required vars     |
| 13.4 | Do schemas validate? (validate_schemas.sh)    | docs/schemas            | Data contracts    |
| 13.5 | Pre-commit passed? (no secrets)               | pre-commit-check        | Before commit     |

---

## 14. Cost & Time Guardrails

| #    | Check                                    | Source                 | Before           |
| ---- | ---------------------------------------- | ---------------------- | ---------------- |
| 14.1 | Is improvement <10% of total?            | CONTINUOUS_IMPROVEMENT | Cost guardrail   |
| 14.2 | Am I doing heavy ops after every prompt? | CONTINUOUS_IMPROVEMENT | One-line only    |
| 14.3 | Weekly cadence for consolidation?        | CONTINUOUS_IMPROVEMENT | Sync, lessons    |
| 14.4 | Monthly for research/review?             | CONTINUOUS_IMPROVEMENT | SOURCES_REVIEWED |
| 14.5 | Quarterly for full audit?                | CONTINUOUS_IMPROVEMENT | Refresh docs     |

---

## 15. Testing & Validation

| #    | Check                                             | Source                | Before            |
| ---- | ------------------------------------------------- | --------------------- | ----------------- |
| 15.1 | Have I run the eval harness for changed logic?    | evals.md              | Logic changes     |
| 15.2 | Do golden/regression tests exist?                 | evals.md              | Output changes    |
| 15.3 | Am I testing edge cases? (empty, null, malformed) | Best practice         | Data handling     |
| 15.4 | Can I verify output without full re-run?          | evals                 | Spot checks       |
| 15.5 | Did I baseline before change?                     | RECURSIVE_IMPROVEMENT | Eval before/after |

---

## 16. Security & Input Handling

| #    | Check                                             | Source                 | Before             |
| ---- | ------------------------------------------------- | ---------------------- | ------------------ |
| 16.1 | Am I sanitizing/escaping user input?              | OWASP                  | User-provided data |
| 16.2 | Am I preventing injection? (SQL, shell, template) | security.md            | Dynamic queries    |
| 16.3 | Are secrets only in env/1Password, never in code? | pre-commit, GUARDRAILS | Every secret       |
| 16.4 | Have I checked RBAC for this action?              | security.md            | Multi-user systems |
| 16.5 | Is PII/privilege handled per policy?              | constitution §4        | Sensitive data     |

---

## 17. Idempotency & Rollback

| #    | Check                                    | Source        | Before              |
| ---- | ---------------------------------------- | ------------- | ------------------- |
| 17.1 | Is this operation safe to retry?         | Best practice | Writes, deploys     |
| 17.2 | Can I undo this? (backup, rollback path) | GUARDRAILS    | Destructive changes |
| 17.3 | Did I use --dry-run first?               | sync scripts  | Routing, sync       |
| 17.4 | Am I preventing duplicate writes?        | Idempotency   | Batch operations    |
| 17.5 | Do I have a rollback checklist?          | ops runbook   | Production changes  |

---

## 18. Dependencies & Versioning

| #    | Check                                              | Source        | Before           |
| ---- | -------------------------------------------------- | ------------- | ---------------- |
| 18.1 | Are dependencies pinned? (lockfile, version range) | Best practice | New deps         |
| 18.2 | Have I checked for known CVEs?                     | security      | Before merge     |
| 18.3 | Is license compatible?                             | Compliance    | Third-party code |
| 18.4 | Am I breaking backward compatibility?              | Semver        | API changes      |
| 18.5 | Is migration path documented?                      | CHANGELOG     | Breaking changes |

---

## 19. Documentation & Traceability

| #    | Check                                              | Source                   | Before              |
| ---- | -------------------------------------------------- | ------------------------ | ------------------- |
| 19.1 | Have I updated docs for changed behavior?          | NEW_CAPABILITY_CHECKLIST | New features        |
| 19.2 | Is there inline explanation for non-obvious logic? | Code review              | Complex code        |
| 19.3 | Are entry points (AGENTS.md, README) current?      | CROSS_PLATFORM           | Agent-facing        |
| 19.4 | Did I update CHANGELOG or release notes?           | Release process          | User-facing changes |
| 19.5 | Is the decision rationale captured?                | ADRs, lessons            | Non-trivial choices |

---

## 20. Observability & Debugging

| #    | Check                                                | Source                | Before          |
| ---- | ---------------------------------------------------- | --------------------- | --------------- |
| 20.1 | Can I trace this through logs?                       | Observability         | Production ops  |
| 20.2 | Are errors actionable? (message, context, next step) | Error handling        | Exception paths |
| 20.3 | Do I have a way to verify success?                   | Verification          | Post-execution  |
| 20.4 | Am I logging at the right level? (debug vs info)     | Logging best practice | Verbosity       |
| 20.5 | Is audit trail sufficient for postmortem?            | constitution §3       | Transformations |

---

## 21. Scope & Granularity

| #    | Check                                      | Source               | Before          |
| ---- | ------------------------------------------ | -------------------- | --------------- |
| 21.1 | Am I doing the smallest safe change?       | Incremental delivery | Large tasks     |
| 21.2 | Should this be batched vs incremental?     | Performance          | Bulk operations |
| 21.3 | Am I addressing the root cause vs symptom? | Root cause analysis  | Bug fixes       |
| 21.4 | Is my scope creep-free?                    | AGENTS_EFFICIENCY    | Stay on task    |
| 21.5 | Do I need to split into subtasks?          | Todo management      | 4+ step tasks   |

---

## 22. Human-in-the-Loop

| #    | Check                                                | Source            | Before                 |
| ---- | ---------------------------------------------------- | ----------------- | ---------------------- |
| 22.1 | When do I stop and ask vs auto-proceed?              | constitution §1   | High-stakes            |
| 22.2 | Is the approval checkpoint clear?                    | my-agent.agent.md | Orchestrator           |
| 22.3 | Am I surfacing uncertainty for human review?         | Sedona AI         | Low-confidence outputs |
| 22.4 | Would a human understand my output?                  | Explainability    | Reports, summaries     |
| 22.5 | Have I flagged for attorney review per constitution? | constitution      | Privilege, filings     |

---

## Quick Reference (Copy to Prompts)

```
BEFORE EXECUTE:
├── Governance: high-stakes? claim typing? audit? disclaimer?
├── Safety: destructive? secrets? read target? valid format?
├── Efficiency: one task? output path? persist? no verify loop?
├── Sources: SOURCES_AND_EMULATION_INDEX? emulate patterns? lessons?
├── Repo: canonical? indexes updated? AGENTS/CLAUDE present?
├── Architecture: schema-first? router-first MCP? config exists?
├── Tools: one per step? paginate? persist between?
├── Agent: delegate? playbook? Evaluator gate? skill?
├── Prompt: instructions first? specific? examples? GOLDEN?
├── Improvement: baseline? postmortem/patterns/lessons? anti-pattern?
├── Skills: ontology skills? create skill? verify skills exist?
├── Compliance: ABA/EDRM/Sedona/ISO? GDPR if PII?
├── Verify: routing? connections? env? schemas? pre-commit?
├── Testing: evals? golden? edge cases? baseline?
├── Security: sanitize input? no injection? RBAC? PII policy?
├── Idempotency: retry-safe? rollback path? --dry-run first?
├── Dependencies: pinned? CVE? license? migration path?
├── Docs: updated? rationale captured? entry points current?
├── Observability: traceable? actionable errors? audit sufficient?
├── Scope: smallest safe change? root cause? no creep?
├── Human: when ask vs proceed? approval clear? uncertainty surfaced?
└── Cost: <10% improvement? lightweight after prompt?
```

---

## Execution Order

1. **Critical path** (must pass): 1.1–1.5 (governance), 2.1–2.4 (safety), 3.1–3.5 (efficiency), 16.1–16.5 (security)
2. **Emulation path**: 4.1–4.4, 11.1–11.6
3. **Platform path**: 5.1–5.5, 6.1–6.5
4. **Improvement path**: 10.1–10.6
5. **Verification path**: 13.1–13.5
6. **Quality path**: 15.1–15.5 (testing), 17.1–17.5 (idempotency), 19.1–19.5 (docs)
7. **Human path**: 22.1–22.5 (when to stop, surface uncertainty)

---

_Maintain at: docs/SUPER_DEVELOPER_PRE_EXECUTION_CHECKLIST.md. Update when adding new checks or principles._
