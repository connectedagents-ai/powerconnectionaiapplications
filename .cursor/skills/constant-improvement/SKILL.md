---
name: constant-improvement
description: Lightweight constant improvement after prompts. Use after each significant prompt or task to capture one-line pattern (success) or anti-pattern (failure). Enables recursive improvement of agentic instructions. Do not run heavy research or multi-agent review—reserve those for weekly/monthly cadence. See developer-enhancement/CONTINUOUS_IMPROVEMENT.md for full protocol.
---

# Constant Improvement (Lightweight)

Use after each significant prompt to capture learnings without high cost or time.

## After Prompt — Lightweight Only

| Outcome                   | Action                                                           | Max Cost    |
| ------------------------- | ---------------------------------------------------------------- | ----------- |
| **Success + new pattern** | Append one line to `patterns-that-work.md`                       | 1 line      |
| **Failure**               | Append to `postmortems.log` or write `postmortem-{timestamp}.md` | Brief entry |
| **Inefficiency noticed**  | Add one row to anti-pattern list in rule                         | 1 row       |

**Do not** after every prompt:

- Full post-mortem
- Research (repos, LLMs)
- Multi-agent review
- Long explanation

Reserve those for weekly/monthly cadence (see CONTINUOUS_IMPROVEMENT.md).

## One-Line Capture Format

**Success**: `## YYYY-MM-DD — [Topic]: [what worked in 10 words]`
**Failure**: `## YYYY-MM-DD — [Topic]: [what failed]; fix: [one-line]`
**Anti-pattern**: `| [pattern] | [waste] | [alternative] |`

## Propagation

When adding anti-pattern: update `.cursor/rules/agent-efficiency-context.mdc` anti-pattern table.
When pattern is reused 3+ times: consider promoting to skill example or rule.

## Cadence Reminder

- **Weekly**: Consolidate lessons; sync instructions
- **Monthly**: Research one topic; multi-agent review 2 rules
- **Quarterly**: Audit instruction files; refresh CONTINUOUS_IMPROVEMENT.md

See `developer-enhancement/CONTINUOUS_IMPROVEMENT.md` for full protocol.
