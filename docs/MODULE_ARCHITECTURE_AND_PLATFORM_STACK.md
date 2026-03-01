# Module Architecture & Platform Stack — Connected Agents.AI

> **Purpose**: Reiterate and fine-tune module architecture across all Connected Agents apps (connectedagents.ai, LitigationForce.AI, etc.); define methodology for selecting top Vercel/v0 modules and packages; incorporate design, graphics, colors, and experiences from repo instructions and industry best practices; align with constitution, ABA/EDRM/Sedona, and platform integrations.

**Referenced by**: constitution, REFERENCE_PATTERNS_AND_EXAMPLE_REPOS, litigation-swarm-ui, FUNDAMENTAL_STRATEGIES, V0_SETUP_AND_INSTRUCTIONS

---

## 1. Module Architecture — All Apps

### 1.1 Canonical Module Map

All Connected Agents apps (LitigationForce.AI, Power Connection, CES, NZL, connected-agents-platform) inherit and extend this module map:

| Layer             | Modules                                                                               | Purpose                               | Location / Reference                                                                              |
| ----------------- | ------------------------------------------------------------------------------------- | ------------------------------------- | ------------------------------------------------------------------------------------------------- |
| **Core Platform** | Orchestrator, MCP Server, Knowledge Graph (Neo4j), Ontology, Private LLM, Eval Engine | Routing, tools, schema, inference, QA | `docs/modules/`, agent-os archives                                                                |
| **Agent Types**   | Deterministic, Expert Dynamic, Voice, Orchestrator                                    | Agent taxonomy, playbooks             | `docs/FUNDAMENTAL_STRATEGIES.md` §1                                                               |
| **Interfaces**    | LexVault, Litigation Swarm UI, Video Chat, Avatars, Dashboards                        | File system, web app, voice, visual   | `docs/modules/lexvault.md`, `docs/modules/litigation-swarm-ui.md`, `docs/modules/voice-agents.md` |
| **Integrations**  | MCP (Notion, Linear, GitHub, Supabase, Figma, etc.), APIs, Connectors                 | Tool registry, OAuth, env vars        | `docs/MASTER_MCP_CONNECTORS_APIS.md`, `config/connectors.yaml`                                    |
| **Design System** | Tokens, typography, components, accessibility                                         | Visual identity, WCAG 2.1 AA          | `docs/FUNDAMENTAL_STRATEGIES.md` §4–5, `docs/modules/litigation-swarm-ui.md`                      |

### 1.2 Module Inheritance by Repo

| Repo                          | Inherits                      | Adds                                                            |
| ----------------------------- | ----------------------------- | --------------------------------------------------------------- |
| **connected-agents-platform** | Core, Ontology, MCP, Voice    | Platform economics, vertical modules, marketing                 |
| **LitigationForce.AI**        | All above                     | LexVault, RICO ontology, litigation agents, litigation-swarm-ui |
| **Power Connection**          | Core, MCP                     | Power-ai chat, OpenRouter, private LLM                          |
| **CES / NZL**                 | Core, MCP                     | Quote engine, portal, lending workflows                         |
| **slack-agent-template**      | Bootstrap rules, constitution | Nitro Slack agents, template patterns                           |

### 1.3 Fine-Tuning Principles

- **Single-responsibility** — One module = one domain (file, ontology, UI, voice, connector)
- **Schema-first** — Define in `docs/schemas/` before implementation
- **Skill-per-capability** — Add `.cursor/skills/{name}/SKILL.md` when creating new modules
- **Constitution alignment** — Human-in-loop, claim typing, audit, simulation disclaimer on all outputs

---

## 2. Vercel & v0 Module Selection Methodology

### 2.1 Selection Criteria

When choosing Vercel/v0 modules and packages for any Connected Agents app:

