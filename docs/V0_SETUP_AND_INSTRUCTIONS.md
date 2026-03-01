# v0 Setup & Instructions — litigationforc1 v02 / LitigationForce.AI

> **Purpose**: Detailed rules and settings for v0 by Vercel when building litigationforc1 v02 UI components, aligned with LitigationForce.AI constitution, ABA/EDRM/Sedona, and agent-efficiency practices.

---

## 1. v0 Preference Settings (Recommended)

Configure v0 project preferences as follows:

| Setting                 | Recommendation                            | Rationale                                                 |
| ----------------------- | ----------------------------------------- | --------------------------------------------------------- |
| **Suggestions**         | On                                        | Refinement prompts improve component quality              |
| **Sound Notifications** | On (if multitasking) / Off (focused flow) | Avoid context switching when deep in UI work              |
| **Chat Position**       | Left                                      | Keeps code visible alongside chat                         |
| **Custom Instructions** | Paste content from §2 below               | Ensures litigation context in every v0 chat               |
| **Theme**               | Dark (litigation work) / System           | Reduces eye strain during long sessions                   |
| **Language**            | English                                   | Matches LitigationForce.AI docs and ABA/legal terminology |

---

## 2. Custom Instructions (Copy to v0 — 0 / 2000 chars)

Paste the following into v0 **Custom Instructions** (within 2000 chars):

```
Project: litigationforc1 v02 — LitigationForce.AI UI components.

Context: Build React/Next.js UI for litigation case management, e-discovery, and legal workflows. Align with LitigationForce.AI constitution and ABA/EDRM/Sedona standards.

Prompt rules:
- One component or flow per request. Use "Build X with Y" over long descriptions.
- Reference design by URL or path when context is limited.
- Human-in-the-loop: UI must include attorney review checkpoints for privilege, productions, filings.
- Simulation disclaimer: Add "Draft for attorney review. Not legal advice." to outputs used in legal context.
- Claim typing: Fact/Inference/Opinion tags on any legal assertions in UI copy.
- Use Tailwind, shadcn/ui. Match existing litigationforce.ai design tokens.

Efficiency: Execute immediately. Persist to project files. One task per message.
```

**Character count**: ~650 — leaves room for project-specific additions.

---

## 3. Expanded Custom Instructions (If Under 2000 chars)

Use this if you need more detail and stay under 2000 characters:

```
Project: litigationforc1 v02 — LitigationForce.AI UI components.

Context: Build React/Next.js UI for litigation case management, e-discovery, early case assessment, RICO/multi-forum workflows. Align with LitigationForce.AI constitution, ABA Model Rule 1.1, EDRM TAR, Sedona AI Commentary.

Prompt rules:
1. One component or flow per request. Prefer "Build X with Y" over long descriptions.
2. Reference design/context by URL or Figma path when available.
3. Human-in-the-loop: Include attorney review checkpoints for privilege determinations, productions, filings, damages conclusions.
4. Simulation disclaimer: Add "Draft for attorney review. Not legal advice." to outputs used in legal proceedings.
5. Claim typing: Every legal assertion tagged as FACT/INFERENCE/OPINION/LEGAL_CONCLUSION in UI.
6. Stack: Tailwind, shadcn/ui, Next.js. Match litigationforce.ai design system.

Standards: ABA 1.1 (tech competence), EDRM (transparency, explainability), Sedona (human oversight, bias evaluation).

Efficiency: Execute immediately. Persist to project. One task per message. Verify once.
```

---

## 4. v0 Capability Rules (Per LitigationForce.AI)

| Capability               | Rule                                                                                                                         |
| ------------------------ | ---------------------------------------------------------------------------------------------------------------------------- |
| **Component generation** | One component per prompt. Specify: purpose, props, accessibility, litigation use case.                                       |
| **Multi-step flows**     | Break into steps. Request Step 1 first; reference prior output for Step 2.                                                   |
| **Legal copy / labels**  | Use claim typing: FACT (evidence-backed), INFERENCE, OPINION, LEGAL_CONCLUSION. Avoid unqualified legal conclusions.         |
| **Review checkpoints**   | Any UI that triggers privilege, production, or filing workflows must include "Attorney review required" and confirmation UI. |
| **Design consistency**   | Reference `litigationforce.ai` or Figma for tokens. Use shadcn/ui patterns where applicable.                                 |
| **Error states**         | Show simulation disclaimer and retry when AI output could affect legal decisions.                                            |

---

## 5. Relation to LitigationForce.AI Repo

| LitigationForce.AI artifact             | v0 usage                                                         |
| --------------------------------------- | ---------------------------------------------------------------- |
| `docs/constitution.md`                  | Human-in-loop, claim typing, simulation disclaimer               |
| `.github/agents/my-agent.agent.md`      | Standards (ABA/EDRM/Sedona), vendor inventory, multi-agent roles |
| `docs/NEW_CAPABILITY_CHECKLIST.md`      | When adding new UI capability: skill, index update               |
| `docs/standards-compliance.md`          | Compliance checklist for UI that touches legal workflows         |
| `agent-efficiency/AGENTS_EFFICIENCY.md` | One task per message, persist early, minimal prompts             |
| `agent-efficiency/TOOL_INTEGRATION.md`  | v0-specific: minimal focused prompts, reference by path          |

---

## 6. Sync with Cursor / Claude / Other Tools

v0 outputs (components, flows) should be:

1. **Synced to LitigationForce.AI** — Commit to repo per `scripts/sync-all-repos-and-review.sh`
2. **Documented** — Add to `docs/` or `examples/bundle/` if reusable
3. **Skills** — If a pattern is repeated, create `.cursor/skills/{name}/SKILL.md` per `create-skill`
4. **Indexes** — Update `agents/MASTER_AGENT_INDEX.md` for new UI agents or patterns

---

## 7. Quick Reference (Copy-Paste for v0 Chats)

When starting a v0 session:

```
Build [component name] for [litigation use case]. Use Tailwind + shadcn/ui. Include attorney review checkpoint. Add simulation disclaimer. One component.
```

For refinements:

```
Refine [component]: [specific change]. Keep existing [aspect].
```

---

_Referenced by: constitution.md, UNIVERSAL_INSTRUCTIONS.md, DEV_TOOLS_RULES_SETUP.md, agent-efficiency/TOOL_INTEGRATION.md_
