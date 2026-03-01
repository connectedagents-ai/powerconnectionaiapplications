---
name: recursive-improvement
description: Virtuous loops for agent optimization. Use after failures (post-mortem), at session end (lessons), when a workflow succeeds (pattern capture), or when noticing new waste (anti-pattern accretion). Turns failures into rules and success into reusable patterns.
---

# Recursive Improvement

Use when: something failed, session is ending, a workflow worked well, or you notice new waste.

## Post-Mortem (On Failure)

Write `postmortem-{YYYYMMDD-HHmm}.md`:

```markdown
## What failed

[One paragraph]

## Cause

[Root cause]

## Fix applied / Next step

[What you did or will do]

## Suggested rule/skill update

[Concrete addition to avoid repeat]
```

## Lessons (At Session End)

Append to `lessons.md`:

```markdown
## YYYY-MM-DD

- **Do more**: [pattern that worked]
- **Do less**: [pattern that wasted]
- **Rule to add**: [optional]
```

## Patterns That Work (On Success)

Append to `patterns-that-work.md`:

```markdown
## [Topic] — YYYY-MM-DD

- **What**: [brief description]
- **Why it worked**: [reason]
- **Reuse when**: [trigger]
```

## Anti-Pattern Accretion (When Noticing Waste)

Add to `.cursor/rules/agent-efficiency-context.mdc` anti-pattern table:

`| [pattern] | [waste] | [alternative] |`

Or propose: "Add anti-pattern: X → Y"

## Virtuous Loops

- **Failure → Rules**: Post-mortem → add rule → fewer repeats
- **Success → Patterns**: Append to patterns-that-work → reuse
- **Session → Lessons**: Append to lessons → next session benefits
- **Waste → Anti-Pattern**: Add to list → agent avoids it

## Quick Reference

```
Failure  → postmortem-{date}.md
Session  → append lessons.md
Success  → append patterns-that-work.md
New waste → add anti-pattern
```

See `developer-enhancement/RECURSIVE_IMPROVEMENT.md` for full guide.

**Constant improvement**: For shared instructions, automated sync, multi-agent review, and cadenced research — see `developer-enhancement/CONTINUOUS_IMPROVEMENT.md`.