| Criterion                   | Weight   | Check                                                                           |
| --------------------------- | -------- | ------------------------------------------------------------------------------- |
| **Constitution compliance** | Required | Human-in-loop, audit trail, simulation disclaimer support                       |
| **Design system match**     | High     | Tokens in `FUNDAMENTAL_STRATEGIES` §4; dark-mode first; litigation color coding |
| **Accessibility**           | Required | WCAG 2.1 AA; keyboard nav; screen reader support                                |
| **AI / agent integration**  | High     | Composable with MCP, streaming, structured output                               |
| **Voice agent readiness**   | Medium   | ElevenLabs, STT/TTS, real-time streaming compatible                             |
| **Modern stack**            | High     | Next.js App Router, React Server Components, Tailwind, TypeScript               |
| **Industry adoption**       | Medium   | Top repos, v0 community, shadcn ecosystem                                       |

### 2.2 Recommended Top Modules (With Optionality)

| Category          | Primary               | Optional / Alternative           | Use When                         |
| ----------------- | --------------------- | -------------------------------- | -------------------------------- |
| **UI components** | shadcn/ui             | Radix UI primitives, Headless UI | All apps; shadcn = default       |
| **Charts**        | Recharts              | D3.js, vis.js                    | Dashboards, damages, RICO scores |
| **Graph viz**     | react-force-graph     | vis.js, Cytoscape                | Knowledge graph, enterprise map  |
| **Timeline**      | vis-timeline          | Custom React, react-chrono       | Litigation timelines             |
| **Auth**          | Supabase Auth         | NextAuth, Clerk                  | Magic link; RBAC                 |
| **Forms**         | React Hook Form + Zod | Formik                           | Validation, schema alignment     |
| **Tables**        | TanStack Table        | shadcn DataTable                 | Document lists, case tables      |
| **AI chat**       | Vercel AI SDK         | LangChain.js, custom             | Streaming, tool use              |
| **Voice**         | ElevenLabs            | Whisper, Deepgram                | Legal Scribe, deposition         |
| **Dashboards**    | Custom + Recharts     | Hex-style patterns               | Case KPI, agent status           |

### 2.3 v0-Specific Selection

For **v0 by Vercel** (litigationforc1 v02, etc.):

- Prefer **v0 community components** that match litigation-swarm design tokens
- Use **"Build X with Tailwind + shadcn/ui"** prompts; reference `docs/V0_SETUP_AND_INSTRUCTIONS.md`
- Mirrors: landing pages, dashboards, data tables, document viewers, RICO analysis UI
- Optionality: v0 templates vs. hand-built; choose per project scope and timeline

### 2.4 Config: Module Selection Registry

Create or extend `config/module-selection.yaml`:

```yaml
# config/module-selection.yaml — Vercel/v0 module choices with optionality
modules:
  ui:
    primary: shadcn/ui
    optional: [radix-ui, headless-ui]
  charts: [recharts, d3, vis]
  auth: [supabase-auth, nextauth, clerk]
  ai:
    primary: vercel-ai-sdk
    optional: [langchain-js, openai-sdk]
  voice:
    primary: elevenlabs
    optional: [whisper, deepgram]
  design_tokens: docs/FUNDAMENTAL_STRATEGIES_AND_SPECIFICATIONS.md
  v0_instructions: docs/V0_SETUP_AND_INSTRUCTIONS.md
```

---

## 3. Design, Graphics, Colors, Experiences

### 3.1 Canonical Design Tokens (Connected Agents / Litigation)

| Token                  | Hex       | Use                         |
| ---------------------- | --------- | --------------------------- |
| **Primary background** | `#0A0E27` | Dark navy; app background   |
| **Accent cyan**        | `#00E5FF` | Lean take; secondary accent |
| **Accent green**       | `#39FF14` | Strong take; success        |
| **Accent amber**       | `#F59E0B` | Borderline; caution         |
| **Accent red**         | `#EF4444` | Decline; alert; urgent      |
| **Accent purple**      | `#8B5CF6` | Decision metric             |
| **Neutral**            | `#94A3C8` | Muted; secondary text       |
| **Track CA**           | `#3B82F6` | California litigation       |
| **Track TX**           | `#F59E0B` | Texas litigation            |
| **Track RICO**         | `#EF4444` | Federal RICO                |

