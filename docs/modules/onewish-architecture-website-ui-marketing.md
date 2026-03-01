# OneWish.io Architecture — Website, UI/UX, and Marketing (Module + Submodules)

**Purpose:** Add **OneWish.io architecture** for **website, UI/UX, and marketing** to the master repo in the **granular form** prescribed for ConnectedAgents.AI and related Foundry: **rules**, **skills**, **knowledge**, **modules**, and **submodules**. Includes **write plan** and **questions and anticipated (now)** for downstream and Foundry sync.

**Governance:** Constitution applies. Simulation disclaimer: litigation outputs are for support only; not legal advice; attorney review required.

**References:** [LITIGATIONFORCE_AI_COMPONENT_BREAKDOWN.md](LITIGATIONFORCE_AI_COMPONENT_BREAKDOWN.md) (§2, §5); [config/segment-lit-force-lexvault-connected.yaml](../../config/segment-lit-force-lexvault-connected.yaml); [UI_UX_AND_MARKETING_TURNKEY_GUIDE_SOURCES_AND_ORGANIZATION.md](../UI_UX_AND_MARKETING_TURNKEY_GUIDE_SOURCES_AND_ORGANIZATION.md).

---

## 1. Module Definition (ConnectedAgents.AI / Foundry)

| Attribute           | Value                                                                                                                                                                                                                                        |
| ------------------- | -------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| **Module name**     | onewish-architecture-website-ui-marketing                                                                                                                                                                                                    |
| **Display name**    | OneWish.io Architecture — Website, UI/UX & Marketing                                                                                                                                                                                         |
| **Scope**           | OneWish OS, NextTech OS, and all sub-OSes (LitigationForce.AI, Family Office, Lifestyle, PowerConnection) for **website**, **UI/UX**, and **marketing** (separate and combined sites).                                                       |
| **Sync to Foundry** | Yes. Component is **registered and synced** to ConnectedAgents.AI OS Foundry so Foundry catalog includes website/UI/marketing rules, knowledge, skills, and submodules; downstream consumers can add “website/UI/marketing” as a capability. |
| **Repo type**       | Supporting component (rules, knowledge, skills); no separate repo required — lives in **master repo** under docs/modules, config, .cursor/rules, .cursor/skills, and knowledge_paths.                                                        |

---

## 2. Rules (Granular)

Each rule is **identifiable**, **documented**, and **enforceable** (by human or checklist). Foundry and downstream can reference these by id.

| Rule id          | Rule                                                                                                                                                                                                                                               | Where defined                                                                                                                                                                                                                | Downstream / Foundry           |
| ---------------- | -------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | ---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | ------------------------------ |
| **web-arch-001** | **Design system single source:** One design system (tokens, components) for all sites and apps. Tokens canonical in FUNDAMENTAL_STRATEGIES §4 and litigation-swarm-ui Design System; Figma Variables and shared library must align.                | This module; [UI_UX_AND_MARKETING_TURNKEY_GUIDE](../UI_UX_AND_MARKETING_TURNKEY_GUIDE_SOURCES_AND_ORGANIZATION.md) §5.2; [FUNDAMENTAL_STRATEGIES_AND_SPECIFICATIONS.md](../FUNDAMENTAL_STRATEGIES_AND_SPECIFICATIONS.md) §4. | Foundry: design_system_rule    |
| **web-arch-002** | **Design system enforcer:** One person or checklist enforces that all new UI (Framer, v0, Next) uses the design system; no one-off colors/fonts. (NN/g design system enforcer.)                                                                    | UI_UX_AND_MARKETING_TURNKEY_GUIDE §5.2; this module.                                                                                                                                                                         | Foundry: enforcer_rule         |
| **web-arch-003** | **Content source of truth:** All marketing and site copy lives in repo docs (or one Notion/CMS). No duplicate “master” in unversioned docs. Content map: doc → site per UI_UX_AND_MARKETING_TURNKEY_GUIDE §3.3.                                    | UI_UX_AND_MARKETING_TURNKEY_GUIDE §5.1; LAUNCH_BLOG §2.2.                                                                                                                                                                    | Foundry: content_sot_rule      |
| **web-arch-004** | **Simulation disclaimer on all sites:** Every public site and in-app view must show: “Litigation outputs are for litigation support only. Not legal advice. Attorney review required.”                                                             | Constitution; LAUNCH_BLOG §2.3; this module.                                                                                                                                                                                 | Foundry: disclaimer_rule       |
| **web-arch-005** | **Multi-site hybrid architecture:** Shared design system + shared components; **separate** Framer or Next **projects per domain** (litigationforce.com, onewish.io, talk, smithwick.ai, talianventures.com). No single monolith for all marketing. | UI_UX_AND_MARKETING_TURNKEY_GUIDE §3.2; this module.                                                                                                                                                                         | Foundry: multisite_hybrid_rule |
| **web-arch-006** | **One CTA per landing:** Each marketing/landing page has one primary conversion goal (e.g. “Request demo,” “Talk to Alex”); limited nav and internal links on landing. (Framer best practice.)                                                     | UI_UX_AND_MARKETING_TURNKEY_GUIDE §1.3; this module.                                                                                                                                                                         | Foundry: cta_rule              |
| **web-arch-007** | **5-second test:** Visitor understands offer and why they should care within 5 seconds. Strong headline with benefit; no generic “Transform Your Business.”                                                                                        | UI_UX_AND_MARKETING_TURNKEY_GUIDE §1.3; this module.                                                                                                                                                                         | Foundry: five_second_rule      |
| **web-arch-008** | **Accessibility:** WCAG 2.1 AA minimum for all public and app UI. Contrast and semantics in Framer/Next.                                                                                                                                           | litigation-swarm-ui; UI_UX_AND_MARKETING_TURNKEY_GUIDE §5.2.                                                                                                                                                                 | Foundry: a11y_rule             |

