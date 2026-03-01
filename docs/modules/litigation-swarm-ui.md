# Litigation Swarm — UI/UX & Web Application

> Source: Google Drive "Litigation Swarm Website.md", "lex-vault-litigation-swarm-prd.md", Notion "Litigation Force AI PRD", Vercel/Replit deployments

## Overview

Litigation Swarm is the web application layer of LitigationForce.AI — the attorney-facing interface for case intake, document review, RICO analysis, timeline visualization, and report generation. Deployed on Vercel and Replit.

## Deployments

| Application          | Platform | URL                 | Status              |
| -------------------- | -------- | ------------------- | ------------------- |
| LitigationForce Main | Vercel   | litigationforce.com | Domains need config |
| Smithwick.AI         | Vercel   | smithwick.ai        | Domains need config |
| Talian Ventures      | Vercel   | talianventures.com  | Domains need config |
| SwarmRICO            | Replit   | Replit deployment   | Active              |
| Verital-Legal-Tech   | Replit   | Replit deployment   | Active              |

Vercel Team: `litigationforce1`
Vercel Project: `litigationagentsmultimodalchat`

## Design System

> Source: Google Drive "Litigation Swarm Website.md". **Canonical tokens**: `docs/FUNDAMENTAL_STRATEGIES_AND_SPECIFICATIONS.md` §4.

### Visual Identity

| Element            | Specification                                  |
| ------------------ | ---------------------------------------------- |
| Primary Background | Dark navy `#0A0E27`                            |
| Accent Color       | Electric cyan `#00E5FF`, neon green `#39FF14`  |
| Aesthetic          | Cyberpunk-inspired "weapon against injustice"  |
| Typography         | Modern monospace + clean sans-serif            |
| Animation          | High-energy particle effects, grid backgrounds |
| Tone               | Empowering small attorneys to fight RICO fraud |

### Color Tokens (See FUNDAMENTAL_STRATEGIES §4)

- Track CA: `#3B82F6` | Track TX: `#F59E0B` | Track RICO: `#EF4444`
- Verdict: green (take), cyan (lean), amber (borderline), red (decline)

### Design Principles

1. **Dark-mode first** — reduce eye strain for long review sessions
2. **Data-dense layouts** — attorneys need information density, not whitespace
3. **Color-coded tracks** — Blue (CA), Orange (TX), Red (RICO) consistently
4. **Interactive visualizations** — timelines, knowledge graphs, damages charts
5. **Mobile-responsive** — key features accessible on phone for court access
6. **Accessibility** — WCAG 2.1 AA minimum

## Page Architecture

### Core Pages

| Page            | Route                    | Purpose                                     |
| --------------- | ------------------------ | ------------------------------------------- |
| Login           | `/login`                 | Email magic link login                      |
| Dashboard       | `/dashboard`             | KPI dashboard, case overview, active tasks  |
| Cases           | `/cases`                 | Case list, matter management                |
| Case Detail     | `/cases/:id`             | Single case workspace (all tracks)          |
| Documents       | `/cases/:id/documents`   | Document review, classification, privilege  |
| Timeline        | `/cases/:id/timeline`    | Interactive chronological visualization     |
| Knowledge Graph | `/cases/:id/graph`       | Neo4j entity relationship visualization     |
| RICO Analysis   | `/cases/:id/rico`        | Six-element analysis, pattern scoring       |
| Damages         | `/cases/:id/damages`     | Damages modeling and calculation            |
| Filings         | `/cases/:id/filings`     | Filing draft generation and review          |
| Productions     | `/cases/:id/productions` | Production set management                   |
| Agents          | `/agents`                | Agent status monitor, task management       |
| Settings        | `/settings`              | User preferences, API keys, team management |

### Authentication

- Supabase Auth with magic link login
- Environment variables: `NEXT_PUBLIC_SUPABASE_URL`, `NEXT_PUBLIC_SUPABASE_ANON_KEY`
- RBAC: Attorney, Paralegal, Admin, Client roles
- Session management with secure cookies

## Component Library

### Case Dashboard Widgets

| Widget           | Data Source                       | Refresh                |
| ---------------- | --------------------------------- | ---------------------- |
| Active Tasks     | Blackbox API `/api/tasks`         | 10s polling            |
| Case Health      | Pattern Score + Evaluator Summary | On analysis completion |
| Document Stats   | LexVault counts by classification | 5 min cache            |
| Timeline Preview | Last 10 events                    | On evidence ingest     |
| Risk Alerts      | Risk Monitor agent output         | Real-time SSE          |

### Document Review Interface