Source: `docs/FUNDAMENTAL_STRATEGIES_AND_SPECIFICATIONS.md` §4.

### 3.2 Design Principles (From Repo + Best Practices)

| Principle                        | Specification                                   | Source              |
| -------------------------------- | ----------------------------------------------- | ------------------- |
| **Dark-mode first**              | Reduce eye strain for long review sessions      | litigation-swarm-ui |
| **Data-dense layouts**           | Attorneys need information density              | litigation-swarm-ui |
| **Color-coded tracks**           | Blue (CA), Orange (TX), Red (RICO)              | litigation-swarm-ui |
| **Interactive visualizations**   | Timelines, knowledge graphs, damages            | litigation-swarm-ui |
| **Mobile-responsive**            | Key features on phone for court access          | litigation-swarm-ui |
| **Accessibility**                | WCAG 2.1 AA minimum                             | Constitution, ABA   |
| **AI-native UX**                 | Streaming, tool call feedback, voice interfaces | Modern AI apps      |
| **Voice-first where applicable** | Legal Scribe, deposition, hands-free research   | voice-agents module |

### 3.3 Industry Alignment

Incorporate patterns from:

- **Top repos**: shadcn/ui, v0.dev community, Vercel templates, Lovable/Bolt-style flows
- **Modern design**: Liquid glass, micro-interactions, skeleton loaders, optimistic updates
- **AI features**: Streaming text, agent status indicators, structured output previews, claim typing badges
- **Voice agents**: ElevenLabs embed, universal streaming, VAD, speaker diarization

---

## 4. Platform Integration Matrix

| Platform         | Module Role                  | Config                               | Notes                     |
| ---------------- | ---------------------------- | ------------------------------------ | ------------------------- |
| **Vercel**       | Deploy, Edge, Serverless     | `vercel.json`, env                   | Primary for web apps      |
| **v0**           | UI generation, components    | Custom Instructions (§2 in V0_SETUP) | litigationforc1 v02       |
| **Replit**       | Staging, Python agents       | Replit config                        | SwarmRICO, Verital        |
| **Google Dev**   | Gemini, Vertex, Document AI  | `config/connectors.yaml`             | Inference, cloud          |
| **Hugging Face** | Models, Spaces, Datasets     | `HF_TOKEN`                           | Fine-tuning, demos        |
| **Lovable**      | Rapid prototype, AI agents   | (per project)                        | Alternative to v0 for MVP |
| **Bolt.new**     | Browser IDE, multi-framework | (per project)                        | Next/Vue/Svelte/Astro     |
| **Figma**        | Design system, Code Connect  | Figma MCP                            | Design-to-code            |
| **Hex**          | Dashboards, AI analytics     | (per org)                            | Data apps, Notebook Agent |
| **ElevenLabs**   | Voice agents                 | `ELEVENLABS_API_KEY`                 | Legal Scribe, TTS/STT     |

### 4.1 Optionality Matrix

| Need       | Primary           | Optional             |
| ---------- | ----------------- | -------------------- |
| UI build   | v0 + shadcn       | Lovable, Bolt, Mocha |
| Deploy     | Vercel            | Replit, Netlify      |
| Auth       | Supabase          | NextAuth, Clerk      |
| AI chat    | Vercel AI SDK     | LangChain, custom    |
| Dashboards | Custom + Recharts | Hex, Metabase        |
| Voice      | ElevenLabs        | Whisper, Deepgram    |

---

## 5. Voice Agents & AI Features Focus

### 5.1 Voice Module Integration

- **Legal Scribe** — ElevenLabs conversational AI; claim typing; evidence linking
- **Deposition Transcriber** — Multi-format import; speaker diarization; timestamp alignment
- **Case Research Voice** — Hands-free LexVault search; timeline navigation