---

## 3. Skills (Granular)

Skills are **Cursor (or equivalent) skills** that agents use when working on website, UI/UX, or marketing. Each skill has a **path** and **scope**.

| Skill id          | Skill name              | Path                                            | Scope                                                                                                                                                                                                                                                                                                                                                        | Foundry                                                              |
| ----------------- | ----------------------- | ----------------------------------------------- | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------ | -------------------------------------------------------------------- |
| **web-skill-001** | v0-litigation-ui        | .cursor/skills/v0-litigation-ui/SKILL.md        | Litigation Swarm UI with v0; attorney checkpoints; simulation disclaimer; claim typing.                                                                                                                                                                                                                                                                      | Already in lit_force segment; catalog in Foundry                     |
| **web-skill-002** | ui-ux-marketing-turnkey | .cursor/skills/ui-ux-marketing-turnkey/SKILL.md | When building or updating website, landing, or marketing: use UI_UX_AND_MARKETING_TURNKEY_GUIDE; design system from FUNDAMENTAL_STRATEGIES §4 and litigation-swarm-ui; content from WEBSITE_AND_INVESTOR, LAUNCH_BLOG §2, FOR_CUSTOMERS; multi-site map §3.3; cleanup checklist §5; Figma/Mobbin/Framer/Next workflow §4; repos/starred search Part 8 / §10. | Done; in segment website_ui_marketing; catalog in Foundry when ready |

**Skill creation (write plan):** Create `.cursor/skills/ui-ux-marketing-turnkey/SKILL.md` that references this module and UI_UX_AND_MARKETING_TURNKEY_GUIDE; triggers when user asks to build or organize website, UI, UX, marketing, multi-site, or design system.

---

## 4. Knowledge (Granular)

Knowledge is **path-based**. Each path is a **knowledge_path** that agents and Foundry can resolve. Order is significant for priority.

