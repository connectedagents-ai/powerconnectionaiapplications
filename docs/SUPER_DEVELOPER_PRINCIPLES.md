# Super Developer Principles

> **Purpose**: Canonical list of principles reviewed and updated during all-repo review. Consolidated with architecture, workflows, and governance.
>
> **Review cadence**: Every all-repo review (run via `scripts/sync-all-repos-and-review.sh`).
>
> **Referenced by**: `docs/architecture.md`, AGENTS.md, route-constitution, ALL_REPO_REVIEW.md
>
> **Sources**: See `docs/SOURCES_REVIEWED.md` for full list of repos and LLM docs reviewed.

---

## 1. Safety First

| Principle                   | Definition                                                                             | Check             |
| --------------------------- | -------------------------------------------------------------------------------------- | ----------------- |
| **Confirm destructive ops** | Never `rm -rf`, force push, or overwrite production without explicit user confirmation | Guardrails rule   |
| **Never commit secrets**    | No API keys, tokens, passwords, `.env` (except `.env.example`)                         | Pre-commit scan   |
| **Validate before write**   | Read target file; check patterns; ensure valid format                                  | Before every edit |
| **Human checkpoint**        | High-stakes outputs (filings, privilege, production) require attorney/human sign-off   | Constitution      |

---

## 2. Efficiency & Context

| Principle                   | Definition                                                                | Check                 |
| --------------------------- | ------------------------------------------------------------------------- | --------------------- |
| **Execute, don't announce** | Never "I'll do X now" without doing it. One-line blocker if stuck         | Agent efficiency rule |
| **Persist early**           | Write to disk as soon as produced; don't hold large structures in context | Persistence protocol  |
| **Scope narrowly**          | One task per message; split multi-part requests                           | Self-correction       |
| **Verify once**             | No verification loops; verify once, move on                               | Anti-pattern list     |
| **Paginate APIs**           | Limit 10–25; minimal fields; cache to files                               | API/MCP efficiency    |

---

## 3. Recursive Improvement

| Principle                      | Definition                                                       | Check                 |
| ------------------------------ | ---------------------------------------------------------------- | --------------------- |
| **Post-mortem on failure**     | Write `postmortem-{date}.md`; capture cause, fix, suggested rule | Recursive improvement |
| **Lesson at session end**      | Append to `lessons.md` (do more, do less, rule to add)           | Constant improvement  |
| **Anti-pattern accretion**     | When noticing waste, add to anti-pattern list before continuing  | Agent efficiency      |
| **Pattern capture on success** | Append to `patterns-that-work.md` (what, why, reuse when)        | Constant improvement  |

---

## 4. Orchestration & Planning

| Principle                    | Definition                                                   | Check                 |
| ---------------------------- | ------------------------------------------------------------ | --------------------- |
| **Decompose then execute**   | Ordered steps; one outcome each; persist between steps       | Advanced capabilities |
| **Checkpoint between steps** | Write `checkpoint-{step}.json` or update plan status         | Planning template     |
| **One active step**          | Don't start step N+1 until step N is persisted and validated | Orchestration rules   |
| **Explicit handoffs**        | Output path of step N = input path of step N+1               | Delegation protocol   |

---

## 5. Governance & Compliance

| Principle                 | Definition                                                               | Check                     |
| ------------------------- | ------------------------------------------------------------------------ | ------------------------- |
| **Claim typing**          | Every assertion carries type: FACT, INFERENCE, OPINION, LEGAL_CONCLUSION | Evaluator swarm           |
| **Evaluator gate**        | Fact Checker, Citation Validator, Logic Auditor, Ethics Reviewer         | Constitution              |
| **Simulation disclaimer** | AI outputs are for support; require human review                         | Master rules              |
| **Provenance & audit**    | Who, what, when, input_hash, output_hash                                 | Security, ABA/EDRM/Sedona |

---

## 6. Constant Improvement (Meta)

| Principle                    | Definition                                                                   | Check                        |
| ---------------------------- | ---------------------------------------------------------------------------- | ---------------------------- |
| **Lightweight after prompt** | One-line capture; no heavy research or multi-agent review per prompt         | Constant improvement rule    |
| **Cadenced heavy ops**       | Weekly: consolidate. Monthly: research, multi-agent review. Quarterly: audit | CONTINUOUS_IMPROVEMENT.md    |
| **Sync instructions**        | Canonical sources propagate to all repos via sync script                     | sync-all-repos-and-review.sh |
| **Cost guardrail**           | Improvement activities &lt;10% of total                                      | Cost/time limits             |

---

