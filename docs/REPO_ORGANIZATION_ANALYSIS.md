# Repo Organization Analysis — Why LexVault Was Missed & What Else Needs Sorting

> **Purpose**: Post-mortem on LexVault/modules sync gap; inventory of repos needing organization; best practices from constitution and master files.

**Referenced by**: REFERENCE_PATTERNS_AND_EXAMPLE_REPOS, CROSS_PLATFORM_UPDATE_CHECKLIST, NEW_CAPABILITY_CHECKLIST

---

## 1. How Was LexVault / docs/modules Missed?

### Root Causes

| Factor                       | Explanation                                                                                                                                                                                                                             |
| ---------------------------- | --------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| **Incremental growth**       | Constitution routing was designed first (route-constitution-to-repos.sh). Principles, agent instructions, and module specs were added later — no single "propagation inventory" existed.                                                |
| **Different artifact types** | Constitution, checklist, universal are **governance** files. docs/modules/ are **reference patterns** — they were documented in cross-system-index but never added to the sync script's artifact list.                                  |
| **Index vs. sync**           | NEW_CAPABILITY_CHECKLIST said "update cross-system-index" for new repos but did NOT say "sync docs/modules" or "emulate LexVault." Constitution §6 said "update indexes" but did not mention reference patterns until added in 2026-02. |
| **No propagation checklist** | CONSTITUTION_ROUTING_DESIGN and AUTOMATION_INSTRUCTIONS_SYNC focus on constitution→repos. There was no holistic checklist of "everything that must propagate to child repos."                                                           |
| **Pre-push hook scope**      | Pre-push only triggers on constitution, checklist, universal, bootstrap — not on docs/modules or REFERENCE_PATTERNS.                                                                                                                    |

### What Was Missing in Master Instructions

- **UNIVERSAL_INSTRUCTIONS**: Did not mention docs/modules or REFERENCE_PATTERNS
- **master-project-rules.mdc**: "Before adding new capabilities" did not cite docs/modules/lexvault or REFERENCE_PATTERNS
- **CONSOLIDATION_AND_REPO_STATUS**: Did not list docs/modules as synced artifacts

### Fix Applied (2026-02)

- docs/modules/ and REFERENCE_PATTERNS_AND_EXAMPLE_REPOS.md added to sync-all-repos-and-review.sh
- Constitution §6 step 5 added: emulate LexVault for file/evidence; ontology for schemas
- NEW_CAPABILITY_CHECKLIST, CROSS_PLATFORM_UPDATE_CHECKLIST, routing-verification.yaml updated

---

## 2. Repos That Need Sorting / Organizing

From `docs/REPO_SIMILARITY_AND_MERGE_PLAN.md` (259 repos analyzed):

### High Priority (Merge or Add to Sync)

| Cluster                    | Repos | Action                                                | Status                                                                |
| -------------------------- | ----- | ----------------------------------------------------- | --------------------------------------------------------------------- |
| **Next.js AI chatbot**     | 5     | Merge into nextjs-ai-chatbot                          | Pending; add to REFERENCE_PATTERNS "clone when creating"              |
| **PowerConnection**        | 5     | powerconnectionaiapplications canonical; merge others | powerconnectionai, powerconnectionodoo, spark-insight-chooser pending |
| **LitigationForce family** | 9     | Merge variants into LitigationForce.AI                | litforce-ai-gateway, litigationagentsmultimodalchat, etc.             |
| **connected-agent**        | 3     | Merge into connected-agents-platform                  | connected-agent-ai, Connectedagentsrepo1                              |
| **Vercel AI demos**        | 8     | Create vercel-ai-demos monorepo or archive            | vercel-ai-gateway-demo, etc.                                          |

### Medium Priority

| Cluster         | Repos | Action                                           |
| --------------- | ----- | ------------------------------------------------ |
| AI SDK starters | 3     | Merge litforce/deepinfra into ai-sdk-starter-xai |
| Powermed        | 2     | Merge design variant → Powermed-Marketing        |
| InfraNodus      | 2     | Delete 2infranodus-obsidian-plugin (duplicate)   |

### Low Value (Archive Candidates)

| Repos                         | Reason               |
| ----------------------------- | -------------------- |
| demo-repository               | GitHub demo template |
| ubiquitous-octo-dollop        | Generic clone        |
| skills-introduction-to-github | Generic              |
| Cursor-Project-1              | Generic              |
| precedent, daddy, remix       | Unclear purpose      |