| Knowledge id     | Path                                                               | Description                                                                                                                                   | Foundry         |
| ---------------- | ------------------------------------------------------------------ | --------------------------------------------------------------------------------------------------------------------------------------------- | --------------- |
| **web-know-001** | docs/UI_UX_AND_MARKETING_TURNKEY_GUIDE_SOURCES_AND_ORGANIZATION.md | Turnkey guide: institutional sources (NN/g, Figma, Framer, Mobbin); repos; multi-site architecture; content map; workflow; cleanup checklist. | knowledge_paths |
| **web-know-002** | docs/WEBSITE_AND_INVESTOR_PRESENTATION_INTEGRATED.md               | Website copy (Part B), one-liners (Part D), investor (Part C); shared assets.                                                                 | knowledge_paths |
| **web-know-003** | docs/LAUNCH_BLOG_SCHEDULE_WEBSITES_VOICE_AGENT_AND_SETUP.md        | Domains; pages to implement (§2.2); deployment steps (§2.3); content source per page.                                                         | knowledge_paths |
| **web-know-004** | docs/FUNDAMENTAL_STRATEGIES_AND_SPECIFICATIONS.md                  | Design tokens (§4); canonical for all UI.                                                                                                     | knowledge_paths |
| **web-know-005** | docs/modules/litigation-swarm-ui.md                                | Litigation Swarm design system; pages; deployment; tokens; integration.                                                                       | knowledge_paths |
| **web-know-006** | docs/FOR_CUSTOMERS_WHY_ONEWISH_AND_GENIE_DESKTOP.md                | OneWish/Genie copy for onewish.io and end-user messaging.                                                                                     | knowledge_paths |
| **web-know-007** | docs/ARCHITECTURE_FOR_THIRD_PARTY_PRESENTATION.md                  | Partner/investor architecture and narrative.                                                                                                  | knowledge_paths |
| **web-know-008** | docs/modules/onewish-architecture-website-ui-marketing.md          | This module: rules, skills, knowledge, submodules, write plan, Q&A.                                                                           | knowledge_paths |
| **web-know-009** | config/module-selection.yaml                                       | UI components (shadcn, v0); platforms (Framer, Figma); design_tokens ref.                                                                     | knowledge_paths |
| **web-know-010** | docs/PRE_LAUNCH_AND_PARTNER_PRESENTATIONS_VC_CLOUD_LEGAL_TECH.md   | Pre-launch; partner presentations; Part 0B full platform value; examples and visuals.                                                         | knowledge_paths |
| **web-know-011** | docs/CONSOLIDATION_AND_REPO_STATUS.md                              | Canonical repo map; all_repos; search for enhancement.                                                                                        | knowledge_paths |
| **web-know-012** | docs/REFERENCE_PATTERNS_AND_EXAMPLE_REPOS.md                       | Module specs; example repos; what to emulate.                                                                                                 | knowledge_paths |
| **web-know-013** | docs/SOURCES_AND_EMULATION_INDEX.md                                | Top sources per action; §7b Website/UI/Marketing.                                                                                             | knowledge_paths |
| **web-know-014** | docs/STARRED_AND_REFERENCE_REPOS.md                                | All platform repos; website/UI/marketing reference repos; enhancement process.                                                                | knowledge_paths |
| **web-know-015** | docs/MASTER_FILES_AND_REVIEW_BEFORE_ACTION.md                      | Review loop; §5 starred/other repos integrate in parts.                                                                                       | knowledge_paths |
| **web-know-016** | docs/WEBAPPS_INVENTORY_AND_IMPLEMENT_IN_CONTEXT.md                 | All webapps; implement-in-context checklist per app; content map.                                                                             | knowledge_paths |
| **web-know-017** | docs/COMPONENT_BREAKDOWN_SYNC_AND_RUN.md                           | Break into modular parts; integrate/sync/push; run → go run → genie run.                                                                      | knowledge_paths |

---

## 5. Submodules (Granular)

Submodules are **logical subdivisions** of the module. Each can be **synced to Foundry** as a **sub-component** so downstream can add “design system” or “multi-site” without the full module.

| Submodule id    | Submodule name          | Contents                                                                                                                            | Sync to Foundry |
| --------------- | ----------------------- | ----------------------------------------------------------------------------------------------------------------------------------- | --------------- |
| **web-sub-001** | design-system           | Rules web-arch-001, web-arch-002, web-arch-008; knowledge web-know-004, web-know-005, web-know-009; tokens and enforcer.            | Yes             |
| **web-sub-002** | multi-site-architecture | Rules web-arch-005, web-arch-006, web-arch-007; knowledge web-know-001 (§3), web-know-002, web-know-003; domain list; hybrid model. | Yes             |
| **web-sub-003** | content-map             | Rule web-arch-003; knowledge web-know-001 (§3.3), web-know-002, web-know-003, web-know-006, web-know-007; doc → site table.         | Yes             |
| **web-sub-004** | institutional-sources   | Knowledge web-know-001 (§1, §2); NN/g, Figma, Framer, Mobbin links and use cases; repos (Contentful, next-marketing-site).          | Yes             |
| **web-sub-005** | cleanup-checklist       | Knowledge web-know-001 (§5); checklist items for content, design, sites, SEO, repo index.                                           | Yes             |
| **web-sub-006** | figma-framer-workflow   | Knowledge web-know-001 (§4); tool-to-task matrix; design → build → content steps.                                                   | Yes             |

---

## 6. Downstream and Foundry Sync