See `docs/modules/voice-agents.md`.

### 5.2 AI Features Checklist

| Feature                 | Required         | Implementation                               |
| ----------------------- | ---------------- | -------------------------------------------- |
| Streaming responses     | Yes              | Vercel AI SDK, SSE                           |
| Tool / function calling | Yes              | MCP router, agent playbooks                  |
| Structured output       | Yes              | Zod, JSON schema                             |
| Claim typing badges     | Yes (litigation) | FACT/INFERENCE/OPINION/LEGAL_CONCLUSION      |
| Attorney checkpoints    | Yes              | Confirm before privilege, filing, production |
| Audit trail             | Yes              | Processing history, hashes                   |
| Voice input/output      | Optional         | ElevenLabs embed                             |

---

## 6. Constitution & Repo Alignment

### 6.1 Constitution Rules in Modules

| Rule                       | Module Impact                                                                   |
| -------------------------- | ------------------------------------------------------------------------------- |
| **Human-in-loop**          | UI must include attorney review checkpoints for privilege, productions, filings |
| **Claim typing**           | Every assertion tagged; badges in document viewer, timeline                     |
| **Explainability & audit** | Log prompts, tool calls, outputs; immutable trail                               |
| **Simulation disclaimer**  | "Draft for attorney review. Not legal advice." on legal outputs                 |
| **New capabilities**       | Create skill; update indexes; emulate LexVault/ontology                         |

### 6.2 Relevant Repo Instructions

| Doc                                                 | Use                                         |
| --------------------------------------------------- | ------------------------------------------- |
| `docs/constitution.md`                              | Non-negotiable principles                   |
| `docs/FUNDAMENTAL_STRATEGIES_AND_SPECIFICATIONS.md` | Agent types, design tokens, rules hierarchy |
| `docs/V0_SETUP_AND_INSTRUCTIONS.md`                 | v0 Custom Instructions, litigationforc1 v02 |
| `docs/modules/lexvault.md`                          | File/evidence systems                       |
| `docs/modules/ontology.md`                          | Entity schemas, naming                      |
| `docs/modules/litigation-swarm-ui.md`               | Web app, pages, components                  |
| `docs/modules/voice-agents.md`                      | Voice agent specs                           |
| `docs/REFERENCE_PATTERNS_AND_EXAMPLE_REPOS.md`      | What to emulate                             |

---

## 7. Industry Best Methods (Researched 2025)

> **Sources**: Netguru, PRM Infotech, Google Cloud Architecture Center, Netguru/Gatsby, Seahawk Media, Viartisan, Analytics Insight, GetOrchestra, DevTech Insights, Bubble.io, Webflow, Babylon.js, React Native/Flutter comparisons.

### 7.1 Website Architecture

| Pattern                       | Use Case                          | Tech                                 | Notes                                    |
| ----------------------------- | --------------------------------- | ------------------------------------ | ---------------------------------------- |
| **Jamstack**                  | Marketing sites, docs, content    | Next.js, Gatsby, Hugo + Headless CMS | Pre-rendered static HTML, CDN, high perf |
| **Headless CMS (API-driven)** | Large content, multi-channel      | Storyblok, Sanity, Contentful        | Webhooks for rebuilds; GROQ/GraphQL      |
| **Headless CMS (Git-based)**  | Lower cost, data ownership        | TinaCMS, CloudCannon, Decap          | Offline builds, no vendor lock-in        |
| **SSG**                       | Content-heavy, infrequent updates | Next.js SSG, Astro                   | Build-time render; no runtime backend    |

**Recommendation**: Jamstack + Headless CMS for connectedagents.ai marketing; API-driven for scale, Git-based for cost/control.

---

### 7.2 Web App Architecture (Scalable)

