---
name: efficient-context-management
description: Prevents context overload and agent inefficiency. Use when agents hit context limits, repeat intent without action, get stuck in verification loops, waste tokens on meta-commentary, or fail to persist data. Apply for DevOps, MCP/API work, multi-tool setup, and long-running tasks. Includes self-correction: before executing any plan, check for inefficiency and refactor scope/steps if needed.
---

# Efficient Context Management

Use this skill when you observe or risk: context overload, repeated "I'll do X now" without action, verification loops, excessive todo updates, or lost work from context compaction.

## Core Rules

1. **Execute, don't announce** — Never say "I'll create X now" without creating it. If blocked, one-line explanation.
2. **Persist early** — Write outputs to disk immediately. Paths: `{dir}/raw/{name}.json`, `plan-{topic}.md`.
3. **Scope narrowly** — One task per message. For multi-part requests: do first task, persist, then continue.
4. **Verify once** — No verification loops. Verify once, then proceed.
5. **Todo sparingly** — Update task lists only when status meaningfully changes.
6. **API/MCP efficiency** — Paginate (limit 10–25), minimal fields, cache to files, reference files instead of re-querying.

## Persistence Protocol

| When            | Action                                      |
| --------------- | ------------------------------------------- |
| After fetch     | `write {output_dir}/raw/{resource}.json`    |
| After design    | `write plan-{topic}.md` or `structure.json` |
| Before long ops | Write in-progress marker; remove when done  |
| On error        | Write `error-{timestamp}.json` with context |

## Self-Correction (Before Executing Plans)

Before executing any plan, check and refactor if the plan shows:

- 4+ tasks in one plan → Split into steps; execute step 1 only
- No output path → Add file path; write there first
- Broad API query → Scope to one resource; paginate
- Re-fetch of data on disk → Use "read from `path`" instead
- Verify/validate in loop → Single verification at end
- Intent without action → Replace with concrete first action

Refactor silently. Execute first step. Persist. Continue.

## Anti-Pattern Checklist

Before replying, avoid:

- [ ] Announcing intent without immediately acting
- [ ] Updating todos without status change
- [ ] Re-verifying completed steps
- [ ] Re-fetching data already in files
- [ ] Long meta-commentary ("Let me continue...", "I'll pick up...")
- [ ] Broad API queries (all teams + projects + issues); paginate and split

## Prompt Design (User-Facing)

When helping users structure requests:

- One task per message
- Specify output path
- Reference prior files instead of re-requesting data
- Break large asks into ordered steps

## Quick Reference

```
Check plan → Refactor if inefficient → Execute first step → Persist → One task → Verify once → Todo sparingly → Paginate APIs
```

## Recursive Improvement

- On failure → `postmortem-{date}.md` (what failed, cause, fix, suggested rule)
- At session end → append to `lessons.md` (do more, do less, rule to add)
- When noticing new waste → add to anti-pattern list
- When workflow works → append to `patterns-that-work.md`

For full rules: `AGENTS_EFFICIENCY.md`
