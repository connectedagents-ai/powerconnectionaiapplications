# Build Launch — Full Developer Docs

**Audience:** Developers implementing or extending Build Launch (website, voice agent, launch sequences, scripts).

**Governance:** [constitution.md](../constitution.md); [LAUNCH_BLOG_SCHEDULE_WEBSITES_VOICE_AGENT_AND_SETUP.md](../LAUNCH_BLOG_SCHEDULE_WEBSITES_VOICE_AGENT_AND_SETUP.md); [marketing/voice-agent/agent-config.md](../../marketing/voice-agent/agent-config.md).

---

## 1. Build Launch overview (developer)

**Build Launch** = Named framework for:

- **Product/website/voice agent** build and launch from every perspective.
- **Core sequence** (run every launch): checklist, deployment, disclaimer, voice agent first message and escalation.
- **Situational/variable** instructions (by audience, topic, channel) **expanded by top-level agents**.

Artifacts:

| Artifact | Path / location |
|----------|------------------|
| Build Launch docs | `docs/build-launch/` (this folder) |
| Voice agent config (ElevenLabs) | `marketing/voice-agent/agent-config.md` |
| Voice app (Next.js) | `marketing/voice-app/` |
| Static voice widget | `marketing/voice-agent/` (index.html + widget) |
| Launch blog & setup | `docs/LAUNCH_BLOG_SCHEDULE_WEBSITES_VOICE_AGENT_AND_SETUP.md` |
| Voice agents module | `docs/modules/voice-agents.md` |
| Platform connections | `config/platform-connections.yaml` |
| Repos / sync | `config/repos.yaml`; `scripts/sync-all-repos-and-review.sh` |

---

## 2. Voice agent — tech stack and config

### 2.1 ElevenLabs

- **Product:** Conversational AI agent (Alex — marketing).
- **Create:** https://elevenlabs.io/conversational-ai
- **Config:** Name, voice (e.g. Rachel/Adam), language (English), first message, **system prompt** from `marketing/voice-agent/agent-config.md`.
- **Widget:** Embed in `marketing/voice-agent/index.html` or `marketing/voice-app/`; set agent ID (replace `REPLACE_WITH_MARKETING_AGENT_ID`).

### 2.2 Deployment targets

| Target | Use |
|--------|-----|
| **talk.litigationforce.com** | Primary voice widget (static or Next.js from `marketing/voice-app/`) |
| **marketing.connectedagents.ai** | Alternate host for voice widget |

### 2.3 Scripts and automation

- **Sync/propagation:** `scripts/sync-all-repos-and-review.sh` — ensure Build Launch docs and voice-agent references are in `idxdoc` if they should propagate to child repos.
- **Full Review (pre-launch):** `scripts/run-full-review.sh`; mandatory checklist in `docs/audits/full-review-summary.md` (includes commit review and final decision).
- **Validation:** Schema validation, connection checks per [LAUNCH_BLOG_SCHEDULE_WEBSITES_VOICE_AGENT_AND_SETUP.md](../LAUNCH_BLOG_SCHEDULE_WEBSITES_VOICE_AGENT_AND_SETUP.md) Part 4.

---

## 3. Website and marketing launch — developer checklist

1. **Domains (Vercel):** litigationforce.com, talk.litigationforce.com, smithwick.ai, talianventures.com, marketing.connectedagents.ai as configured.
2. **Voice widget:** Deploy `marketing/voice-agent/` or `marketing/voice-app/` to talk.litigationforce.com; agent ID and env (if any) set.
3. **Simulation disclaimer:** Present on every public page and in-app: *"Litigation outputs are for litigation support only. Not legal advice. Attorney review required."*
4. **SEO:** Meta titles/descriptions, Open Graph for talk.litigationforce.com ("Talk to Alex — LitigationForce.AI voice agent").
5. **CTAs:** All launch CTAs include link to talk.litigationforce.com where appropriate.

See [WEBSITE_MARKETING_LAUNCH_SEQUENCE.md](WEBSITE_MARKETING_LAUNCH_SEQUENCE.md) for full sequence and [VOICE_AGENT_SEQUENCE.md](VOICE_AGENT_SEQUENCE.md) for voice-agent flow.

---

## 4. Voice agent instructions — where they live

