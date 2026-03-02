# Master File Commit Review and Final Decision System — Claude Code, Cursor, Codex

**Purpose:** Define the system for **retroactive review** of any commit to master files by **Claude Code**, **Cursor**, and **Codex**; **gather** responses, new ideas, and modifications from all three; **rerun** (consolidate and re-review); and **Claude Code calls the final decisions** on **OneWish OS level matters**.

**Governance:** [constitution.md](constitution.md); [ONEWISH_PROTOCOL.md](ONEWISH_PROTOCOL.md) §5 (never-miss), §6 (this system); [NEVER_MISS_INSTRUCTIONS.md](NEVER_MISS_INSTRUCTIONS.md). **OneWish OS level matters** = constitutional, protocol, master files, propagation, governance, rigid review, and improvement. **Every-response suggestions (constitution §6.6):** Each review output (Claude Code, Cursor, Codex) must include at least one suggestion (next moves, concepts, additions, concerns, best practices, top repos, protections) with clear reasoning; this review **further defines and/or clarifies** those suggestions.

---

## 1. Trigger

| Trigger                      | When                                                                                                                                                                                                                                                                                                                                          |
| ---------------------------- | --------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| **Commit to master files**   | Any commit (or push) that touches **master files** in the master repo (CURSOR CLOUD AGENTS): constitution, protocol, MASTER_INDEX, never-miss docs, config/repos.yaml, entry points (AGENTS.md, CLAUDE.md), sync/route scripts, or any doc listed in [MASTER_FILES_AND_REVIEW_BEFORE_ACTION.md](MASTER_FILES_AND_REVIEW_BEFORE_ACTION.md) §2. |
| **Optional: push to master** | When policy requires, the same flow runs after **push** to the default branch (e.g. after merge to main).                                                                                                                                                                                                                                     |

**Scope of “master files”:** Governance (§2.1), structure/repo map (§2.2), architecture/integrations (§2.3), entry points (§2.4) in MASTER_FILES_AND_REVIEW_BEFORE_ACTION; plus ONEWISH_PROTOCOL, NEVER_MISS_INSTRUCTIONS, full-review-summary mandatory checklist, and any file synced via route-constitution or sync-all-repos-and-review.

---

## 2. Retroactive review by Claude Code, Cursor, and Codex

Each of the three dev tools **reviews the commit(s) to master files** retroactively:

| Dev tool        | Role in review                                                                                                                                                                                                | Output |
| --------------- | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | ------ |
| **Claude Code** | Reviews committed changes against constitution, protocol, rigid review (usability, operability, efficiency), and improvement triggers. Produces **responses**, **new ideas**, and **proposed modifications**. |
| **Cursor**      | Reviews same commit(s); checks entry points (AGENTS.md, rules), sync/route impact, and agent/playbook alignment. Produces **responses**, **new ideas**, and **proposed modifications**.                       |
| **Codex**       | Reviews same commit(s); checks config, scripts, and repo alignment per DEV_TOOLS_REPO_ALIGNMENT. Produces **responses**, **new ideas**, and **proposed modifications**.                                       |

**Retroactive** = review happens **after** the commit (and optionally after push). The goal is to capture feedback and improvements from all three tools so nothing is missed and the next cycle (rerun, final decision) can incorporate them.

---

## 3. Gather responses, new ideas, and modifications

**Gathering:** Collect all outputs (responses, new ideas, modifications) from Claude Code, Cursor, and Codex into a single, versioned artifact so they can be used in the rerun and final decision.

| Element                | Description                                                                                                                                                                                                            |
| ---------------------- | ---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| **Canonical location** | `docs/audits/commit-review-gathered/` — one file per review cycle, e.g. `commit-review-YYYY-MM-DD-HHMM.md` or `commit-review-<git-rev-or-branch>.md`.                                                                  |
| **Contents**           | For each dev tool: (1) **Responses** (summary of review; pass/fail/notes); (2) **New ideas** (suggestions for protocol, master files, or process); (3) **Modifications** (concrete edits or checklist items to apply). |
| **Format**             | Markdown with clear sections per tool (Claude Code, Cursor, Codex); optional JSON sidecar for machine-readable (e.g. `commit-review-YYYY-MM-DD.json`) if needed for automation.                                        |
| **Who gathers**        | The operator or agent running the “commit review” flow: run the three reviews (or trigger them), then merge outputs into the canonical file for that cycle.                                                            |

**Template (per cycle):**

```markdown
# Commit review gathered — YYYY-MM-DD [optional: git rev or branch]

Commit(s): <rev or range>
Master files touched: <list or link to diff>

## Claude Code

- **Responses:** ...
- **New ideas:** ...
- **Modifications:** ...

## Cursor

- **Responses:** ...
- **New ideas:** ...
- **Modifications:** ...

## Codex

- **Responses:** ...
- **New ideas:** ...
- **Modifications:** ...
```

---

## 4. Rerun

After gathering, **rerun** so the system incorporates the collected feedback:

