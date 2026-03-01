# Agent Orchestration Best Practices — Production-Grade Multi-Agent Systems

> **Purpose**: Best practices from Microsoft Multi-Agent Reference Architecture, arXiv agentic workflows paper, Collabnix, and production deployments. Aligns with constitution and my-agent.agent.md.
>
> **Sources**: learn.microsoft.com/azure/architecture/ai-ml, arxiv.org/2512.08769, collabnix.com, Microsoft multi-agent-reference-architecture (full review 2025-02)
>
> **Referenced by**: constitution, my-agent.agent.md, master-orchestrator, SUPER_DEVELOPER_PRE_EXECUTION_CHECKLIST

---

## 1. Nine Core Best Practices (Production-Grade Agentic AI)

| #   | Practice                               | What                                                                 | Apply When          |
| --- | -------------------------------------- | -------------------------------------------------------------------- | ------------------- |
| 1   | **Tool-first design**                  | Use Model Context Protocol (MCP); tools before logic                 | All agent design    |
| 2   | **Pure-function invocation**           | Predictable, deterministic tool calls                                | Tool implementation |
| 3   | **Single-tool, single-responsibility** | One agent = one tool/responsibility; reduce complexity               | Agent design        |
| 4   | **Externalized prompt management**     | Prompts in config/playbooks.yaml, not hardcoded                      | Maintainability     |
| 5   | **Model-consortium + Responsible AI**  | Align with constitution: human-in-loop, claim typing, explainability | High-stakes         |
| 6   | **Clean separation**                   | Workflow logic separate from MCP servers                             | Architecture        |
| 7   | **Containerized deployment**           | Scalable, reproducible ops                                           | Production          |
| 8   | **KISS**                               | Keep It Simple; lowest complexity that works                         | Design decisions    |
| 9   | **Deterministic orchestration**        | Clear workflow decomposition; no hidden state                        | Orchestrator design |

---

## 2. Orchestration Patterns

| Pattern               | Use When                                     | Pros                           | Cons                          |
| --------------------- | -------------------------------------------- | ------------------------------ | ----------------------------- |
| **Centralized**       | Strong consistency, simplified monitoring    | Single source of truth         | Bottleneck at scale           |
| **Decentralized P2P** | Scale, fault tolerance                       | No single point of failure     | Consensus complexity          |
| **Hybrid**            | Orchestrator + specialist agents (our model) | Balance control and delegation | Clear delegation rules needed |

**Our default**: Centralized orchestrator (master-orchestrator) delegates to specialist agents. Evaluator Swarm gates high-stakes outputs.

---

## 3. When to Use Multi-Agent vs Single Agent

| Level                     | Use When                              | Example                                  |
| ------------------------- | ------------------------------------- | ---------------------------------------- |
| Direct model call         | Simple, single-task                   | One API call for summarization           |
| Single agent + tools      | Domain-specific query                 | RAG over case files                      |
| Multi-agent orchestration | Cross-functional, specialized domains | Privilege + Contract + Compliance agents |

**Rule**: Use lowest complexity that solves the problem.

---

## 4. Enterprise Design Principles

| Principle                          | What                                                 | Source                   |
| ---------------------------------- | ---------------------------------------------------- | ------------------------ |
| **Separation of concerns**         | Each agent has distinct, well-defined responsibility | Azure Architecture       |
| **Secure by design**               | Auth, authorization, sensitive data management       | security.md              |
| **Observability & traceability**   | End-to-end instrumentation; correlated metrics       | constitution §3          |
| **Agent registration & lifecycle** | Version control, validation before production        | NEW_CAPABILITY_CHECKLIST |
| **Failure isolation**              | Prevent cascading failures; graceful degradation     | RECURSIVE_IMPROVEMENT    |
| **Context management**             | Clear policies on shared state, data propagation     | AGENTS_EFFICIENCY        |

---

## 5. Integration with Constitution

- **Human-in-loop** (§1): Orchestrator never auto-approves high-stakes (privilege, filing, production, damages)
- **Claim typing** (§2): Fact Checker, Logic Auditor, Ethics Reviewer, Citation Validator per claim type
- **Audit trail** (§3): Preserve prompts, tool calls, params, outputs, evaluator results
- **New capabilities** (§6): Create skill, update indexes, emulate reference patterns

---

## 6. Playbook & Config

| Config                             | Purpose                                  |
| ---------------------------------- | ---------------------------------------- |
| `config/playbooks.yaml`            | Per-agent prompt templates; externalized |
| `config/connectors.yaml`           | MCP servers; budgets; tool registry      |
| `docs/playbooks/*.md`              | Detailed per-agent instructions          |
| `.github/agents/my-agent.agent.md` | Master spec; multi-agent roles           |

---

## 7. Anti-Patterns

| Anti-Pattern             | Fix                                            |
| ------------------------ | ---------------------------------------------- |
| God agent                | Split by responsibility; delegate              |
| Hardcoded prompts        | Move to playbooks.yaml                         |
| No Evaluator gate        | Add Fact/Citation/Logic/Ethics for high-stakes |
| Shared mutable state     | Single evidence base; immutable audit          |
| Missing human checkpoint | Add approval step per constitution §1          |

---

## Quick Reference

```
ORCHESTRATION:
├── Tool-first (MCP); single-tool single-responsibility
├── Externalized prompts (playbooks.yaml)
├── Centralized orchestrator → specialist agents
├── Evaluator Swarm for high-stakes
├── Secure, observable, failure-isolated
└── Constitution §1-6 always applies
```

---

_Maintain at: docs/AGENT_ORCHESTRATION_BEST_PRACTICES.md_