- **System prompt and core knowledge:** `marketing/voice-agent/agent-config.md` (paste into ElevenLabs).
- **Conversations, troubleshooting, escalation:** [VOICE_AGENT_INSTRUCTIONS.md](VOICE_AGENT_INSTRUCTIONS.md).
- **Tough questions and escalation table:** [LAUNCH_BLOG_SCHEDULE_WEBSITES_VOICE_AGENT_AND_SETUP.md](../LAUNCH_BLOG_SCHEDULE_WEBSITES_VOICE_AGENT_AND_SETUP.md) Part 3.2–3.3.
- **Core + situational sequence:** [VOICE_AGENT_SEQUENCE.md](VOICE_AGENT_SEQUENCE.md).

When **top-level agents** add or change instructions, update:

1. `marketing/voice-agent/agent-config.md` (if system prompt / knowledge changes).
2. [VOICE_AGENT_INSTRUCTIONS.md](VOICE_AGENT_INSTRUCTIONS.md) (conversation rules, troubleshooting, escalation).
3. [VOICE_AGENT_SEQUENCE.md](VOICE_AGENT_SEQUENCE.md) (core steps, situational branches).
4. ElevenLabs dashboard (re-paste system prompt if changed).

---

## 5. Expansion points for top-level agents

Top-level agents (orchestrator, platform-architect, marketing/launch owners) should:

1. **Complete core** — Ensure every step in [VOICE_AGENT_SEQUENCE.md](VOICE_AGENT_SEQUENCE.md) (core) and [WEBSITE_MARKETING_LAUNCH_SEQUENCE.md](WEBSITE_MARKETING_LAUNCH_SEQUENCE.md) is executable (no undefined placeholders for critical path).
2. **Add situational instructions** — Per audience (attorney, investor, enterprise, compliance), topic (pricing, security, competitors), channel (web, phone, future channels); document in VOICE_AGENT_INSTRUCTIONS and VOICE_AGENT_SEQUENCE.
3. **Sync to voice agent** — Push new knowledge/instructions into agent-config and ElevenLabs so the live agent reflects Build Launch.
4. **Update launch sequence** — Add or refine website/marketing steps and copy for each perspective; keep WEBSITE_MARKETING_LAUNCH_SEQUENCE and related runbooks in sync.

---

## 6. APIs and integrations (reference)

- **ElevenLabs:** Conversational AI API / widget — see ElevenLabs docs; agent ID in env or widget config.
- **Vercel:** Deploy via Git or CLI; env vars per project (e.g. `VERCEL_TOKEN` in platform-connections).
- **Litigation Swarm / Replit:** See [LAUNCH_BLOG_SCHEDULE_WEBSITES_VOICE_AGENT_AND_SETUP.md](../LAUNCH_BLOG_SCHEDULE_WEBSITES_VOICE_AGENT_AND_SETUP.md) Part 4 (connections, Replit UI ↔ engine).

---

## 7. Cross-references

| Topic | Document |
|-------|----------|
| Build Launch entry | [README.md](README.md) |
| Investor presentation slide(s) | [INVESTOR_SLIDES.md](INVESTOR_SLIDES.md) (what it does, why game changer, how it fits OneWish OS / NextTech OS / repos / agents / features / functions; all perspectives) |
| Executive / Average Joe / Technical | [EXECUTIVE.md](EXECUTIVE.md), [AVERAGE_JOE.md](AVERAGE_JOE.md), [TECHNICAL.md](TECHNICAL.md) |
| Voice agent instructions | [VOICE_AGENT_INSTRUCTIONS.md](VOICE_AGENT_INSTRUCTIONS.md) |
| Voice agent sequence | [VOICE_AGENT_SEQUENCE.md](VOICE_AGENT_SEQUENCE.md) |
| Website marketing launch | [WEBSITE_MARKETING_LAUNCH_SEQUENCE.md](WEBSITE_MARKETING_LAUNCH_SEQUENCE.md) |
| Launch blog & setup (full) | [LAUNCH_BLOG_SCHEDULE_WEBSITES_VOICE_AGENT_AND_SETUP.md](../LAUNCH_BLOG_SCHEDULE_WEBSITES_VOICE_AGENT_AND_SETUP.md) |
| Voice agents module | [modules/voice-agents.md](../modules/voice-agents.md) |
| Pre-launch & partner | [PRE_LAUNCH_AND_PARTNER_PRESENTATIONS_VC_CLOUD_LEGAL_TECH.md](../PRE_LAUNCH_AND_PARTNER_PRESENTATIONS_VC_CLOUD_LEGAL_TECH.md) |

---

_Simulation disclaimer: All litigation outputs are for litigation support only. Not legal advice. Attorney review required._
