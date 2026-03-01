# Product That Builds the Product — Architecture as Core Tenet

**Purpose:** (1) State that OneWish OS is **the product that builds the product**, with **architecture** as a core feature and tenet. (2) Require that **after each review** we run a step that ensures all **new commands are organized in place** and that **architecture** is **updated and/or reviewed** (in whole or in part) based on **computer-science-based rules**, **repos**, and **best practices**, **every time relevant to any change**.

**Governance:** Constitution §8 (integration, code-through-architecture); [ONEWISHOS_ARCHITECTURE_AND_METHODS.md](ONEWISHOS_ARCHITECTURE_AND_METHODS.md); [NEVER_MISS_INSTRUCTIONS.md](NEVER_MISS_INSTRUCTIONS.md); [EVAL_LOOP_AND_CHAIN_OF_EVENTS.md](EVAL_LOOP_AND_CHAIN_OF_EVENTS.md).

---

## 1. The product that builds the product

OneWish OS **is the product that builds the product**. It is the platform that defines, propagates, and improves the systems, repos, agents, workflows, and tooling that deliver value. Core to that role:

- **Architecture** is a **core feature and tenet**. Structure, layering, single source of truth, propagation order, and review/audit flow are first-class; they are not incidental.
- **Commands and scripts** are the executable surface of that architecture. Every new command must be **organized in place** (indexed, categorized, and documented where to use it) so the product remains coherent and discoverable.
- **Architecture must be reviewed** in whole or in part whenever changes are relevant—aligned to computer-science-based rules, reference repos, and best practices (e.g. SOURCES_AND_EMULATION_INDEX, 12-Factor, Production-Grade Agentic AI, MCP best practices, TRiSM, ABA/EDRM/Sedona).

---

## 2. After each review: commands organized + architecture reviewed

**Rule:** After each **Review** (Full Review, Comprehensive Eval, Genie loop, Go flow, or any run that produces a review artifact), run the **commands-and-architecture review** step so that:

| Requirement | What it means |
|-------------|----------------|
| **All new commands organized in place** | Every script in `scripts/` is accounted for in the commands/scripts index; new scripts are added to the index and to the appropriate “when to use” doc (e.g. NEVER_MISS_INSTRUCTIONS, ONEWISH_OMNI_MAC_DATA_MODEL_AND_COMMANDS). Entry points (run-review.sh, run-go-flow.sh, run-full-review.sh, etc.) remain the canonical list. |
| **Architecture updated and/or reviewed** | Architecture docs (ONEWISHOS_CRYSTAL_CLEAR_ARCHITECTURE_AND_AGENT_TAXONOMY, ONEWISHOS_ARCHITECTURE_AND_METHODS, MASTER_INDEX, SOURCES_AND_EMULATION_INDEX, CORE_ARCHITECTURE_TENETS) are checked for consistency with the change. Where the change touches structure, layers, propagation, or review flow, architecture is updated or explicitly reviewed (in whole or in part) against CS-based rules, reference repos, and best practices. |

**Script:** `./scripts/run-commands-and-architecture-review.sh`  
- Runs automatically at the end of Full Review and at the end of Comprehensive Eval (post-run eval).  
- Produces: `docs/audits/commands-and-architecture-review-latest.md` (and optionally appends a one-line to chain-of-events).  
- No-fail: the step always runs; findings are reported so that “organize commands” and “review architecture” are never skipped.

---

## 3. Computer-science and best-practice basis

Architecture review (in whole or in part) is aligned to:

- **Computer science:** Single source of truth per category; canonical lists; dependency order; contracts first (schemas, inputs/outputs); no-fail audit so no target is missed.
- **Repos and standards:** SOURCES_AND_EMULATION_INDEX; BEST_PRACTICES_FROM_TOP_REPOS; 12-Factor Agents; Production-Grade Agentic AI (arXiv 2512.08769); MCP best practices; Google Cloud agent evaluation (three pillars); TRiSM; ABA/EDRM/Sedona where applicable.
- **Relevance to change:** Only the parts of architecture (and only the commands) affected by the change need to be updated or reviewed in that run; “in part” is sufficient when the change is scoped.

---

## 4. Where this is wired

| Where | What runs |
|-------|-----------|
| **run-full-review.sh** | After Phase 2 (summary write), runs `run-commands-and-architecture-review.sh`. |
| **run-comprehensive-eval-and-cleanup.sh** | After post-run eval (chain of events), runs `run-commands-and-architecture-review.sh`. |
| **run-go-flow.sh** | Full Review is step 3; Full Review already invokes the commands-and-architecture review. |
| **run-review.sh** / **run-every-turn.sh** | Comprehensive Eval runs at the end; it invokes the commands-and-architecture review. |

So every Full Review and every Comprehensive Eval run includes the “commands organized + architecture reviewed” step.

---

## 5. References

| Doc | Purpose |
|-----|--------|
| [ONEWISHOS_ARCHITECTURE_AND_METHODS.md](ONEWISHOS_ARCHITECTURE_AND_METHODS.md) | Leading methods; “best we can do”; alignment to CS and best practices |
| [NEVER_MISS_INSTRUCTIONS.md](NEVER_MISS_INSTRUCTIONS.md) | When to use each script; never-miss sequence; single source of truth |
| [COMMANDS_AND_SCRIPTS_INDEX.md](COMMANDS_AND_SCRIPTS_INDEX.md) | Canonical list of scripts by category; “organize in place” target |
| [EVAL_LOOP_AND_CHAIN_OF_EVENTS.md](EVAL_LOOP_AND_CHAIN_OF_EVENTS.md) | Eval after each run; chain of events |
| [SOURCES_AND_EMULATION_INDEX.md](SOURCES_AND_EMULATION_INDEX.md) | Top sources per action; repos and best practices for architecture review |

_Maintain at: docs/PRODUCT_THAT_BUILDS_THE_PRODUCT_AND_ARCHITECTURE_TENET.md._