| Action                  | Description                                                                                                                                                                                                                                                          |
| ----------------------- | -------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| **Register module**     | Register `onewish-architecture-website-ui-marketing` in ConnectedAgents.AI OS Foundry with: module id, display name, scope, rules (web-arch-001 … 008), skills (web-skill-001, web-skill-002), knowledge_paths (web-know-001 … 010), submodules (web-sub-001 … 006). |
| **Register submodules** | Each submodule (design-system, multi-site-architecture, content-map, institutional-sources, cleanup-checklist, figma-framer-workflow) is a **sub-component** in Foundry; consumers can add by submodule.                                                             |
| **Segment config**      | Add optional segment `website_ui_marketing` (or extend existing segment) in config with knowledge_paths and skills from §3 and §4 so agents route to this context when working on website/UI/marketing.                                                              |
| **Propagation**         | When this module or its rules/knowledge/skills are updated, push metadata to Foundry; Foundry propagates to ConnectedAgents.AI OS and back to sub-OSes (virtuous loop).                                                                                              |

---

## 7. Write Plan

**Order of operations** for creating and wiring this module and its downstream artifacts.

| Step   | Task                                          | Artifact                                                                                     | Owner |
| ------ | --------------------------------------------- | -------------------------------------------------------------------------------------------- | ----- |
| **W1** | Module doc (this file)                        | docs/modules/onewish-architecture-website-ui-marketing.md                                    | Done  |
| **W2** | Create skill ui-ux-marketing-turnkey          | .cursor/skills/ui-ux-marketing-turnkey/SKILL.md                                              | To do |
| **W3** | Add knowledge_paths to segment or new segment | config/segment-lit-force-lexvault-connected.yaml or config/segment-website-ui-marketing.yaml | To do |
| **W4** | Add rules to .cursor/rules (optional refs)    | e.g. .cursor/rules/web-arch-design-system.mdc with ref to web-arch-001, web-arch-002         | To do |
| **W5** | Foundry registry entry (when Foundry exists)  | Component metadata: module id, rules, skills, knowledge_paths, submodules                    | To do |
| **W6** | MASTER_INDEX or docs README                   | Link to this module and UI_UX_AND_MARKETING_TURNKEY_GUIDE under “Website / UI / Marketing”   | To do |

**Dependencies:** W2–W6 depend on W1. W3 can add paths that point to existing docs (web-know-001 … 010). W5 depends on Foundry API or registry format.

---

## 8. Questions and Anticipated (Now)

**Use this section** when onboarding, when syncing to Foundry, or when a downstream consumer asks “how do I use website/UI/marketing?”

### 8.1 Questions and answers

| #       | Question                                                                         | Anticipated answer                                                                                                                                                                                                                                                                                                            |
| ------- | -------------------------------------------------------------------------------- | ----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| **Q1**  | Where is the single source of truth for website and marketing copy?              | Repo docs: WEBSITE_AND_INVESTOR_PRESENTATION_INTEGRATED (Part B), FOR_CUSTOMERS_WHY_ONEWISH_AND_GENIE_DESKTOP, ARCHITECTURE_FOR_THIRD_PARTY_PRESENTATION, LAUNCH_BLOG_SCHEDULE §2.2. Content map: UI_UX_AND_MARKETING_TURNKEY_GUIDE §3.3. Rule: web-arch-003.                                                                 |
| **Q2**  | Where are design tokens defined?                                                 | FUNDAMENTAL_STRATEGIES_AND_SPECIFICATIONS §4; litigation-swarm-ui Design System. Figma Variables and Framer/Next must align. Rule: web-arch-001.                                                                                                                                                                              |
| **Q3**  | How do we organize multiple sites (litigationforce.com, onewish.io, talk, etc.)? | Hybrid: one design system; **separate** Framer or Next project per domain. No single monolith. Rule: web-arch-005. See UI_UX_AND_MARKETING_TURNKEY_GUIDE §3.1, §3.2.                                                                                                                                                          |
| **Q4**  | What tools do we use for UI/UX and marketing?                                    | Figma (design system, Variables); Mobbin (inspiration); Framer (marketing/landing); Next.js (Litigation Swarm app); v0 (Litigation UI). See UI_UX_AND_MARKETING_TURNKEY_GUIDE §4.2, module-selection.yaml.                                                                                                                    |
| **Q5**  | Who enforces the design system?                                                  | One person or checklist (web-arch-002). All new UI must use design system; no one-off colors/fonts.                                                                                                                                                                                                                           |
| **Q6**  | What must every public site show?                                                | Simulation disclaimer: “Litigation outputs are for litigation support only. Not legal advice. Attorney review required.” Rule: web-arch-004.                                                                                                                                                                                  |
| **Q7**  | How do I add this module to Foundry or a downstream app?                         | Register module `onewish-architecture-website-ui-marketing` with rules (web-arch-001 … 008), skills (web-skill-001, web-skill-002), knowledge_paths (web-know-001 … 010), submodules (web-sub-001 … 006). Optionally add only submodules (e.g. design-system, multi-site-architecture).                                       |
| **Q8**  | Where is the cleanup and organization checklist?                                 | UI_UX_AND_MARKETING_TURNKEY_GUIDE §5 (content, design, sites, SEO, repo). Submodule: web-sub-005.                                                                                                                                                                                                                             |
| **Q9**  | What institutional sources back our UI/UX decisions?                             | NN/g (design systems, enforcer, multi-site); Figma (Variables, shared library, large-scale structure); Framer (landing, conversion, SEO); Mobbin (patterns, Figma plugin). Links in UI_UX_AND_MARKETING_TURNKEY_GUIDE §1, §6.                                                                                                 |
| **Q10** | How does this relate to LitigationForce.AI component breakdown?                  | This module is a **supporting component** (rules, knowledge, skills) like “Rules & plugins” and “Knowledge bases” in LITIGATIONFORCE_AI_COMPONENT_BREAKDOWN §2.3. It applies across OneWish/NextTech and all sub-OSes for **website/UI/marketing**; LitForce-specific UI remains in litigation-swarm-ui and v0-litigation-ui. |

