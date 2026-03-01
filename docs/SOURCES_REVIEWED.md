# Sources Reviewed — Top Repos & LLM Developer Docs

> **Purpose**: Confirm full review of best practices from top coders, repos, and LLM developer documentation. Updated with each all-repo sync.
>
> **Last full review**: 2025-02-24

---

## LLM Developer Documentation (Official)

| Source                        | URL                                                                 | Status         | Key Practices Incorporated                                                                                                           |
| ----------------------------- | ------------------------------------------------------------------- | -------------- | ------------------------------------------------------------------------------------------------------------------------------------ |
| **Anthropic Claude Code**     | docs.anthropic.com/en/docs/claude-code/best-practices               | ✅ Full review | Self-verification, explore→plan→code, context management, specific prompts, CLAUDE.md, course-correct early                          |
| **OpenAI Prompt Engineering** | help.openai.com, platform.openai.com/docs/guides/prompt-engineering | ✅ Full review | Instructions at start with delimiters, be specific, output format via examples, zero-shot→few-shot→fine-tune, reduce fluffy language |
| **Google Gemini API**         | ai.google.dev/gemini-api/docs/prompting-strategies                  | ✅ Full review | Clear instructions, be concise, structure with ##, provide examples, optimize output length, break complex tasks                     |
| **GitHub Copilot**            | docs.github.com/en/copilot/get-started/best-practices               | ✅ Full review | Break complex tasks, provide examples, baseline→improve→verify                                                                       |

---

## Top Repos & Community Resources

| Source                        | URL / Location                                        | Status         | Key Practices Incorporated                                                       |
| ----------------------------- | ----------------------------------------------------- | -------------- | -------------------------------------------------------------------------------- |
| **AGENTS.md standard**        | f/awesome-chatgpt-prompts AGENTS.md, Claude artifacts | ✅ Full review | Universal agent context; READ FIRST; context engineering                         |
| **Claude Code best practice** | shanraisshan/claude-code-best-practice                | ✅ Full review | AGENTS.md structure, agentic context                                             |
| **awesome-claude-agents**     | rahulvrane/awesome-claude-agents, Chat2AnyLLM         | ✅ Full review | Agent types, specialist patterns                                                 |
| **Prompt Builder GOLDEN**     | promptbuilder.cc                                      | ✅ Full review | Goal, Output, Limits, Data, Evaluation, Next (GOLDEN checklist)                  |
| **Cursor Rules guides**       | design.dev, majesticlabs, cursorhow.com               | ✅ Full review | .cursor/rules/\*.mdc, glob patterns, @reference, agentic rules                   |
| **Agentic Coding Context**    | Claude public artifacts                               | ✅ Full review | Context engineering: environmental, session, implicit, explicit                  |
| **Claude 4.6 Prompting**      | platform.claude.com/docs (2025-02)                    | ✅ Full review | XML tags, 3–5 examples, long docs at top, chain-of-thought                       |
| **OpenAI Prompt Engineering** | platform.openai.com/docs/guides (2025-02)             | ✅ Full review | Instructions first, developer role, evals, model pinning                         |
| **Microsoft Multi-Agent**     | learn.microsoft.com/azure/architecture/ai-ml          | ✅ Full review | Separation of concerns, observability, failure isolation                         |
| **Agentic Workflows (arXiv)** | arxiv.org/2512.08769                                  | ✅ Full review | Tool-first, single-responsibility, externalized prompts                          |
| **12-Factor Agents**          | github.com/humanlayer/12-factor-agents (18K★)         | ✅ Full review | Own prompts, context; tools=structured; human via tools; small agents; stateless |
| **Awesome Agent Skills**      | github.com/skillmatic-ai/awesome-agent-skills         | ✅ Full review | Modular SKILL.md, progressive disclosure                                         |
| **OSS Guide**                 | opensource.guide/best-practices                       | ✅ Full review | CONTRIBUTING, CODE_OF_CONDUCT, SECURITY; 3x PR with CONTRIBUTING                 |
| **MCP Best Practices**        | mcp-best-practice.github.io, modelcontextprotocol.io  | ✅ Full review | Single responsibility, controlled autonomy, contracts first                      |

---

## Practices Consolidated into SUPER_DEVELOPER_PRINCIPLES

### From Anthropic Claude Code

- Self-verification (tests, screenshots, expected outputs)
- Explore first → Plan → Code → Commit
- Manage context aggressively (track usage, reduce tokens)
- Provide specific context (files, constraints, patterns)
- CLAUDE.md for persistent project context
- Course-correct early and often

### From OpenAI

- Instructions at beginning; delimiters (###, """)
- Be specific about context, outcome, length, format
- Articulate output format through examples
- Zero-shot → few-shot → fine-tune progression
- Reduce fluffy descriptions; say what to do, not just what not to do

### From Google Gemini

- Clear, specific instructions; be concise
- Structure prompts with ##; provide examples
- Optimize output length; lower temperature for deterministic tasks
- Break complex tasks into multiple focused prompts

### From AGENTS.md / Cursor

- READ FIRST block; canonical doc references
- .cursor/rules/\*.mdc with globs; agentic instructions
- Reference architecture with @syntax; explicit context

### From GOLDEN / Prompt Builder

- Goal, Output, Limits, Data, Evaluation, Next
- Baseline → Improve → Verify loop
- Avoid format drift, hidden constraints, context dumping

---

## Verification

Each source was reviewed for:

1. Structural patterns (instructions first, delimiters, examples)
2. Context management (token reduction, specific prompts)
3. Verification and validation (self-check, tests, rubrics)
4. Workflow (explore→plan→code, decompose, chain)
5. Anti-patterns (vague goals, format drift, context dumping)

---

---

## Quarterly Refresh

| Cadence       | Action                                                            | Output                                                                  |
| ------------- | ----------------------------------------------------------------- | ----------------------------------------------------------------------- |
| **Quarterly** | Re-review LLM developer docs (Anthropic, OpenAI, Google, Copilot) | Update SOURCES_REVIEWED; propagate to SUPER_DEVELOPER_PRINCIPLES        |
| **Quarterly** | Search "prompt engineering 2025" (or current year)                | Capture to research/practices-YYYYMM.md                                 |
| **Quarterly** | Scan top repos (awesome-\*-prompts, AGENTS.md stars)              | Extract patterns; add to SOURCES_AND_EMULATION_INDEX                    |
| **Quarterly** | Run `./scripts/sources-compare-and-update.sh`                     | Compare vs external; update EXPERT_PROMPT_ENGINEERING, SOURCES_REVIEWED |

**Reminder**: Add to sync cadence or calendar. Run: `./scripts/sync-all-repos-and-review.sh` then manual review of SOURCES_REVIEWED.

---

_Maintain at: docs/SOURCES_REVIEWED.md. Re-review quarterly or when new major docs release._
