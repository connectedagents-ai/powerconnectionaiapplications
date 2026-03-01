---
name: beginner-guardrails
description: Safety and validation for beginners. Use when performing destructive operations (rm, force push, bulk delete), handling sensitive data (API keys, secrets, PII), or first-time use of a new tool/API. Requires confirmation before irreversible actions and validation before writing files.
---

# Beginner Guardrails

Use this skill when: destructive ops, sensitive data, first-time tool use, deployment, or overwriting production config.

## Destructive Operations

Before running: `rm -rf`, `delete`, bulk delete, `force push`, overwrite production, drop tables, revoke access

1. **State what will be removed/overwritten** — list impact
2. **Require explicit user confirmation** — do not proceed without "yes"
3. If user has not confirmed → pause and ask

## Sensitive Data

Never commit: API keys, tokens, passwords, `.env` (except `.env.example`), PII, private keys

Before commit: scan staged files for `api_key`, `secret`, `password`, `token`, `.env`

## Validation Before Write

- Read target file first
- Check existing patterns and conventions
- No duplicates when adding to lists/config
- Valid format for config/code

## First-Time Tool Use

- Explain what the tool does and how it will be used
- Wait for user approval before executing
- Describe any risks (e.g., rate limits, costs)

## Human Checkpoints

Pause and confirm for:

- Deployment to production
- Auth/permission changes
- Legal/compliance output
- Privileged or confidential data sharing

## Quick Reference

```
Destructive? → Confirm + list impact
Sensitive?   → Never commit
Before write → Read file, check patterns
First-time?  → Explain, wait for approval
```

See `developer-enhancement/GUARDRAILS.md` for full guide.
