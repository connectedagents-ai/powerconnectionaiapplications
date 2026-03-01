# Top Repo & Dev Best Practices — Industry Standards Consolidated

> **Purpose**: Best practices from top repos, dev tools, and dev docs. Integrated into SUPER_DEVELOPER_PRINCIPLES, AGENT_ORCHESTRATION, and virtuous loop. Full review 2025-02.
>
> **Sources**: 12-Factor Agents (18K★), Awesome Agent Skills, OSS Guide, Cursor/Claude, MCP, Legal Benchmarks 2025

---

## 1. 12-Factor Agents (humanlayer/12-factor-agents)

Production-ready LLM applications. Most products use deterministic code with LLM steps at key points.

| Factor                            | Principle                                         | Our Implementation                                    |
| --------------------------------- | ------------------------------------------------- | ----------------------------------------------------- |
| **Own your prompts**              | Externalize; version; no hardcoding               | config/playbooks.yaml, docs/EXPERT_PROMPT_ENGINEERING |
| **Own your context**              | Token-efficient; structure; pre-fetch when needed | AGENTS_EFFICIENCY, pagination, schema-first           |
| **Tools = structured outputs**    | Schemas; explicit side effects                    | docs/schemas/, MCP tool descriptors                   |
| **Contact humans via tool calls** | Human checkpoint as tool, not bolt-on             | Constitution §1, HumanCheckpoint                      |
| **Small, focused agents**         | One responsibility per agent                      | AGENT_ORCHESTRATION_BEST_PRACTICES §3                 |
| **Stateless reducer**             | Execution state separate from business state      | Orchestrator pattern                                  |
| **Compact errors**                | Fit errors into context; actionable messages      | Observability §20                                     |
| **Launch/Pause/Resume**           | Simple APIs for suspension                        | Checkpoint JSON, resume from step                     |

---

## 2. AGENTS.md & Dev Tool Best Practices

| Source                  | Practice                                                            | Apply                                |
| ----------------------- | ------------------------------------------------------------------- | ------------------------------------ |
| **Cursor**              | Plan Mode before coding; separate research from implementation      | SUPER_DEVELOPER_PRE_EXECUTION §9.5   |
| **Claude Code**         | Verification essential: tests, screenshots, expected outputs        | EXPERT_PROMPT_ENGINEERING §7         |
| **AGENTS.md 3-layer**   | Global (~/.codex) < Project (repo) < Module (dir). Closer overrides | AGENTS.md, CLAUDE.md, .cursor/rules/ |
| **Context engineering** | Let agents search; don't manually tag everything                    | Cursor Plan Mode                     |
| **AGENTS.override.md**  | Temporary project-phase overrides                                   | Optional per repo                    |

---

## 3. Open Source Documentation (GitHub OSS Guide)

| Doc                 | Purpose                                     | Status                     |
| ------------------- | ------------------------------------------- | -------------------------- |
| **README**          | Purpose, install, quickstart                | ✅                         |
| **CONTRIBUTING**    | How to contribute; PR process; style guide  | Add                        |
| **CODE_OF_CONDUCT** | Community standards (Contributor Covenant)  | Add                        |
| **SECURITY**        | Vulnerability reporting; security policy    | Add                        |
| **Documentation**   | Keep current; mark outdated; invite updates | SOURCES_REVIEWED quarterly |

**Insight**: Projects with comprehensive CONTRIBUTING receive 3x more PRs.

---

## 4. MCP Best Practices

| Principle                 | Implementation                                     |
| ------------------------- | -------------------------------------------------- |
| **Single responsibility** | One clear domain per MCP server                    |
| **Controlled autonomy**   | Least-privilege tools; approval for high-impact    |
| **Contracts first**       | Strict input/output schemas; explicit side effects |
| **Security by design**    | Auth, authorization, audit in servers              |
| **Stateless by default**  | Scalability and resilience                         |
| **Input validation**      | Schema validation; allow-lists; sanitize outputs   |

---

## 5. Awesome Agent Skills (skillmatic-ai)

| Practice                   | Implementation                               |
| -------------------------- | -------------------------------------------- |
| **Modular SKILL.md**       | YAML frontmatter, Instructions, Examples     |
| **Progressive disclosure** | Router-first MCP; fetch schema on demand     |
| **Learning phases**        | Fundamentals → Implementation → Benchmarking |

---

## 6. Legal AI Benchmarks 2025

| Finding                                                    | Implication                                 |
| ---------------------------------------------------------- | ------------------------------------------- |
| AI 73.3% first-draft reliability vs 70% human              | Competitive; emphasize verification         |
| Risk detection: Legal AI 83% vs general AI 55% vs human 0% | Lead with risk-detection strength           |
| Workflow integration = differentiator                      | Integrate with Word, case mgmt, e-discovery |
| Two-thirds use 2+ platforms                                | Multi-tool support; connector strategy      |

---

## 7. Capture Template (Virtuous Loop)

Standardize one-line captures:

```
[PATTERN|POSTMORTEM] [action] [outcome] [1-line]
```

Examples:

- `[PATTERN] Used XML tags for prompt structure — 30% format consistency gain`
- `[POSTMORTEM] Sync failed on powerconnection path — add existence check before cp`

---

## 8. Verification Checklist (Before Delivery)

From Claude Code, Cursor, Anthropic:

1. Run tests if code changed
2. Validate output against schema
3. Quote sources when grounding in documents
4. Course-correct early if diverging
5. One-line capture after prompt (no heavy ops)

---

_Maintain at: docs/TOP_REPO_AND_DEV_BEST_PRACTICES.md. Re-review quarterly with SOURCES_REVIEWED._