### Repos Needing Bootstrap When Cloned

| Repo              | When to Add                  | How                                                             |
| ----------------- | ---------------------------- | --------------------------------------------------------------- |
| nextjs-ai-chatbot | Clone for new chat UI        | Run bootstrap-repo-with-constitution.sh; add to ROUTES if local |
| adk-python        | Reference for agent patterns | GitHub-only; document in REFERENCE_PATTERNS                     |
| connectedenergyai | After CEA transfer           | Manual clone → push → delete source                             |

---

## 3. Best Practices (From Constitution & Master Files)

### Constitution §6 — New Capabilities

1. Read constitution, my-agent.agent.md, master-project-rules.mdc
2. Create skill at .cursor/skills/{name}/
3. Use ontology skills for schemas/lists/entities
4. Update cross-system-index, CONSOLIDATION_AND_REPO_STATUS, MASTER_AGENT_INDEX
5. **Emulate reference patterns**: file/evidence → lexvault.md; entity schemas → ontology.md

### NEW_CAPABILITY_CHECKLIST

- New repo → update cross-system-index, CONSOLIDATION_AND_REPO_STATUS, REFERENCE_PATTERNS (if template)
- File/evidence → emulate LexVault; entity schemas → ontology

### CONSOLIDATION_AND_REPO_STATUS — New Repo

1. Add to ROUTES (route-constitution) if local path exists
2. Or run bootstrap-repo-with-constitution.sh (GitHub-only)
3. Create AGENTS.md and CLAUDE.md with READ FIRST block
4. Update cross-system-index
5. Update this doc

### SUPER_DEVELOPER_PRINCIPLES

- **Sync instructions**: Canonical sources propagate via sync-all-repos-and-review.sh
- **Cadenced heavy ops**: Weekly sync; monthly research; quarterly audit

### ALL_REPO_REVIEW

- Run sync-all-repos-and-review.sh —review
- Cadence: immediate on setup; weekly or when adding repos

### Propagation Checklist (Complete)

| Artifact                                            | Synced By          | When       |
| --------------------------------------------------- | ------------------ | ---------- |
| constitution.md                                     | route-constitution | Every sync |
| NEW_CAPABILITY_CHECKLIST, UNIVERSAL_INSTRUCTIONS    | route-constitution | Every sync |
| platform-bootstrap.mdc                              | route-constitution | Every sync |
| SUPER_DEVELOPER_PRINCIPLES, SOURCES_REVIEWED        | sync script        | Every sync |
| ALL_REPO_REVIEW, CROSS_PLATFORM_UPDATE_CHECKLIST    | sync script        | Every sync |
| my-agent.agent.md, master-orchestrator.md           | sync script        | Every sync |
| docs/modules/\*.md (LexVault, ontology, etc.)       | sync script        | Every sync |
| REFERENCE_PATTERNS_AND_EXAMPLE_REPOS.md             | sync script        | Every sync |
| Bootstrap (developer-enhancement, agent-efficiency) | sync script        | Every sync |

---

## 4. Gaps to Close (Full Incorporation)

| Gap                              | Recommendation                                                                                                                                                                                       |
| -------------------------------- | ---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| UNIVERSAL_INSTRUCTIONS           | Add step 7: "Reference patterns — docs/modules/lexvault.md (file/evidence), docs/modules/ontology.md (schemas), docs/REFERENCE_PATTERNS_AND_EXAMPLE_REPOS.md"                                        |
| master-project-rules.mdc         | Add to "Before Adding New Capabilities": "For file/evidence systems, read docs/modules/lexvault.md; for entity schemas, docs/modules/ontology.md. See docs/REFERENCE_PATTERNS_AND_EXAMPLE_REPOS.md." |
| Pre-push hook                    | Optionally add docs/modules/ and REFERENCE_PATTERNS to trigger route OR run full sync (heavier)                                                                                                      |
| CONSOLIDATION_AND_REPO_STATUS §8 | Add docs/modules and REFERENCE_PATTERNS to Document Reference Matrix                                                                                                                                 |

---

_Maintain at: docs/REPO_ORGANIZATION_ANALYSIS.md. Update when merge plan executes or new gaps found._
