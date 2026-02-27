# New Capability Checklist — Platform Instructions

> **When creating any new tool, toolkit, agent, skill, or platform capability**, follow this checklist. Ensures constitution alignment, skill creation, and index updates.

**Referenced by**: `master-project-rules.mdc`, `.github/agents/my-agent.agent.md`, `create-skill` skill.

---

## 1. Read Master Instructions First

Before implementing a new capability:

| Document      | Path                                     | Purpose                                      |
| ------------- | ---------------------------------------- | -------------------------------------------- |
| Constitution  | `docs/constitution.md`                   | Non-negotiable principles, human-in-the-loop |
| Agent spec    | `.github/agents/my-agent.agent.md`       | Ontology skills, compliance, provenance      |
| Master rules  | `.cursor/rules/master-project-rules.mdc` | Structure, naming, workflow                  |
| Create-skill  | `.cursor/skills/create-skill/SKILL.md`   | Skill format, placement, trigger scenarios   |
| Sources index | `docs/SOURCES_AND_EMULATION_INDEX.md`    | Top sources per action; virtuous loop        |
| Systems best practices | `docs/LLM_AI_MULTIAGENT_AND_SYSTEMS_BEST_PRACTICES.md` | Design, setup, naming, structure for LLMs, agents, MCP, dev tools, robotics; **all systems from now on** follow this. |

---

## 2. Create a Cursor Skill

Every new capability must have a corresponding skill so agents know when and how to use it.

- **Location**: `.cursor/skills/{capability-name}/` (project) or `~/.cursor/skills/` (personal)
- **Format**: `SKILL.md` with YAML frontmatter (`name`, `description`), Instructions, Examples
- **Reference**: Use `create-skill` skill when authoring
- **Trigger terms**: Include in `description` so the agent auto-applies when relevant

Example: File management toolkit → `.cursor/skills/file-management-toolkit/SKILL.md`

---

## 3. Use Ontology Skills (When Applicable)

When creating schemas, configs, lists, or entity names:

| Need                           | Skill                                            |
| ------------------------------ | ------------------------------------------------ |
| Taxonomy, JSON schemas, naming | `.cursor/skills/ontology-schema-syntax/SKILL.md` |
| Task lists, projects, backlogs | `.cursor/skills/lists-todos-projects/SKILL.md`   |
| Entity names, relationships    | `.cursor/skills/names-and-connections/SKILL.md`  |

---

## 4. Update Indexes and Consolidation

| Change                           | Update                                                                                                                                                                                                                |
| -------------------------------- | --------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| New repo                         | `docs/cross-system-index.md` (GitHub Repositories table)                                                                                                                                                              |
| New repo                         | `docs/CONSOLIDATION_AND_REPO_STATUS.md` (canonical map, add to ROUTES or bootstrap)                                                                                                                                   |
| New repo                         | `docs/REFERENCE_PATTERNS_AND_EXAMPLE_REPOS.md` (if new example/template)                                                                                                                                              |
| File/evidence                    | Emulate `docs/modules/lexvault.md`; entity schemas → `docs/modules/ontology.md`                                                                                                                                       |
| New agent/skill                  | `agents/MASTER_AGENT_INDEX.md` (Agent Matrix, Skill Matrix)                                                                                                                                                           |
| New playbook                     | `config/playbooks.yaml`                                                                                                                                                                                               |
| New app/MCP/API from vendor list | Run `python3 scripts/recommend-tools-from-list.py --input <file-or-stdin>`; use report to add to canonical, matrix, inventory; see [TOOL_LIST_UPLOAD_AND_RECOMMENDATIONS.md](TOOL_LIST_UPLOAD_AND_RECOMMENDATIONS.md) |

---

## 5. New tool from a list of apps/MCPs/APIs

When the new capability comes from a **vendor dashboard, audit, or pasted list** of apps/MCPs/APIs:

1. Save the list as a YAML file (see `examples/tool-list-upload-example.yaml`) or paste into stdin.
2. Run: `python3 scripts/recommend-tools-from-list.py --input <path-or--> [--output report.md] [--yaml]`.
3. Use the report to: add to `config/canonical-mcp-connectors.yaml` (if MCP/connector) → sync; add to `config/agent-mcp-function-matrix.yaml`; update `docs/MODULAR_TOOLS_AND_ENDPOINTS_INVENTORY.md` and `docs/MASTER_MCP_CONNECTORS_APIS.md`.
4. Customize recommendations by editing `config/tool-recommendation-capability-map.yaml` if needed.

---

## 6. Constitution Alignment

- **Human-in-the-loop**: AI outputs (e.g., file Clerk renames) require human review note in README/docs
- **Explainability**: Document audit trail (e.g., `processing_log.json`)
- **Simulation disclaimer**: If output is used in legal/litigation context, add disclaimer

---

## Summary Checklist

- [ ] Read `docs/constitution.md`, `.github/agents/my-agent.agent.md`, `master-project-rules.mdc`
- [ ] Create skill under `.cursor/skills/{name}/`
- [ ] Use ontology skills for schemas/lists/entities
- [ ] If new tool from vendor/list: run `scripts/recommend-tools-from-list.py` and apply recommendations (canonical, matrix, inventory)
- [ ] Update `docs/cross-system-index.md` if new repo
- [ ] Update `agents/MASTER_AGENT_INDEX.md` if new agent/skill
- [ ] Add constitution alignment notes (human review, audit, disclaimer as applicable)
- [ ] Check SOURCES_AND_EMULATION_INDEX for this action type; apply virtuous loop
