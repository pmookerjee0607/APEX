# APEX
### AI-Powered Execution Framework

APEX is an execution framework for AI-enabled program delivery. Skills, agents, plugins, and a context system that make Claude operate as a program-aware delivery instrument rather than a generic assistant.

> Status: Phase 1 prototype. Not yet published. The skill layer, context template, and plugin are complete.

---

## Architecture

APEX has four layers. Each depends on the one below it.

**Layer 1. Context.** A loaded program context every downstream output operates within. Without it, outputs are generic. With it, outputs are program-specific and immediately usable. The runtime template is `APEX_CONTEXT.md`: program type, governance model, tooling stack, team structure, milestones, constraints, terminology. Populate it once per program and load it at session start.

**Layer 2. Skills.** Eight domain skill files. Each tells Claude how to operate in one delivery domain: role, input format, output specification, prompt templates, worked example, anti-patterns, quality bar. Skills are the atomic units. They can be invoked directly by a human, by an agent (Phase 2), or by the orchestrator (Phase 3).

**Layer 3. Domain Agents** *(Phase 2).* Each skill becomes an agent with a defined task loop. A skill tells Claude how to operate; an agent runs the workflow without step-by-step prompting and returns structured output.

**Layer 4. Orchestration** *(Phase 3).* The Delivery Command Agent receives natural-language inputs, routes them to the right agent sequence, holds program state across a session, and returns synthesised output.

A shared governance layer sits underneath all four. Four rules: conflicting input resolution, disclosure boundary, escalation autonomy, and authorization precondition. Skills and agents reference these rules rather than restating them, so behaviour stays consistent across domains.

---

## What's available today

Phase 1 is functionally complete. The skill layer, context template, and Claude Code plugin are all built and live-verified.

| File | Domain | Primary output |
|---|---|---|
| `pm-planning.md` | Project planning and WBS | Work breakdown structures, schedules, dependency maps, PI planning prep |
| `pm-risk.md` | Risk management | RAID logs, pre-mortems, mitigation plans |
| `pm-reporting.md` | Status reporting | RAG status, executive narratives, steering packs |
| `pm-release.md` | Release and testing | Go/no-go checklists, UAT plans, cutover runbooks |
| `pm-resources.md` | Resource management | Conflict maps, allocation plans, capacity models |
| `pm-financials.md` | Project financials | EAC and ETC models, variance narratives |
| `pm-client.md` | Client management | Governance packs, escalation frameworks |
| `pm-governance.md` | PMO and governance | KPI dashboards, portfolio reporting, gate packs |

`APEX_CONTEXT.md` is a fillable program-context template. Populate it once per programme and load it alongside any skill.

---

## How to use the skill files today

Three patterns, in order of friction.

**Direct.** Open the skill file you need in Claude. Use the prompt templates inside it. The output is built to paste into a steering deck, a Confluence page, or a runbook without rewriting.

**With context.** Populate `APEX_CONTEXT.md` for your program once. Load both files at session start. Same skill prompts, now program-aware.

**Via Claude Code slash commands.** The `apex` plugin registers eight commands against the skill layer:

```
/status-report        → pm-reporting.md
/raid-extract          → pm-risk.md
/risk-premortem         → pm-risk.md (pre-mortem variant)
/go-no-go               → pm-release.md
/resource-conflict      → pm-resources.md
/financial-variance     → pm-financials.md
/release-readiness      → pm-release.md
/meeting-intel           → pm-governance.md, then pm-risk.md
```

`/meeting-intel` runs as a two-step sequence: governance items are extracted first, then risk and RAID items are extracted informed by that governance context, rather than two independent calls.

`pm-planning.md` and `pm-client.md` are not wrapped by a command. Their output is too program-specific or audience-dependent for a single command framing and are intended for direct skill invocation instead.

Install: `claude --plugin-dir /path/to/apex/plugin`

---

## Quality standard

Every output should be immediately usable without editing. Not a draft, not a starting point, a deliverable. Status reports paste into steering decks. RAID logs paste into Confluence. Go/no-go checklists list hard stops with owners and verification methods. If something needs rewriting before you can use it, treat that as a defect in the skill, not in the prompt.

This is the bar APEX is built against.

---

## Why this exists

Program delivery is not generic. A status report for a $50M public-sector modernisation is structurally different from a sprint update. A go/no-go for a regulated cutover is different from a feature release. APEX exists because the gap between "Claude can help with delivery" and "Claude is a program-aware delivery instrument" is closed by structure, not by a clever prompt.

On one programme, disciplined risk identification with assignable, tracked mitigation took portfolio slippage from over 20% to under 8%. APEX encodes that discipline so it is repeatable across programmes, teams, and contexts, not lost when the strong PM rotates off.

---

## Roadmap

| Phase | Focus | Status |
|---|---|---|
| 1 | Skill layer, plugin, context template | Complete |
| 2 | Domain agents: Program Intelligence, RAID, Release Readiness | Planned |
| 3 | Delivery Command Agent, Jira / M365 / ServiceNow / Salesforce integrations | Planned |

---

## Architectural lineage

APEX is the operational execution layer of a broader framework, the AI-Enabled Delivery Framework (AIDF), which defines the philosophy and maturity model for AI-enabled delivery. The two are designed to compose. The AIDF is documented separately.

---

## Author

Built and maintained by Projit Mookerjee, Director of Client Engagement and Digital Delivery. Practitioner-built, not vendor-built.