```
┌─────────────────────────────────────────────────────────┐
│  Document Viewer (split panel)                          │
│                                                         │
│  ┌─────────────────┐  ┌──────────────────────────────┐ │
│  │ Original (PDF)  │  │ Extracted Text + Annotations │ │
│  │                 │  │                              │ │
│  │ [Pan] [Zoom]    │  │ Highlighted entities         │ │
│  │ [Rotate]        │  │ Claim type badges            │ │
│  │                 │  │ Evidence link indicators      │ │
│  └─────────────────┘  └──────────────────────────────┘ │
│                                                         │
│  ┌──────────────────────────────────────────────────┐  │
│  │ Properties | Privilege | Classification | Notes  │  │
│  │                                                  │  │
│  │ Type: Contract    RICO: Critical                 │  │
│  │ Custodian: R.B.   Privilege: ⚠️ Review Needed    │  │
│  │ Track: Federal    Confidence: 0.94               │  │
│  │                                                  │  │
│  │ [Approve] [Flag Privilege] [Escalate] [Annotate] │  │
│  └──────────────────────────────────────────────────┘  │
└─────────────────────────────────────────────────────────┘
```

### RICO Analysis Dashboard

| Component            | Visualization                                   |
| -------------------- | ----------------------------------------------- |
| Enterprise Map       | Force-directed graph of enterprise participants |
| Pattern Timeline     | Predicate acts plotted chronologically          |
| Element Scores       | Radar chart of 6 RICO element scores            |
| Rule 9(b) Checklist  | Who/what/when/where/how/why per predicate       |
| Continuity Indicator | Open-ended vs closed-ended with evidence        |

## Module Selection

For choosing components and packages, see `docs/MODULE_ARCHITECTURE_AND_PLATFORM_STACK.md` and `config/module-selection.yaml`. Primary: shadcn/ui, Recharts, react-force-graph, vis-timeline. v0: `docs/V0_SETUP_AND_INSTRUCTIONS.md`.

---

## Tech Stack

| Layer      | Technology                               |
| ---------- | ---------------------------------------- |
| Framework  | Next.js (App Router)                     |
| Auth       | Supabase Auth (magic link)               |
| Database   | Supabase Postgres                        |
| Storage    | Supabase Storage + Box (LexVault)        |
| Styling    | Tailwind CSS + shadcn/ui                 |
| Charts     | Recharts / D3.js                         |
| Graph Viz  | vis.js / react-force-graph (Neo4j)       |
| Timeline   | vis-timeline / custom React component    |
| Deployment | Vercel (primary), Replit (staging)       |
| AI Backend | Blackbox Cloud API, OpenAI Responses API |

## Integration with Master Repo

| UI Component         | Maps to Repo Artifact                            |
| -------------------- | ------------------------------------------------ |
| Agent status monitor | `scripts/blackbox_client.py` (polling, SSE logs) |
| Document viewer      | `docs/schemas/evidence-object.schema.json`       |
| RICO dashboard       | `docs/schemas/pattern-score.schema.json`         |
| Timeline view        | `docs/schemas/timeline-event.schema.json`        |
| Filing editor        | `config/playbooks.yaml` → filing_generator       |
| Privilege review     | `.cursor/rules/security-evidence.mdc`            |
| Damages calculator   | `config/playbooks.yaml` → damages_modeler        |
| Bundle export        | `docs/schemas/bundle-package.schema.json`        |

## UI/UX and marketing turnkey

For **design system alignment**, **multi-site organization**, and **sources** (Figma, Mobbin, Framer, Node/Next.js, NN/g): see [docs/UI_UX_AND_MARKETING_TURNKEY_GUIDE_SOURCES_AND_ORGANIZATION.md](../UI_UX_AND_MARKETING_TURNKEY_GUIDE_SOURCES_AND_ORGANIZATION.md). Use it to keep Litigation Swarm tokens and pages consistent with marketing sites (litigationforce.com, onewish.io, talk).

## Notion References

| Page                          | URL                                                              | Content                               |
| ----------------------------- | ---------------------------------------------------------------- | ------------------------------------- |
| Litigation Force AI PRD       | [Notion](https://www.notion.so/d8bdd1da69c1494f83af91dee6614cee) | UI/UX requirements, workflow support  |
| PRD v2.0 Hierarchical Context | [Notion](https://www.notion.so/79fe10580a59485894a137d48565ae8b) | Agent IDs, context system             |
| Deep Dive — Deployment        | [Notion](https://www.notion.so/8bf25bca803b476bab14e5628e156a62) | Terraform, GitOps, CI/CD, autoscaling |
