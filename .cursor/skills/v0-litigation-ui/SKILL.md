---
name: v0-litigation-ui
description: Use when building litigation UI with v0 by Vercel (litigationforc1 v02). Includes Custom Instructions, attorney checkpoints, simulation disclaimer, claim typing. Applies to v0 projects for LitigationForce.AI.
---

# v0 Litigation UI — litigationforc1 v02

When building litigation case management, e-discovery, or legal workflow UI with **v0 by Vercel**:

## Full Setup

Read **`docs/V0_SETUP_AND_INSTRUCTIONS.md`** for:
- Custom Instructions to paste into v0 (2000 char max)
- Recommended v0 preference settings
- Capability rules (one component per prompt, attorney checkpoints, claim typing)
- Quick-reference prompts

## When to Use

- User mentions **v0**, **litigationforc1**, **litigationforce UI**, or Vercel v0
- Building React/Next.js components for litigation, e-discovery, RICO, case management
- User asks for v0 setup or Custom Instructions

## Quick Rules

1. **One component per prompt** — Request "Build X with Y" not multi-step flows in one message.
2. **Attorney checkpoints** — Any UI touching privilege, productions, or filings must include "Attorney review required."
3. **Simulation disclaimer** — Add "Draft for attorney review. Not legal advice." for legal outputs.
4. **Claim typing** — Tag legal assertions as FACT/INFERENCE/OPINION/LEGAL_CONCLUSION in UI copy.
5. **Stack** — Tailwind, shadcn/ui, Next.js. Match litigationforce.ai design tokens.

## Copy-Paste for v0 Custom Instructions

Paste into v0 Preferences → Custom Instructions (see `docs/V0_SETUP_AND_INSTRUCTIONS.md` §2 for full text).

## Platform

Constitution applies. Read `docs/constitution.md` first. New capabilities: `docs/NEW_CAPABILITY_CHECKLIST.md`.
