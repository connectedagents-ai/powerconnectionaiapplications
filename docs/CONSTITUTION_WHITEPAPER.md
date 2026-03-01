# AI Constitution for Legal Workflows — A Governance Model for Production AI

> **Whitepaper** | Connected Agents.AI | 2026
>
> How we govern AI outputs in litigation and discovery to achieve defensibility, explainability, and attorney supervision.

---

## Executive Summary

Legal AI must be more than accurate—it must be **defensible**. Courts, regulators, and clients demand transparency, human oversight, and auditability. This whitepaper describes our **Constitution** model: a set of non-negotiable principles that every AI agent and output must follow. The result is production-grade legal AI that attorneys can trust and defend.

---

## 1. The Problem

Legal AI faces unique challenges:

- **Privilege and confidentiality** — One misclassification can waive privilege or breach confidentiality
- **Fact vs. inference** — Assertions must be typed; evidence must be cited
- **Regulatory alignment** — ABA Model Rule 1.1, EDRM, Sedona 2023, ISO/IEC 42001
- **Liability** — AI outputs presented as legal advice create risk; disclaimers and human review are mandatory

Generic AI lacks the guardrails needed for legal work. We need **governance by design**, not by retrofit.

---

## 2. The Constitution Model

Our Constitution has six pillars:

### 2.1 Human-in-the-Loop Checkpoints

High-stakes outputs **never** auto-approve. Privilege determinations, filings, productions, expert narratives, damages conclusions, and compliance determinations route through a human checkpoint. The system prompts for attorney sign-off by name or role.

### 2.2 Claim Typing

Every assertion carries a type: **FACT** (cited evidence), **INFERENCE** (logically derived), **OPINION** (expert judgment), **LEGAL_CONCLUSION** (legal standard application). FACT claims require an evidence pointer and quoted excerpt—or explicit UNVERIFIED. Each type routes to a corresponding quality gate.

### 2.3 Explainability & Audit

Prompts, tool calls, parameters, outputs, and evaluator results are preserved. Every transformation has an immutable audit trail: stage, agent, timestamp, input_hash, output_hash. This supports EDRM, Sedona, and ISO/IEC 42001 requirements.

### 2.4 Bias & Safety

Outputs are evaluated for bias and harmful content. Mitigations are documented. Sensitive inferences require attorney review. ABA Standard 303 (professional identity, bias awareness) is respected.

### 2.5 Simulation Disclaimer

All litigation outputs are drafts for support only. Not legal advice. Attorney review required before use in legal proceedings. This disclaimer appears on every generated document.

### 2.6 New Capability Flow

When adding tools, agents, or skills: read constitution first, create skill, use ontology, update indexes, emulate reference patterns. A full checklist ensures no governance gap.

---

## 3. The Evaluator Swarm

Before any output reaches a human reviewer, it passes four gates:

| Gate               | Target      | Purpose                                 |
| ------------------ | ----------- | --------------------------------------- |
| Fact Checker       | ≥90%        | Claims verified against source evidence |
| Citation Validator | ≥95%        | Legal citations valid and current       |
| Logic Auditor      | ≥85%        | Reasoning chains free of fallacies      |
| Ethics Reviewer    | ≥98% recall | Privilege risks, bias, ethical concerns |

**All must pass.** Max 3 remediation loops. Then escalate to human. This aligns with Sedona 2023: human oversight, adversarial disclosure, bias evaluation.

---

## 4. Implementation

The Constitution is implemented as:

- **docs/constitution.md** — Single source of truth
- **Route propagation** — Synced to all platform repos via `route-constitution-to-repos.sh`
- **Entry points** — AGENTS.md, CLAUDE.md, my-agent.agent.md reference it
- **Pre-execution checklist** — 110+ checks ensure compliance before acting

---

## 5. Impact

- **Defensibility** — Audit trail supports "what did the AI do and why?"
- **Compliance** — ABA, EDRM, Sedona, ISO aligned
- **Attorney control** — No high-stakes output without human approval
- **Quality** — Claim typing and Evaluator Swarm gate unreliable outputs

---

## 6. Conclusion

An AI Constitution is not optional for legal workflows—it is foundational. By encoding governance as a living document, routing it to every repo, and enforcing it through checkpoints and gates, we achieve production-grade legal AI that attorneys can trust and defend.

---

_Connected Agents.AI — The operating system for every business. Private-first. Voice-native. Agent-evaluated._