| Pattern                       | Principle                               | Use When                                 |
| ----------------------------- | --------------------------------------- | ---------------------------------------- |
| **Layered**                   | Presentation → Business Logic → Data    | Clear separation; easier testing         |
| **Microservices**             | Domain-driven; independent deploy       | Large teams; polyglot; scale             |
| **Event-driven**              | Message queues (Kafka, RabbitMQ); async | Loosely coupled; fault tolerance         |
| **Serverless**                | Scale zero-to-high; pay-per-use         | Spiky traffic; Vercel, AWS Lambda, Azure |
| **Container + orchestration** | Docker + Kubernetes                     | Full control; multi-cloud                |

**Scaling**: Horizontal (add instances) > vertical for cost. Stateless components; multi-level caching; DB read replicas + sharding.

---

### 7.3 Mobile / Phone App Architecture

| Approach               | Best For                             | Pros                                        | Cons                               |
| ---------------------- | ------------------------------------ | ------------------------------------------- | ---------------------------------- |
| **React Native**       | Teams with JS/React; CodePush OTA    | Web talent reuse; New Architecture (faster) | iOS hardware access limits         |
| **Flutter**            | Pixel-perfect UI; complex animations | Impeller renderer; owns render stack        | Larger app size                    |
| **PWA**                | Web-first; installable; offline      | Fast MVP; no store; single codebase         | iOS limitations; complex UI harder |
| **Clean Architecture** | All approaches                       | MVC, layered; offline-first; security-first | —                                  |

**Recommendation**: PWA for court-access lightweight (litigation); React Native or Flutter for full-featured mobile apps. Match framework to team and use case.

---

### 7.4 UI/UX Trends: 3D, Holographic, Interactive

| Trend                        | Tech                                        | Use                                          |
| ---------------------------- | ------------------------------------------- | -------------------------------------------- |
| **Holographic / 3D web**     | WebXR, Three.js, Babylon.js                 | Volumetric UI; elements "pop out"; immersive |
| **Spatial / immersive**      | Apple Vision Pro, Meta Quest 3              | Depth, gesture, eye tracking; contextual UI  |
| **WebXR**                    | Babylon.js (first-class), Three.js (manual) | VR/AR in browser; hand tracking              |
| **AI hyper-personalization** | —                                           | Remember preferences; 40%+ revenue potential |
| **Voice UI**                 | ElevenLabs, conversational design           | Hands-free; court/litigation workflows       |
| **Dark mode**                | —                                           | Litigation swarm default; reduce strain      |

**3D/Holographic**: Babylon.js for AR/WebXR (built-in helpers); Three.js for lighter weight. Principles: depth/layers, user comfort (high refresh, no motion sickness), multimodal (haptic, voice, gestures).

---

### 7.5 No-Code / Low-Code Tools & Automations

| Category                | Platforms                                 | Use                                                                         |
| ----------------------- | ----------------------------------------- | --------------------------------------------------------------------------- |
| **Workflow automation** | Zapier, Make, n8n                         | Connectors; multi-step; integrations                                        |
| **Enterprise low-code** | Microsoft Power Platform, Appian, Workato | Forrester leader; enterprise scale; API-first                               |
| **UI builders**         | Webflow, Bubble, Retool                   | Webflow = design; Bubble = full-stack apps; Retool = internal tools         |
| **Data + apps**         | Airtable, WeWeb                           | Airtable = relational + automations; WeWeb = data-driven on custom backends |
| **Mobile no-code**      | Thunkable, FlutterFlow                    | Thunkable = native mobile; FlutterFlow = cross-platform                     |
| **Open-source**         | n8n                                       | Self-host; node-based; flexible                                             |

**Platform types (2025)**: Execution orchestration; integration/middleware; workflow automation; BaaS; full-stack app; UI builders. Gartner: 60% of dev teams will adopt enterprise low-code by 2028.

---

### 7.6 3D / WebXR Stack (Optional for Immersive)

