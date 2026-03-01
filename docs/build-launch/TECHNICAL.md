# Build Launch — Technical Explanation

**Audience:** Technical readers (architects, platform engineers) who need architecture, data flow, and integration details.

**Governance:** [constitution.md](../constitution.md); [AGENTS_ROLES_SWARMS_AND_CONTINUOUS_LEARNING.md](../AGENTS_ROLES_SWARMS_AND_CONTINUOUS_LEARNING.md); [LAUNCH_BLOG_SCHEDULE_WEBSITES_VOICE_AGENT_AND_SETUP.md](../LAUNCH_BLOG_SCHEDULE_WEBSITES_VOICE_AGENT_AND_SETUP.md).

---

## 1. Build Launch — technical definition

**Build Launch** is the named control plane for:

1. **Build** — Product (LitigationForce.AI, OneWish OS), website(s), and voice agent: implementation, config, schemas, deployment pipelines.
2. **Launch** — Execution of two ordered sequences:
   - **Website marketing launch sequence:** Pre-launch → launch week → post-launch (domains, pages, content, CTAs, disclaimer).
   - **Voice agent sequence:** Core (every conversation) + situational/variable (by audience, topic, channel).
3. **Core every time** — Invariants: simulation disclaimer, voice agent first message and escalation rules, deployment checklist, Full Review gate.
4. **Variable/situational** — Instructions that depend on audience (attorney vs investor vs enterprise), topic (pricing, security, competitors), or channel (web widget, future phone/car). These are **expanded by top-level agents** so the system stays complete from every perspective.

---

## 2. Architecture — high-level

```
┌─────────────────────────────────────────────────────────────────────────┐
│                         BUILD LAUNCH                                     │
├─────────────────────────────────────────────────────────────────────────┤
│  Core (every time)          │  Variable (situational)                    │
│  • Disclaimer              │  • By audience (attorney, investor, …)     │
│  • Voice first message     │  • By topic (pricing, security, …)        │
│  • Escalation rules        │  • By channel (web, future: phone, etc.)   │
│  • Deployment checklist    │  • Expanded by top-level agents            │
│  • Full Review gate        │                                             │
├────────────────────────────┴────────────────────────────────────────────┤
│  Website marketing launch sequence                                       │
│  Pre-launch → Launch week (domains, pages, voice link, PR) → Post-launch │
├─────────────────────────────────────────────────────────────────────────┤
│  Voice agent sequence                                                    │
│  Greet → Qualify → Answer (from knowledge) → Capture contact → Escalate  │
│  + situational branches (tough Q, pricing, legal, competitor, etc.)      │
└─────────────────────────────────────────────────────────────────────────┘
         │                              │
         ▼                              ▼
┌─────────────────────┐      ┌─────────────────────┐
│  Artifacts          │      │  Integrations       │
│  • build-launch/    │      │  • ElevenLabs      │
│  • agent-config.md  │      │  • Vercel           │
│  • LAUNCH_BLOG_*    │      │  • Replit / Swarm   │
└─────────────────────┘      └─────────────────────┘
```

---

## 3. Data flow — voice agent

1. **User** → Browser (talk.litigationforce.com) → ElevenLabs widget → **STT** → agent logic (system prompt + knowledge from agent-config + Build Launch instructions).
2. **Agent** → Answer (and/or escalation path) → **TTS** → user.
3. **Contact capture** (when offered) → CRM/human follow-up (rbailey@connectedagents.ai or “we’ll have someone reach out”).
4. **No PII in logs** — Per compliance; escalation passes only what user consents to share.

Litigation-specific voice agents (Legal Scribe, Deposition Transcriber, Case Research Voice Assistant) are described in [modules/voice-agents.md](../modules/voice-agents.md); they share STT/NLP/TTS patterns but different intents and outputs (transcript, evidence linkage, LexVault).

---

## 4. Sequences — technical specification

### 4.1 Website marketing launch sequence

- **Inputs:** Config (domains, pages, content sources from LAUNCH_BLOG and WEBSITE_MARKETING_LAUNCH_SEQUENCE), deployment targets (Vercel, Replit).
- **Outputs:** Live domains, pages with disclaimer and CTAs, voice widget link in all relevant CTAs, SEO/OG tags.
- **Invariants:** Simulation disclaimer on every public and in-app view; no launch without Full Review and checklist completion.

### 4.2 Voice agent sequence

- **Core (state machine):** Greet → Qualify (what are you interested in?) → Answer (from CORE KNOWLEDGE + tough-Q table) → [Capture contact if relevant] → [Escalate if topic in escalation set].
- **Variables:** Response text and branching per audience/topic/channel; defined in VOICE_AGENT_INSTRUCTIONS and VOICE_AGENT_SEQUENCE; expanded by top-level agents.

---

## 5. Integration points

| System | Integration with Build Launch |
|--------|-------------------------------|
| **ElevenLabs** | Agent ID, system prompt (from agent-config.md), first message; widget embed in marketing/voice-agent or marketing/voice-app. |
| **Vercel** | Deploy marketing/voice-app and main sites; env (e.g. NEXT_PUBLIC_*); domains in dashboard. |
| **Constitution / Full Review** | Build Launch is subject to constitution §6.6 (every-response suggestions), Full Review checklist, and commit review and final decision when master files change. |
| **Sync script** | sync-all-repos-and-review.sh can include build-launch docs in idxdoc so child repos receive updates. |
| **CRM / contact** | Escalation path: email (rbailey@connectedagents.ai) or “have someone reach out”; future: structured contact payload to CRM. |

---

## 6. Variables and extension points

- **Audience:** attorney, investor, enterprise, compliance, “average Joe” — each can have tailored opening or answer set (documented in VOICE_AGENT_INSTRUCTIONS / VOICE_AGENT_SEQUENCE).
- **Topic:** pricing, security, competitors, legal/ethics, “is it built?”, ROI — each has suggested answer and escalation rule (see LAUNCH_BLOG Part 3.2).
- **Channel:** web widget (current); future: phone, in-car, wearable — each may have different core message length or escalation path.
- **Product/vertical:** LitigationForce.AI (current); future: Family Office, Lifestyle, PowerConnection — Build Launch can be extended with product-specific launch steps and voice agent branches.

Top-level agents **read** these extension points and **write** concrete instructions and branches so that every perspective is covered and the voice agent / website launch stay aligned with Build Launch.

---

## 7. References

| Doc | Content |
|-----|---------|
| [README.md](README.md) | Build Launch definition, audience index, expansion by top-level agents |
| [VOICE_AGENT_INSTRUCTIONS.md](VOICE_AGENT_INSTRUCTIONS.md) | Conversations, troubleshooting, escalation |
| [VOICE_AGENT_SEQUENCE.md](VOICE_AGENT_SEQUENCE.md) | Core + situational sequence; expansion points |
| [WEBSITE_MARKETING_LAUNCH_SEQUENCE.md](WEBSITE_MARKETING_LAUNCH_SEQUENCE.md) | Pre-launch, launch week, post-launch steps |
| [modules/voice-agents.md](../modules/voice-agents.md) | Legal Scribe, Deposition, Case Research voice agents; STT/NLP pipeline |

---

_Simulation disclaimer: All litigation outputs are for litigation support only. Not legal advice. Attorney review required._
