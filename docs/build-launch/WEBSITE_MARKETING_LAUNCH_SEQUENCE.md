# Build Launch — Website Marketing Launch Sequence

**Purpose:** Define the **website and marketing launch sequence** so that go-live is consistent from **every perspective** (user, attorney, investor, partner, technical, compliance). **Top-level agents** expand and complete this sequence for each product/vertical and region as needed.

**Governance:** [constitution.md](../constitution.md); [LAUNCH_BLOG_SCHEDULE_WEBSITES_VOICE_AGENT_AND_SETUP.md](../LAUNCH_BLOG_SCHEDULE_WEBSITES_VOICE_AGENT_AND_SETUP.md); [PRE_LAUNCH_AND_PARTNER_PRESENTATIONS_VC_CLOUD_LEGAL_TECH.md](../PRE_LAUNCH_AND_PARTNER_PRESENTATIONS_VC_CLOUD_LEGAL_TECH.md).

---

## 1. Sequence overview

| Phase | When | What |
|-------|------|------|
| **Pre-launch** | 4–6 weeks before | Content calendar, domains configured, voice agent ready, disclaimer and pages in place, Full Review + checklist done. |
| **Launch week** | Go-live | Domains live; blog/PR; voice widget link in all CTAs; simulation disclaimer on every page. |
| **Post-launch** | Ongoing | Weekly/biweekly content; voice agent knowledge updated from real conversations; Build Launch docs updated by agents. |

---

## 2. Pre-launch (4–6 weeks before)

### 2.1 Content and blog (from LAUNCH_BLOG)

| Week | Post / asset | Audience | Channel |
|------|--------------|----------|---------|
| -6 | "Why One Desktop Beats a Dozen AI Tools" | End users, family | OneWish.io, TAKE_HOME |
| -5 | "The Operating System for Every Business" | Investors, partners | NextTech OS / Connected Agents |
| -4 | "From Intake to Case-Ready in 60 Minutes" | Attorneys, small firms | LitigationForce.AI, litigationforce.com |
| -3 | "161:1 — Why They Can't Outspend You" | Litigation buyers | LitigationForce.AI, talk.litigationforce.com |
| -2 | "Knowledge Graphs Beat Folders…" | Technical, legal ops | LitigationForce.AI, docs |
| -1 | "Launch Week: What's Live and How to Try It" | All | All sites + email |

### 2.2 Website setup

- **Domains (Vercel):** litigationforce.com, talk.litigationforce.com, smithwick.ai, talianventures.com, marketing.connectedagents.ai.
- **Pages (minimum):** Home, Why OneWish/Genie, Architecture/For Partners, LitigationForce product, Talk to Alex (voice), Login/App, Legal/Disclaimer, Contact.
- **Voice agent:** ElevenLabs agent created; system prompt from `marketing/voice-agent/agent-config.md`; widget deployed to talk.litigationforce.com (or marketing/voice-app).
- **Simulation disclaimer:** Visible on every public page and in-app: *"Litigation outputs are for litigation support only. Not legal advice. Attorney review required."*
- **SEO:** Meta titles/descriptions per page; Open Graph for talk.litigationforce.com: "Talk to Alex — LitigationForce.AI voice agent."
- **CTAs:** All relevant CTAs include link to talk.litigationforce.com.

### 2.3 Governance and verification

- Full Review passed; mandatory checklist in `docs/audits/full-review-summary.md` complete.
- Constitution and sync propagated (`route-constitution-to-repos.sh`, `sync-all-repos-and-review.sh`).
- Connections and secrets verified (Replit, Supabase, DB, vector, etc.) per LAUNCH_BLOG Part 4.
- Commit review and final decision (when master files changed) per `MASTER_FILE_COMMIT_REVIEW_AND_FINAL_DECISION_SYSTEM.md`.

---

## 3. Launch week

| Day | Post / asset | Audience | Channel |
|-----|--------------|----------|---------|
| **Mon** | "LitigationForce.AI Is Live" | Press, clients, investors | Blog + PR + LinkedIn |
| **Tue** | "Talk to Alex: Voice Agent for LitigationForce" | Prospects, demos | talk.litigationforce.com, blog |
| **Wed** | "OneWish + Genie Desktop: One Button, Your Whole World" | End users | OneWish.io |
| **Thu** | "NextTech OS: One User-Facing Layer for All Products" | Partners, enterprise | NextTech / Connected Agents |
| **Fri** | "Pre-Launch Checklist: What We Verified Before Flipping the Switch" | Technical, compliance | Blog / internal |

**Go-live checks:**

- All domains resolve; voice widget loads at talk.litigationforce.com.
- Disclaimer on every page; contact (rbailey@connectedagents.ai) and "Request a Demo" visible.
- Voice agent first message and tough-Q handling per [VOICE_AGENT_INSTRUCTIONS.md](VOICE_AGENT_INSTRUCTIONS.md) and [VOICE_AGENT_SEQUENCE.md](VOICE_AGENT_SEQUENCE.md).

---

## 4. Post-launch (ongoing)

| Cadence | Topic | Audience |
|---------|--------|----------|
| **Weekly** | Customer story or use case | Attorneys, firms |
| **Biweekly** | Technical deep-dive (one workflow or agent) | Dev, legal ops |
| **Monthly** | Platform / product update (agents, workflows, hardware) | All |
| **Quarterly** | Standards & compliance (ABA, EDRM, Sedona, ISO) | Compliance, risk |

**Voice agent:** Update knowledge base and escalation rules from real conversations; top-level agents add situational instructions per [VOICE_AGENT_SEQUENCE.md](VOICE_AGENT_SEQUENCE.md) and [VOICE_AGENT_INSTRUCTIONS.md](VOICE_AGENT_INSTRUCTIONS.md).

---

## 5. Variable / situational (expandable by top-level agents)

- **By product/vertical:** LitigationForce.AI (current); add Family Office, Lifestyle, PowerConnection with their own landing pages, CTAs, and voice-agent branches when launched.
- **By audience:** Ensure copy and CTAs speak to attorney, investor, enterprise, compliance on the right pages (see VOICE_AGENT_SEQUENCE §2.1 for parallel audience framing).
- **By region/legal:** If we launch in multiple jurisdictions, add region-specific disclaimers or compliance bullets and document in this sequence.

Top-level agents **expand** this section so the website marketing launch is **complete from every perspective** and stays aligned with Build Launch.

---

## 6. References

- **Full launch blog & setup:** [LAUNCH_BLOG_SCHEDULE_WEBSITES_VOICE_AGENT_AND_SETUP.md](../LAUNCH_BLOG_SCHEDULE_WEBSITES_VOICE_AGENT_AND_SETUP.md)
- **Voice agent instructions:** [VOICE_AGENT_INSTRUCTIONS.md](VOICE_AGENT_INSTRUCTIONS.md)
- **Voice agent sequence:** [VOICE_AGENT_SEQUENCE.md](VOICE_AGENT_SEQUENCE.md)
- **Pre-launch & partner (VC, legal tech):** [PRE_LAUNCH_AND_PARTNER_PRESENTATIONS_VC_CLOUD_LEGAL_TECH.md](../PRE_LAUNCH_AND_PARTNER_PRESENTATIONS_VC_CLOUD_LEGAL_TECH.md)
- **Build Launch entry:** [README.md](README.md)

---

_Simulation disclaimer: All litigation outputs are for litigation support only. Not legal advice. Attorney review required._