## 7. Multi-Agent & Tool Coordination

| Principle                 | Definition                                                                   | Check                 |
| ------------------------- | ---------------------------------------------------------------------------- | --------------------- |
| **Router-first MCP**      | Small router tool set; discover actions by intent; fetch schema on demand    | docs/mcp-router.md    |
| **One tool per step**     | When coordinating (Linear, GitHub, etc.), one tool per step; persist between | Advanced capabilities |
| **No cross-tool context** | Assume no memory; pass data via files                                        | Orchestration         |
| **MCP pagination**        | Limit, sparse fields; cache responses                                        | API efficiency        |

---

## 8. Architecture Alignment

| Principle                | Definition                                                          | Check                          |
| ------------------------ | ------------------------------------------------------------------- | ------------------------------ |
| **Schema-first**         | Evidence, Claim, Timeline, Bundle formalized; examples in examples/ | docs/schemas/                  |
| **One evidence base**    | Track-specific outputs from shared evidence                         | Multi-track mapping            |
| **Constitution routing** | All repos receive constitution, checklist, universal, bootstrap     | route-constitution-to-repos.sh |
| **Repo consolidation**   | Canonical map; merged/archived status; ROUTES in sync script        | CONSOLIDATION_AND_REPO_STATUS  |

---

## 9. Prompt & Context Engineering (Top Coders / LLMs)

_Incorporated from: Anthropic Claude Code, OpenAI, Google Gemini, GitHub Copilot, AGENTS.md standard, GOLDEN checklist. See docs/SOURCES_REVIEWED.md._

| Principle                      | Definition                                                                            | Source                        |
| ------------------------------ | ------------------------------------------------------------------------------------- | ----------------------------- |
| **Self-verification**          | Give agent tests, screenshots, or expected outputs to verify its work before delivery | Anthropic                     |
| **Explore → Plan → Code**      | Separate research/planning from implementation; avoid solving the wrong problem       | Anthropic                     |
| **Instructions first**         | Put instructions at beginning; use ### or """ to separate from context                | OpenAI                        |
| **Be specific**                | Specify context, outcome, length, format, style; avoid vague or fluffy language       | OpenAI, Google                |
| **Output format via examples** | Articulate desired format through examples; show, don't just tell                     | OpenAI                        |
| **GOLDEN checklist**           | Goal, Output, Limits, Data, Evaluation, Next — before complex prompts                 | Prompt Builder                |
| **Zero-shot → few-shot**       | Start simple; add examples only if needed; fine-tune last resort                      | OpenAI                        |
| **Say what to do**             | Instead of only "don't do X," say what to do instead                                  | OpenAI                        |
| **Course-correct early**       | Redirect immediately when diverging; don't let wrong path continue                    | Anthropic                     |
| **CLAUDE.md / AGENTS.md**      | Persistent project context: commands, style, workflow rules                           | Anthropic, AGENTS.md standard |

---

## Sources & Emulation (Every Action)

Before significant work, check `docs/SOURCES_AND_EMULATION_INDEX.md` for top sources to emulate by action type. Apply virtuous loop: failure→postmortem+anti-pattern, success→patterns-that-work, session end→lessons.md.

---

## Review Protocol (During All-Repo Review)

When running `sync-all-repos-and-review.sh`:

1. **Read** this document and `docs/architecture.md`
2. **For each principle**: Is it still accurate? Is it implemented in rules/skills? Any gaps?
3. **Update** this document with additions, removals, or refinements
4. **Propagate** changes to architecture.md, AGENTS.md, and routed docs if needed
5. **Commit** SUPER_DEVELOPER_PRINCIPLES.md and related updates

---

## Quick Reference (Copy to System Prompts)

```
SAFETY: Confirm destructive; never secrets; validate before write; human checkpoint
EFFICIENCY: Execute don't announce; persist early; one task; verify once; paginate
IMPROVEMENT: Post-mortem; lesson; anti-pattern; pattern capture; cadence
ORCHESTRATION: Decompose; checkpoint; one active step; explicit handoffs
GOVERNANCE: Claim typing; evaluator gate; disclaimer; provenance
CONSTANT: One-line after prompt; weekly/monthly heavy ops; sync instructions
MULTI-AGENT: Router-first MCP; one tool per step; files for handoffs
ARCHITECTURE: Schema-first; one evidence base; constitution routing
PROMPT: Self-verify; explore→plan→code; instructions first; be specific; examples for format; GOLDEN; course-correct early
```

---

_Maintain at: docs/SUPER_DEVELOPER_PRINCIPLES.md. Updated during all-repo review._