### 8.2 Anticipated “now” (current state)

| Item                                     | Status                                                                                      |
| ---------------------------------------- | ------------------------------------------------------------------------------------------- |
| Module doc (this file)                   | **Done**                                                                                    |
| UI_UX_AND_MARKETING_TURNKEY_GUIDE        | **Done** (sources, multi-site, content map, workflow, checklist)                            |
| Skill ui-ux-marketing-turnkey            | **Done** (.cursor/skills/ui-ux-marketing-turnkey/SKILL.md)                                  |
| Segment config (knowledge_paths + skill) | **Done** (segment website_ui_marketing in config/segment-lit-force-lexvault-connected.yaml) |
| .cursor/rules refs for web-arch-\*       | **Optional** (W4)                                                                           |
| Foundry registry                         | **When Foundry exists** (W5)                                                                |
| MASTER_INDEX / docs index link           | **To add** (W6)                                                                             |

---

## 9. References

| Doc                                                                                                                               | Purpose                                                          |
| --------------------------------------------------------------------------------------------------------------------------------- | ---------------------------------------------------------------- |
| [LITIGATIONFORCE_AI_COMPONENT_BREAKDOWN.md](../LITIGATIONFORCE_AI_COMPONENT_BREAKDOWN.md)                                         | Componentization; Foundry sync; rules, skills, knowledge pattern |
| [UI_UX_AND_MARKETING_TURNKEY_GUIDE_SOURCES_AND_ORGANIZATION.md](../UI_UX_AND_MARKETING_TURNKEY_GUIDE_SOURCES_AND_ORGANIZATION.md) | Turnkey guide; sources; multi-site; content map; checklist       |
| [config/segment-lit-force-lexvault-connected.yaml](../../config/segment-lit-force-lexvault-connected.yaml)                        | Segment pattern: knowledge_paths, skills, agents                 |
| [ONEWISHOS_CRYSTAL_CLEAR_ARCHITECTURE_AND_AGENT_TAXONOMY.md](../ONEWISHOS_CRYSTAL_CLEAR_ARCHITECTURE_AND_AGENT_TAXONOMY.md)       | OneWish → NextTech → sub-OSes; Foundry                           |

---

## 10. Repos and starred repos: search and enhance

**Purpose:** Search **all platform repos** and **starred/reference repos** to **enhance and perfect** this module, the turnkey guide, and downstream (Foundry, segment, rules, knowledge). Follow the process in [MASTER_FILES_AND_REVIEW_BEFORE_ACTION.md](../MASTER_FILES_AND_REVIEW_BEFORE_ACTION.md) §5 (list → review → integrate in parts → gate).

### 10.1 All platform repos (where to search)