| Component        | Primary                  | Optional           |
| ---------------- | ------------------------ | ------------------ |
| **3D engine**    | Babylon.js               | Three.js           |
| **XR/AR**        | WebXR (Babylon built-in) | Raw WebXR API      |
| **Asset format** | glTF, USDz               | —                  |
| **Headsets**     | Meta Quest, Vision Pro   | Valve Index, PS VR |

Use when: court/virtual hearing demos, evidence visualization, knowledge graph 3D. Balance with accessibility and constitution (human-in-loop, simulation disclaimer).

---

## 7.7 Lenny's Podcast & Newsletter — Recommended Applications (Updated 2025)

> **Sources**: ["What's in your stack: The state of tech tools in 2025"](https://www.lennysnewsletter.com/p/whats-in-your-stack-the-state-of) (6,500 respondents, Jan 2025), [AI tools are overdelivering](https://www.lennysnewsletter.com/p/ai-tools-are-overdelivering-results) (1,750 respondents, Dec 2025), [Product Pass](https://www.lennysnewsletter.com/p/productpass) (Jul 2025), [How to get the most out of your product pass](https://www.lennysnewsletter.com/p/how-to-get-the-most-out-of-your-product) (Sep 2025), [Inside Bolt](https://www.lennysnewsletter.com/p/inside-bolt-eric-simons) (Mar 2025), [Lovable growth](https://lennysvault.com/episodes/971e16a9-61a6-46b5-8436-3bb0fbba4d01), [Lenny's Vault](https://lennysvault.com/), [Lennybot](https://www.lennybot.com/).

### Top 5 Most Valued (AMV-Adjusted)

| Rank | Tool           | Use                                                       |
| ---- | -------------- | --------------------------------------------------------- |
| 1    | **Linear**     | Project management; craft winning; Jira alternative       |
| 2    | **Cursor**     | AI-native IDE; 17% overall, 21% engineers; fastest rising |
| 3    | **Slack**      | Communication hub; 72% usage; where work happens          |
| 4    | **Notion**     | Docs, PM, CRM; "good enough at everything"; flexibility   |
| 5    | **Perplexity** | Deep research; answers instead of links; PM workflows     |

### AI Tools (Dominant)

| Tool               | Usage                      | Notes                                         |
| ------------------ | -------------------------- | --------------------------------------------- |
| **ChatGPT**        | 90%                        | Most used tool overall; ahead of Gmail, Slack |
| **Claude**         | 35%                        | Often paired with ChatGPT as thought partner  |
| **Perplexity**     | —                          | Top 5 valued; research, decision-making       |
| **Gemini**         | 24%                        | Google Workspace integration                  |
| **Cursor**         | 17% overall, 21% engineers | AI-native IDE; launched 2023                  |
| **v0**             | ~10%                       | UI generation; with Replit                    |
| **Replit**         | ~10%                       | AI-native coding                              |
| **Bolt**           | 5%                         | Browser IDE                                   |
| **GitHub Copilot** | 40% of engineers           | —                                             |

### Project Management

| Tool       | Share     | Notes                                           |
| ---------- | --------- | ----------------------------------------------- |
| **Jira**   | 68%       | Dominates but tops "please let us switch" list  |
| **Linear** | 10%+      | Fastest-growing; praised UX; modern alternative |
| **Notion** | 2nd in PM | Also docs, CRM                                  |
| **Asana**  | —         | Comparable to Linear adoption                   |

### Design & Presentation

| Tool                           | Use                                                    |
| ------------------------------ | ------------------------------------------------------ |
| **Figma**                      | 97% of designers; 90% overall; ubiquitous              |
| **Canva**                      | Catching up; marketers, founders; quick visuals        |
| **Figma Slides**               | Presentations; ahead of Keynote, closing on PowerPoint |
| **Miro**                       | Virtual whiteboard; ahead of FigJam (barely)           |
| **Pitch, Gamma, Beautiful.ai** | AI-native presentations                                |

### Docs, Collaboration, CRM

| Tool            | Use                                         |
| --------------- | ------------------------------------------- |
| **Google Docs** | Real-time collaboration; go-to              |
| **Notion**      | Team wikis, PM, docs; "good for everything" |
| **Confluence**  | Enterprise; hanging on                      |
| **Slack**       | 29% as customer support (early-stage)       |
| **Notion**      | 11% as CRM; flexibility                     |
| **Salesforce**  | Enterprise CRM; complexity complaints       |
| **HubSpot**     | SMB CRM; intuitive                          |

### Analytics & User Research

| Tool                                    | Use                                    |
| --------------------------------------- | -------------------------------------- |
| **Google Analytics**                    | General analytics; dominant            |
| **Amplitude, Mixpanel**                 | Behavior tracking                      |
| **Tableau, Looker**                     | BI; dashboards                         |
| **PostHog**                             | Open-source; YC favorite; up-and-comer |
| **Power BI**                            | Microsoft stack                        |
| **Hotjar**                              | Heatmaps, session recordings           |
| **Metabase**                            | Startup dashboards                     |
| **Dovetail**                            | Insight management                     |
| **User Interviews**                     | Recruitment (#2 in research)           |
| **Typeform**                            | Survey glow-up                         |
| **UserTesting, Qualtrics, Maze, Sprig** | Specialists                            |

### Podcast / Content Production (Lenny's Stack)

| Category       | Tool                                                        |
| -------------- | ----------------------------------------------------------- |
| **Recording**  | Riverside, Podcastle, Descript                              |
| **Editing**    | Descript                                                    |
| **Hosting**    | Substack (newsletter-integrated)                            |
| **Analytics**  | Podstatus, Chartable                                        |
| **Website**    | Podpage                                                     |
| **Production** | Pen Name, Supermix (clips, trailers)                        |
| **Org**        | Notion (calendar), Coda (questions), Slack, Google Calendar |

### Lenny's Sponsors / Vetted Tools

| Tool                 | Category                        |
| -------------------- | ------------------------------- |
| **Amplitude, Heap**  | Product analytics               |
| **Ahrefs**           | SEO                             |
| **Attio**            | CRM for startups                |
| **AssemblyAI**       | Speech transcription, AI models |
| **Brave Search API** | Independent search for AI apps  |
| **Coda**             | Document collaboration          |
| **CommandBar**       | AI-powered user assistance      |
| **Dovetail**         | Customer research               |
| **DX**               | Developer productivity          |
| **Eppo**             | Experimentation                 |
| **Explo**            | Embedded analytics              |
| **Flatfile**         | CSV/data importer               |
| **Formsort**         | Flow building                   |
| **Braintrust**       | Talent marketplace              |

### Meta-Takeaways (Lenny's Survey)

1. **Bundling** — Jira, Teams, Google Slides win via bundles but rank high on "least valued"; craft can disrupt.
2. **Craft wins** — Linear, Notion, Slack, Figma praised for UX and fit; people willing to switch.
3. **Mix-and-match** — Teams use multiple tools per category (e.g., ChatGPT + Claude, ChatGPT + Perplexity).

**Include in Connected Agents stack**: Linear, Cursor, Notion, Perplexity, Figma, Amplitude/Mixpanel/PostHog, Dovetail, User Interviews; consider Attio (CRM), AssemblyAI (transcription), CommandBar (in-app AI).

**Reference**: [Lenny's Vault](https://lennysvault.com/) — AI-powered search across Lenny's podcast; [Lennybot](https://www.lennybot.com/) — Delphi-powered chatbot trained on newsletter + podcast (pattern for knowledge-base AI).

---

### Recent Episodes & Featured Tools (YouTube / Podcast 2025)

| Episode                        | Guest                        | Key Tools / Insights                                                                                       |
| ------------------------------ | ---------------------------- | ---------------------------------------------------------------------------------------------------------- |
| **Lovable $200M ARR**          | Elena Verna (Head of Growth) | Lovable, vibe coding; growth playbook reinvented; building in public; influencer marketing 10x paid social |
| **Bolt ~$40M ARR in 5 months** | Eric Simons (StackBlitz)     | Bolt, WebContainer, Claude 3.5 Sonnet; PMs may be better positioned than engineers; $30K projects → $300   |
| **Product Pass guides**        | Lenny                        | Replit Agent 3, Warp, Linear, Wispr Flow, Gamma 3.0, Magic Patterns, Descript, Mobbin                      |
| **ChatPRD**                    | —                            | v0 integration, MCP for Cursor/VS Code/Claude                                                              |

### Product Pass — Full List (20+ Tools, Jul 2025)

| Category        | Tools                                                                             |
| --------------- | --------------------------------------------------------------------------------- |
| **Research**    | Manus, Perplexity                                                                 |
| **Design**      | Canva Business, Framer, Gamma, Mobbin                                             |
| **Build**       | Lovable, Replit, Bolt, n8n, Amp, Factory, Devin, Warp, Magic Patterns, ElevenLabs |
| **Scale**       | Railway                                                                           |
| **Track**       | PostHog                                                                           |
| **Collaborate** | Linear, Wispr Flow, Granola, ChatPRD                                              |
| **Incorporate** | Stripe Atlas                                                                      |

### AI Productivity Survey (1,750 respondents, Dec 2025)

| Finding                           | Stat                                                        |
| --------------------------------- | ----------------------------------------------------------- |
| AI exceeded expectations          | 55%                                                         |
| Save ≥ half day/week on key tasks | 50%+                                                        |
| Founders benefit most             | 49% save 6+ hrs/week                                        |
| Report significant downsides      | 92.4%                                                       |
| n8n                               | Dominates agent/automation landscape (adoption still early) |
| Designers                         | Fewer benefits than engineers/founders                      |

### Recent Sponsors & New Tools (Episodes 2025)

| Tool               | Role                                                            |
| ------------------ | --------------------------------------------------------------- |
| **WorkOS**         | Enterprise SSO, SCIM, RBAC, audit logs; "Stripe for enterprise" |
| **VZero** (Vercel) | Web dev assistant; AI + DB; screenshot import; GitHub sync      |
| **Eppo**           | Experimentation                                                 |
| **OneSchema**      | CSV import 10x faster                                           |
| **Fundrise**       | Real estate investing                                           |

### New Additions for Connected Agents

- **Wispr Flow** — Voice dictation for vibe coding, IDE, phone
- **Magic Patterns** — AI prototyping for PMs; use existing component library
- **Gamma 3.0** — AI presentations, landing pages, docs
- **Manus** — Research
- **VZero** — Vercel's professional web dev assistant
- **ChatPRD** — v0 + MCP integration; PRD → prototypes

---

## 8. Quick Reference: Choosing Modules

1. **Read** `docs/constitution.md`, `docs/FUNDAMENTAL_STRATEGIES_AND_SPECIFICATIONS.md`
2. **Match design** — Use tokens from §3.1; dark-mode first; litigation color coding
3. **Select stack** — Primary from §2.2; optional from §2.2 if scope requires
4. **Check platform** — Vercel/v0/Replit/Hex per §4
5. **Architecture** — Website (§7.1) vs Web App (§7.2) vs Mobile (§7.3); 3D/immersive (§7.4, §7.6) if needed
6. **No-code/low-code** — Zapier, Make, n8n, Power Platform, Bubble, Webflow per §7.5
7. **Voice?** — ElevenLabs if voice agent; see voice-agents module
8. **Constitution** — Human-in-loop, claim typing, audit, disclaimer in UI
9. **Update** — Add to `config/module-selection.yaml` if new pattern

---

_Maintain at: docs/MODULE_ARCHITECTURE_AND_PLATFORM_STACK.md. Sync to child repos via sync-all-repos-and-review.sh._
