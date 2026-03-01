# Expert Prompt Engineering — Top LLM Practices Consolidated

> **Purpose**: Production-grade prompt practices from Anthropic Claude, OpenAI, Google Gemini, Cursor, and Prompt Builder. Applied for super-developer accuracy and zero-mistake workflows.
>
> **Sources**: platform.claude.com, platform.openai.com, ai.google.dev, cursor.com, promptbuilder.cc (full review 2025-02)
>
> **Referenced by**: constitution, SUPER_DEVELOPER_PRE_EXECUTION_CHECKLIST, expert-prompting.mdc, zero-mistake-workflow skill

---

## 1. Claude (Anthropic) Best Practices

| Practice                | What                                                                                                                  | Apply When                  |
| ----------------------- | --------------------------------------------------------------------------------------------------------------------- | --------------------------- |
| **Be clear and direct** | Explicit, specific instructions. Golden rule: Show to colleague with minimal context—if confused, Claude will be too. | Every prompt                |
| **Add context**         | Explain _why_ constraints matter; Claude generalizes from reasoning.                                                  | Constraint-heavy prompts    |
| **Use 3–5 examples**    | Structured in `<examples>` tags; diverse; relevant. Few-shot dramatically improves consistency.                       | Format-sensitive outputs    |
| **Structure with XML**  | `<instructions>`, `<context>`, `<documents>`, `<query>`. Nest when hierarchy exists.                                  | Complex, multi-part prompts |
| **Give a role**         | One sentence: "You are a helpful coding assistant specializing in Python."                                            | System/instruction context  |
| **Long context**        | Put long docs at TOP; query at END (up to 30% improvement); wrap each doc in `<document>` with metadata.              | 20K+ token inputs           |
| **Ground in quotes**    | For doc tasks: "Quote relevant parts first, then analyze." Reduces hallucination.                                     | Long document analysis      |
| **Chain-of-thought**    | Dedicated space to think before responding; improves accuracy.                                                        | Complex reasoning           |
| **Say what TO do**      | "Your response should be composed of smoothly flowing prose." Not "Do not use markdown."                              | Output control              |

---

## 2. OpenAI Best Practices

| Practice                  | What                                                                       | Apply When                     |
| ------------------------- | -------------------------------------------------------------------------- | ------------------------------ |
| **Instructions first**    | Put instructions at beginning; use `###` or `"""` delimiters.              | Every prompt                   |
| ** developer > user**     | Chain of command: developer messages prioritized over user.                | System logic vs user input     |
| **Be specific**           | Context, outcome, length, format, style—not vague.                         | Any non-trivial task           |
| **Examples for format**   | Show output format with examples; models respond better than descriptions. | Structured output              |
| **Progressive prompting** | Zero-shot → few-shot → fine-tune.                                          | Scaling from simple to complex |
| **Pin model snapshots**   | Use specific snapshots for production consistency.                         | Production deployments         |
| **Build evals**           | Measure prompt performance as you iterate and upgrade.                     | Production, version changes    |
| **Prompt caching**        | Up to 80% latency reduction, 75% cost reduction for repeated context.      | High-context apps              |

---

## 3. Google Gemini Best Practices

| Practice                | What                                          | Apply When           |
| ----------------------- | --------------------------------------------- | -------------------- |
| **Clear instructions**  | Concise, specific.                            | Every prompt         |
| **Structure with ##**   | Use markdown headers for structure.           | Long prompts         |
| **Provide examples**    | 3–5 for format and edge cases.                | Format-sensitive     |
| **Optimize length**     | Explicitly constrain output length.           | Cost/speed sensitive |
| **Lower temperature**   | For deterministic tasks.                      | Reproducible outputs |
| **Break complex tasks** | Multiple focused prompts vs one giant prompt. | Multi-step workflows |

---

## 4. Cursor Rules & AGENTS.md Best Practices

| Practice                   | What                                                    | Apply When             |
| -------------------------- | ------------------------------------------------------- | ---------------------- |
| **Plan Mode first**        | Shift+Tab: create detailed plan before coding.          | Complex implementation |
| **Let agents search**      | Don't manually tag everything; agents find context.     | Large codebases        |
| **Revert and refine**      | Fix plans rather than patch in-progress work.           | When plan drifts       |
| **Modular rules**          | One rule file per feature (backend, frontend, testing). | .cursor/rules/         |
| **&lt;500 lines per file** | Split when rules cover distinct contexts.               | Rule maintenance       |
| **Verification steps**     | Concrete examples, edge-case handling.                  | Every rule             |
| **Real examples**          | Correct/incorrect patterns; mark deprecated explicitly. | Rule content           |
| **README/AGENTS current**  | Entry points must reflect current behavior.             | Agent-facing docs      |

---

## 5. GOLDEN Checklist (Prompt Builder)

For complex prompts, apply:

| Letter | Element    | Check                                                 |
| ------ | ---------- | ----------------------------------------------------- |
| **G**  | Goal       | Is the goal explicit and measurable?                  |
| **O**  | Output     | Is output format specified with examples?             |
| **L**  | Limits     | Are constraints (length, scope, exclusions) clear?    |
| **D**  | Data       | Is input data structure and availability specified?   |
| **E**  | Evaluation | How will success be verified? (tests, rubric, human)  |
| **N**  | Next       | What happens after? (follow-up, handoff, persistence) |

---

## 6. Anti-Patterns to Avoid

| Anti-Pattern            | Fix                                                                                                |
| ----------------------- | -------------------------------------------------------------------------------------------------- |
| Vague goals             | "Create a dashboard" → "Create analytics dashboard with 5 charts, filters, export CSV, responsive" |
| Format drift            | Specify output with 3–5 examples; validate against schema                                          |
| Context dumping         | Put only relevant context; structure with tags                                                     |
| Hidden constraints      | State all constraints explicitly; explain why                                                      |
| Say what NOT to do only | Lead with what TO do                                                                               |
| No verification path    | Add self-check, tests, or rubric before delivery                                                   |
| Single giant prompt     | Break into explore→plan→code or sub-tasks                                                          |

---

## 7. Self-Verification Path (Before Delivery)

Before delivering output:

1. **Run tests** if code changed
2. **Validate output** against schema or expected format
3. **Quote sources** when grounding in documents
4. **Course-correct early** if diverging from goal
5. **One-line capture** after prompt (pattern or postmortem) — no heavy ops

---

## 8. Integration with Constitution

- **Claim typing** (FACT/INFERENCE/OPINION/LEGAL) applies to every assertion in prompts
- **Audit trail** — preserve prompts, tool calls, outputs for transformations
- **Simulation disclaimer** — all litigation outputs are drafts; attorney review required
- **High-stakes** — human checkpoint required; never auto-approve

---

## Quick Reference (Copy to Prompts)

```
EXPERT PROMPTING:
├── Claude: Clear, direct; 3-5 examples in <examples>; XML structure; role; long docs at top
├── OpenAI: Instructions first; ### delimiters; examples for format; pin model
├── Cursor: Plan first; agents search; modular rules; verify steps
├── GOLDEN: Goal, Output, Limits, Data, Evaluation, Next
├── Anti: No vague goals; no format drift; no context dump; verify before deliver
└── Self-check: Tests, schema validate, quote sources
```

---

_Maintain at: docs/EXPERT_PROMPT_ENGINEERING.md. Re-review quarterly with SOURCES_REVIEWED._