| Repo                              | Config source                                                | What to search for (website/UI/marketing)                                                                   |
| --------------------------------- | ------------------------------------------------------------ | ----------------------------------------------------------------------------------------------------------- |
| **Master (this repo)**            | `.`                                                          | docs/, config/, .cursor/skills; CONSOLIDATION, REFERENCE_PATTERNS, SOURCES_AND_EMULATION_INDEX; all modules |
| **connected-agents-platform**     | config/repos.yaml routes                                     | Platform UI patterns, ontology, shared components                                                           |
| **LitigationForce.AI**            | config/repos.yaml routes                                     | Litigation Swarm UI, design tokens, deployment, v0                                                          |
| **file-management-toolkit**       | config/repos.yaml routes                                     | File/naming conventions that affect site or asset structure                                                 |
| **powerconnectionaiapplications** | config/repos.yaml routes                                     | Vertical app UI/marketing patterns                                                                          |
| **slack-agent-template**          | all_repos                                                    | Agent/doc patterns for consistency                                                                          |
| **nextjs-ai-chatbot**             | CONSOLIDATION §2                                             | Next.js + Vercel marketing/chat UI patterns                                                                 |
| **Archives**                      | docs/archives/ (github-archive, projects-archives, agent-os) | Historical design, config, or content to adopt                                                              |

**Canonical list:** [CONSOLIDATION_AND_REPO_STATUS.md](../CONSOLIDATION_AND_REPO_STATUS.md); [config/repos.yaml](../../config/repos.yaml). **Enhancement list:** [STARRED_AND_REFERENCE_REPOS.md](../STARRED_AND_REFERENCE_REPOS.md) (all platform repos + website/UI/marketing reference repos).

### 10.2 Starred and reference repos (website/UI/marketing)

| Source                                                                                                     | Use for                                                                                                   |
| ---------------------------------------------------------------------------------------------------------- | --------------------------------------------------------------------------------------------------------- |
| [STARRED_AND_REFERENCE_REPOS.md](../STARRED_AND_REFERENCE_REPOS.md) § Website / UI / Marketing             | Contentful, thvroyal/next-marketing-site, caisy; Figma, Framer, Mobbin, NN/g (integrated or to integrate) |
| [UI_UX_AND_MARKETING_TURNKEY_GUIDE](../UI_UX_AND_MARKETING_TURNKEY_GUIDE_SOURCES_AND_ORGANIZATION.md) §6.2 | Repos (starter/reference) for Next + marketing                                                            |
| [REFERENCE_PATTERNS_AND_EXAMPLE_REPOS.md](../REFERENCE_PATTERNS_AND_EXAMPLE_REPOS.md)                      | Module specs to emulate; example repos (e.g. nextjs-ai-chatbot for AI chat UI)                            |
| [SOURCES_AND_EMULATION_INDEX.md](../SOURCES_AND_EMULATION_INDEX.md)                                        | Top sources per action; add Website/UI/Marketing row and keep updated                                     |

### 10.3 Enhancement checklist (what to pull)

When searching repos or starred/reference repos:

- **Design system:** Tokens, variables, components that could align with FUNDAMENTAL_STRATEGIES §4 and litigation-swarm-ui; add to knowledge_paths or rules if adopted.
- **Content and copy:** Narrative, one-liners, or page structures that belong in WEBSITE_AND_INVESTOR, LAUNCH_BLOG, FOR_CUSTOMERS; update content map (turnkey guide §3.3).
- **Multi-site / hybrid:** Patterns for domain-per-project, shared design system, or internal linking; update rules (web-arch-005) or turnkey §3.
- **Institutional sources:** New NN/g, Figma, Framer, or Mobbin links or practices; add to turnkey guide §1 or §6 and to submodule web-sub-004.
- **Cleanup and checklist:** Items for turnkey guide §5 (content, design, sites, SEO, repo index); add to web-sub-005.
- **Master files:** Any change that affects governance, repo map, or architecture → update per MASTER_FILES_AND_REVIEW_BEFORE_ACTION §2–§4.

After integrating: update this module (§2–§5 if rules/skills/knowledge/submodules change), [UI_UX_AND_MARKETING_TURNKEY_GUIDE](../UI_UX_AND_MARKETING_TURNKEY_GUIDE_SOURCES_AND_ORGANIZATION.md) Part 8, and [STARRED_AND_REFERENCE_REPOS.md](../STARRED_AND_REFERENCE_REPOS.md) (Integrated column or new rows).

---

_Simulation disclaimer: All litigation outputs are for litigation support only. Not legal advice. Attorney review required._