| Step        | Action                                                                                                                                                                                                                                                                                 |
| ----------- | -------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| **Rerun 1** | **Full Review** (or relevant subset) with the **gathered** file as input: run `./scripts/run-full-review.sh` (or equivalent) and ensure the mandatory checklist in `docs/audits/full-review-summary.md` is completed **in light of** the gathered responses, ideas, and modifications. |
| **Rerun 2** | **Route and sync:** If any modification affects governance or master files, run `./scripts/route-constitution-to-repos.sh` and/or `./scripts/sync-all-repos-and-review.sh` so propagation reflects the post-review state.                                                              |
| **Rerun 3** | **Update master files** where the **final decision** (see §5) has approved a modification: apply only those changes that Claude Code has approved as final; then commit (and push) from master.                                                                                        |

**Rerun** = run the review and propagation again with the gathered input; then apply only the final-approved changes.

---

## 5. Claude Code calls the final decisions on OneWish OS level matters

**Authority:** For **OneWish OS level matters**, **Claude Code** is the designated authority to **call the final decisions**. OneWish OS level matters include:

- Constitutional alignment (human-in-the-loop, claim typing, audit, bias/safety, simulation disclaimer)
- Protocol and never-miss propagation (what gets routed/synced, when)
- Master file content and structure (MASTER_INDEX, MASTER_FILES_AND_REVIEW_BEFORE_ACTION, entry points)
- Rigid review outcomes (usability, operability, efficiency) for protocol-scope changes
- Improvement triggers and what gets captured (postmortem, patterns-that-work, lessons)
- Which gathered responses, ideas, or modifications from Cursor and Codex are **adopted** vs. deferred or rejected

**Process:**

1. **Input:** Gathered file from §3 and rerun results from §4.
2. **Claude Code** (operator or agent in Claude Code) reviews the gathered feedback and rerun output and **decides**:
   - Which modifications to **apply** to master files or protocol
   - Which new ideas to **accept** (and how to implement) or **defer**
   - Any **overrides** or **reconciliations** when Cursor and Codex disagree
3. **Output:** Final decisions are recorded (e.g. in the same `docs/audits/commit-review-gathered/` cycle file under a **Final decisions (Claude Code)** section, or in a short decision log). Only final-approved changes are committed to master.

**Cursor and Codex** contribute fully to the gathered feedback and rerun; they do **not** override Claude Code on OneWish OS level matters. Domain-specific or repo-specific decisions may follow tool-specific policy where documented.

---

## 6. End-to-end flow (summary)

1. **Commit** (and optionally push) to master files.
2. **Retroactive review:** Claude Code, Cursor, and Codex each review the commit(s) and produce responses, new ideas, and modifications.
3. **Gather:** Merge all outputs into one file under `docs/audits/commit-review-gathered/` for that cycle.
4. **Rerun:** Full Review (and route/sync as needed) using the gathered file; apply only changes that are approved in the final decision step.
5. **Final decision:** Claude Code calls the final decisions on OneWish OS level matters; record them; apply approved modifications to master and commit (and push).

---

## 7. Scripts and automation (optional)

- **Super agent ask and gather:** `./scripts/run-super-agent-ask-and-gather.sh` — Prints the **canonical ask** (for pasting into Codex, Cursor, and Claude Code) and creates a timestamped placeholder in `docs/audits/commit-review-gathered/super-agent-eval-YYYY-MM-DD-HHMM.md`. Claude Code then **compiles** the three outputs and writes the **memorialized document** to `docs/audits/ONEWISHOS_SUPER_AGENT_COMPILED_EVALUATION-YYYY-MM-DD.md`. See [SUPER_AGENT_ASK_AND_COMPILATION.md](SUPER_AGENT_ASK_AND_COMPILATION.md).
- **Trigger script (optional):** A script or CI job that, on commit/push to master, creates a placeholder gathered file and notifies or queues the three reviews (e.g. `scripts/trigger-commit-review.sh` or a GitHub Action).
- **Gather script (optional):** A script that merges three input files (one per tool) into the canonical gathered file for that cycle.
- **Rerun:** Existing `run-full-review.sh`, `route-constitution-to-repos.sh`, `sync-all-repos-and-review.sh` are used; no new script required for “rerun” itself.

When automation is added, update this section and [NEVER_MISS_INSTRUCTIONS.md](NEVER_MISS_INSTRUCTIONS.md) so the commit-review flow remains in the never-miss checklist where applicable.

---

## 8. References

| Doc                                                                                  | Purpose                                                                      |
| ------------------------------------------------------------------------------------ | ---------------------------------------------------------------------------- |
| [constitution.md](constitution.md)                                                   | Governance; Full Review; master-synced/never-miss files                      |
| [ONEWISH_PROTOCOL.md](ONEWISH_PROTOCOL.md)                                           | Never-miss (§5); this system (§6); rigid review; improvement                 |
| [NEVER_MISS_INSTRUCTIONS.md](NEVER_MISS_INSTRUCTIONS.md)                             | Sequence (sync → route → review → commit → push); dev tools commit to master |
| [MASTER_FILES_AND_REVIEW_BEFORE_ACTION.md](MASTER_FILES_AND_REVIEW_BEFORE_ACTION.md) | What counts as master files; review before action                            |
| [audits/full-review-summary.md](audits/full-review-summary.md)                       | Mandatory checklist; used in rerun                                           |

_Maintain at: docs/MASTER_FILE_COMMIT_REVIEW_AND_FINAL_DECISION_SYSTEM.md. Update when adding automation, changing canonical paths, or changing final-decision authority._
