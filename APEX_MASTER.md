# APEX — AI-Powered Execution Framework
## Master Design Document
*Owner: Projit Mookerjee | Last updated: June 2026 | Status: Phase 1 in design*

---

## 00 — How to Use This File

This is the single source of truth for the APEX ecosystem. Every new chat working on APEX reads this file first. No re-explaining architecture, naming, or decisions already made. When a session produces a decision, output, or completed artifact, the BUILD LOG (APEX_BUILD_LOG.md) is updated. This file covers design intent, architecture, and standing decisions. The build log covers execution state.

**Reading order for a new chat:**
1. This file (APEX_MASTER.md) — full read
2. APEX_BUILD_LOG.md — scan completed items, note current phase and next task
3. Proceed without re-litigating anything marked DECIDED

---

## 01 — What APEX Is

APEX is the operational execution layer of the AI-Enabled Delivery Framework (AIDF). Where the AIDF defines the philosophy and maturity model for AI-enabled delivery, APEX is the machinery that operationalises it: skills, agents, plugins, and a context system that makes Claude behave as a program-aware delivery intelligence, not a generic AI assistant.

**The product family (canonical hierarchy):**

```
AI in PM Guide          — learning layer (live, GitHub Pages)
PM Prompt Kit           — prompt layer (live, GitHub Pages)
AI-Enabled Delivery Framework (AIDF)  — framework layer (HTML artifact)
APEX                    — execution layer (this build)
```

Each asset links to the next. APEX is positioned as "the framework that makes the AIDF run." Externally it is described as: *"The AIDF tells you what AI-enabled delivery looks like. APEX gives you the machinery to run it."*

---

## 02 — Naming and Brand

**Full name:** APEX — AI-Powered Execution Framework  
**Short form:** APEX (always uppercase)  
**Parent brand:** AIDF (AI-Enabled Delivery Framework)  
**Author brand:** Projit Mookerjee — practitioner, not vendor

**Design system (inherited from portfolio site, must match exactly):**
- Fonts: Fraunces (display/serif) + Epilogue (body) + JetBrains Mono (mono/labels)
- Palette: ink (#0f1117) / paper (#f8f5ef) / cream (#ede9e0) / accent (#c8410a orange)
- All external HTML artifacts match the portfolio site nav branding and footer format
- Portfolio site is the design master: pmookerjee0607.github.io/projitmookerjee

**Voice and tone (all external content):**
- Practitioner-led, specific, experience-grounded
- No advisory tone, no promotional framing, no AI-generated structural tells
- No em dashes anywhere
- No bullet arrows
- Sounds like a senior delivery professional wrote it, not an AI assistant

**Confidentiality rule:** All external-facing APEX content is intentionally free of client names, employer names, and confidential data. Sapiens, WCB Saskatchewan, and KPMG are internal context only and must never appear in published assets. Descriptive labels replace specifics where needed.

---

## 03 — Architecture

APEX has four layers. Each layer depends on the one below it.

### Layer 1 — Context + Integration
The program-awareness foundation. Every agent and skill operates within a loaded context. Without it, outputs are generic. With it, outputs are program-specific and immediately usable.

**APEX_CONTEXT.md** is the runtime context template. It captures:
- Program type (enterprise transformation / SaaS migration / public sector / regulated)
- Client governance model and stakeholder map
- Active tooling stack (Jira, M365, ServiceNow, Salesforce — any combination)
- Team structure (FTEs, vendors, geographies)
- Active milestones and known constraints
- Risk and compliance environment
- Program-specific terminology and naming conventions

In the external version, APEX_CONTEXT.md ships as a fillable template. Users populate it for their program and load it at session start. In the Sapiens internal version, it is pre-populated with WCB Saskatchewan program specifics.

**Integration targets (phased):**
- Phase 1: Context file only (no live integrations)
- Phase 3: Jira via MCP, M365 via MCP, ServiceNow via API, Salesforce via API

### Layer 2 — Skills (.md files)
Eight skill files, one per delivery domain. Each skill is a structured markdown file that tells Claude how to operate in that domain: role, input format, output format, prompt templates, worked example, anti-patterns, and quality bar.

Skills are the atomic units. Agents invoke them. The plugin registers them. Users can also invoke them directly in Claude Code via slash commands.

**The eight skills (canonical names):**

| Skill file | Domain | Primary output |
|---|---|---|
| pm-planning.md | Project Planning & WBS | Work breakdown structures, schedules, dependency maps |
| pm-risk.md | Risk Management | RAID logs, pre-mortems, mitigation plans |
| pm-reporting.md | Status Reporting | RAG status, exec narratives, steering packs |
| pm-release.md | Release & Testing | Go/no-go checklists, UAT plans, cutover runbooks |
| pm-resources.md | Resource Management | Conflict maps, allocation plans, capacity models |
| pm-financials.md | Project Financials | EAC/ETC models, variance narratives, time reports |
| pm-client.md | Client Management | Governance packs, escalation frameworks, comms |
| pm-governance.md | PMO & Governance | CoE frameworks, KPI dashboards, portfolio reporting |

**Skill file structure (every file follows this exactly):**
```
# [Skill Name] — APEX Skill
## Role Definition
## Input Requirements
## Output Specification
## Prompt Templates (3–5, numbered)
## Worked Example
## Anti-Patterns
## Quality Bar
## Sapiens Extension (internal only, clearly marked)
```

Every skill file inherits the Governance Block defined in 03a. Skills do not restate these rules; they reference them and, where the domain requires it, define the domain-specific application of a rule (for example, what "critical path" means in a risk context vs. a reporting context).

### 03a — Governance Block (Cross-Skill, DECIDED)

This block is the shared judgment layer underneath all eight skills and, later, all domain agents. It exists because every domain — reporting, risk, financials, client, governance — hits the same three decision points: what to do when inputs disagree, what must be disclosed regardless of audience, and what an agent is allowed to act on without a human. Defining these once prevents drift between skill files and gives the Layer 3 agents a single inherited contract instead of eight slightly different ones.

Generic by design. Each rule ships with a stated default and an explicit override path through APEX_CONTEXT.md, so an industry or program variant (regulated public sector, fixed-price commercial, internal-only initiative) can sharpen a rule without rewriting it. These rules reflect best-current judgment, not a final specification — they are expected to be stress-tested against real program scenarios once the system is functional, and refined or scaled based on what that testing surfaces. Treat each rule as the sharpest reasonable default for now, not a permanent boundary.

**1. Conflicting Input Resolution**
When two inputs to a skill disagree (a system metric vs. a qualitative signal; two data sources; a stated plan vs. observed reality), the skill does not silently pick one. It surfaces the conflict and the more cautious signal sets the floor for any status, severity, or confidence output. Default reasoning: a quantitative signal describes the past; a qualitative or forward-looking signal often describes what's about to happen to the data. Treat the latter as at least as material until the program's context file specifies otherwise.

*Scope note:* this rule governs disagreement between inputs, not the mechanics of how a domain converts inputs into a score (e.g., a probability × impact matrix, a roll-up formula, a KPI threshold). The scoring mechanism itself is domain-specific logic and lives in the relevant skill file. But the facts and signals fed into that mechanism are not exempt from this rule simply because they're about to be scored — if a stated plan or a PM's qualitative call disagrees with observed reality before scoring happens, Rule 1 applies to resolve that disagreement first, and the resolved (more cautious) input is what gets scored.

**2. Disclosure Boundary**
Audience calibration governs tone, framing, and level of internal detail. It never governs whether something gets disclosed. Anything contractually, legally, or compliance-mandated, or material to schedule/budget/scope commitments made to a client or sponsor, is present in every audience version of an output, regardless of how softly it's framed. Default on ambiguity is disclosure; a human reviewer downgrades if appropriate. This default can be sharpened (not loosened) by APEX_CONTEXT.md for regulated environments.

**3. Escalation Autonomy**
No skill or agent auto-escalates, auto-notifies externally, or takes a downstream action on a deteriorating, critical, or high-severity finding. The skill produces a recommendation. Anything touching the critical path, a committed deliverable, a client-facing commitment, or a financial threshold is routed for explicit human sign-off before any communication or action follows. Items without that profile may be surfaced informationally in routine output without a sign-off gate, since visibility carries no action risk on its own. The line is: consequential impact requires a human decision; visibility into a trend does not.

**4. Authorization Precondition**
Some skills produce recommendations or outputs whose validity depends on a binary authorization having been granted by a named authorizer and recorded as an artifact, before the recommended action can proceed. The framework calls such a mechanism a Gate. A Gate is not subject to severity weighting, completion-percentage averaging, or "in progress" framing: it is satisfied or it is not. While an applicable Gate is unsatisfied, the skill cannot endorse the underlying action regardless of how strong the rest of the picture is. Default reasoning: silence about whether a Gate applies is not evidence that none does. When program context does not make Gate applicability clear, the skill flags the possibility and asks, rather than proceeding as if unregulated.

*Scope note:* what counts as a Gate is domain-specific. Release readiness Gates (compliance, audit, regulatory sign-off) are not identical in form to portfolio stage Gates (phase-review approvals, charter approval, baseline approval) or financial Gates (budget reallocation authorization, baseline change approval, commitment-threshold sign-off). The general pattern is shared (binary, named authorizer, recorded artifact, blocking by default); the domain-specific instances live in each skill file.

*Relationship to Rule 3:* a Gate is a precondition the skill enforces on its own output. Rule 3 governs what happens when an agent detects an attempt to proceed past an unsatisfied Gate. The two interact at exactly one point: an unsatisfied Gate that is being bypassed is, by definition, a critical-path finding, and that finding is handled per Rule 3.

**Inheritance note for Layer 3/4:** when a domain skill is invoked directly by a human, these rules show up as instructions to the model. When the same skill is invoked by a Domain Agent or the Delivery Command Agent, these rules become the agent's actual autonomy boundary, not just guidance, since there's no human reviewing the intermediate output. Agent design in Layer 3 must implement Rule 3 and Rule 4 as hard stops, not prompt suggestions: Rule 3 prevents autonomous escalation on consequential findings, and Rule 4 prevents the agent from producing an endorsement output while a required Gate is unsatisfied.

### Layer 3 — Domain Agents
Each domain skill becomes an agent with a defined task loop. The distinction: a skill tells Claude how to operate; an agent runs a workflow, makes decisions at defined points, and produces structured output without requiring step-by-step user prompting.

**Phase 2 agents (build order):**
1. Program Intelligence Agent — weekly program health brief (RAG per workstream, top risks, escalation flag, recommended action). Highest-value first demonstrator for Sapiens PMO.
2. RAID Agent — structured RAID log from any unstructured input (transcript, email, notes). Directly connected to the 22-to-8% proof point.
3. Release Readiness Agent — go/no-go checklist calibrated to release type and environment. WCB variant built in parallel once Sapiens license is active.

**Agent architecture:**
- Each agent is a Claude API call with a structured system prompt drawn from the skill .md
- Defined JSON input schema
- Defined JSON output schema
- Runnable in Claude Code Phase 1-2; exposed via Cowork plugin in Phase 3

### Layer 4 — Orchestration (Delivery Command Agent)
The coordinator that ties all domain agents together. Receives natural language inputs and routes them to the right agent sequence. Maintains program state across a session. Returns synthesised output.

Example inputs the Delivery Command Agent handles:
- "Prepare this week's steering pack" → invokes Reporting + Risk + Financials agents in sequence
- "Flag resource conflicts for next sprint" → invokes Resources agent with sprint data
- "What are the top risks across all workstreams?" → invokes Risk agent with portfolio scope

For Sapiens internal deployment, the Delivery Command Agent is loaded with WCB program context at session start and behaves as a program-aware copilot throughout.

---

## 04 — Tool Roles (DECIDED — do not relitigate)

| Tool | Role | What happens here |
|---|---|---|
| Claude.ai Projects | Design + content layer | Architecture, skill file drafting, agent system prompts, context file design, QA, LinkedIn content |
| Claude Code | Build + execution layer | Writes files to disk, runs plugin, executes agents, builds HTML, manages repo |
| Cowork | Deploy + team layer | Non-developer access to APEX for Sapiens PMO team; Phase 3 only |
| GitHub Pages | Hosting | External landing page, skill files (free tier), README |

**Handoff protocol:**
- Everything is designed and approved in Claude.ai Projects first
- Claude.ai produces a Claude Code instruction block formatted as a copy-paste ready prompt
- That instruction goes to Claude Code exactly as written — no interpretation required
- Output lands in the repo and is logged in APEX_BUILD_LOG.md
- Nothing goes to Claude Code half-baked

**Chat discipline:**
- One chat per significant deliverable (one skill file, one agent, one artifact)
- Each chat starts by reading this file and the build log
- Each chat ends by producing an update for the build log
- No chat should be used to re-establish context that already exists in these files

---

## 05 — Build Phases

### Phase 1 — Foundation (Weeks 1–3)
*Goal: publishable external version + Claude Code-ready internal scaffold*
*No Sapiens license required*

Deliverables:
- /apex/skills/ directory with 8 .md skill files
- APEX_CONTEXT.md template (fillable, generic)
- apex.plugin for Claude Code (registers skills, wires slash commands)
- README.md (external documentation, doubles as framework overview)
- APEX HTML landing page (GitHub Pages, matches portfolio design system)

Slash commands registered in the plugin:
- /status-report
- /raid-extract
- /risk-premortem
- /go-no-go
- /resource-conflict
- /financial-variance
- /release-readiness
- /meeting-intel

Skill file structure in Phase 1: clean markdown, no YAML header. YAML header added in Phase 2 when the plugin is wired for programmatic skill selection.

### Phase 2 — Domain Agents (Weeks 4–6)
*Goal: three working agents via Claude API, runnable in Claude Code*

Deliverables:
- Program Intelligence Agent (JSON input/output, weekly health brief)
- RAID Agent (unstructured input → structured RAID log)
- Release Readiness Agent (release definition → go/no-go checklist)
- Agent test suite with worked examples per agent
- YAML headers added to skill files

### Phase 3 — Orchestration + Sapiens Internal (Weeks 7–10)
*Goal: Delivery Command Agent + full integration layer + Cowork deployment*
*Requires Sapiens Claude license*

Deliverables:
- Delivery Command Agent (routes inputs, sequences domain agents, synthesises output)
- Integration layer: Jira MCP, M365 MCP, ServiceNow API, Salesforce API
- WCB Saskatchewan context file (internal only, never published)
- Cowork plugin configuration for Sapiens PMO team access
- Sapiens extension sections added to relevant skill files (internal branch only)

### Phase 4 — External Product + Freemium (Ongoing from Phase 1 completion)
*Goal: traffic, audience, consulting pipeline*

Three tiers:
- **Free tier:** Framework documentation (GitHub Pages), skill .md files, APEX_CONTEXT.md template, read-only prompt library. Traffic driver. Links to PM Guide, Prompt Kit, AIDF.
- **Practitioner tier:** Claude Code plugin, full agent definitions, worked examples per domain. Accessed via email capture or GitHub star gate. Audience-building layer.
- **Consulting engagement tier (paid):** Custom APEX deployment for a specific program or PMO. Projit brings the framework, configures the context layer, runs onboarding. Monetisation path.

**LinkedIn content plan for APEX launch:** To be built as a separate 6-post sequence after Phase 1 completes. Framed as the natural next layer of the AIDF, not a standalone announcement. Each post ties back to a delivery problem APEX solves.

---

## 06 — Quality Standard

Every skill, agent, and plugin must produce output that is immediately usable without editing. Not a draft. Not a starting point. A deliverable. This is the standard that separates APEX from a prompt library and makes the consulting engagement tier defensible.

Specifically:
- Status reports: ready to paste into a steering deck or send to a client
- RAID logs: structured, owned, dated — paste directly into Confluence or ServiceNow
- Go/no-go checklists: hard stops flagged, owner roles assigned, verification method defined
- Executive narratives: board-ready tone, correct variance framing, no hedging

If an output requires the user to rewrite it before using it, the skill or agent is not finished.

---

## 07 — Sapiens Internal Deployment (Confidential)

This section contains context that informs the internal build. It must never appear in any external-facing asset.

**Internal program context:**
- Current program: WCB Saskatchewan migration to Sapiens Coresuite and Digital Suite
- Timeline: 24-month phased implementation, currently in flight
- Key external partners: KPMG (SI), Microsoft (Azure AI integration)
- Team structure: India, EU, and North America geographies
- AI integration in flight: Azure AI agents for document processing, underwriting analytics, autonomous claim triage

**Sapiens APEX deployment plan:**
- Trigger: Sapiens Claude Enterprise license activation (timing TBD)
- Entry point: Cowork plugin for PMO team (no terminal required for end users)
- Context file: WCB Saskatchewan variant of APEX_CONTEXT.md, pre-populated
- First agent to deploy internally: Program Intelligence Agent (weekly health brief)
- Skill extensions: pm-release.md and pm-governance.md get WCB-specific sections covering Coresuite implementation patterns and Digital Suite rollout sequencing
- Internal vs external separation: Sapiens-specific content lives in a private repo branch. The public repo contains only the generic, client-safe version.

**Internal rollout sequence:**
1. Deploy to Projit's own workflow first — validate and refine
2. Introduce to 2-3 peer PMs as pilot users — gather feedback
3. Present to Sapiens PMO leadership as a framework — not a tool demo
4. Expand to full PMO org once the framework is stable and the feedback loop is established

---

## 08 — Key Proof Points Woven Through APEX

These metrics are embedded in the framework wherever they strengthen credibility. Use accurately and consistently.

- Program slippage: 22% to under 8% (signature proof point — appears in APEX landing page, README, and the risk skill file as the outcome benchmark)
- Portfolio managed: $65M+ across 12 enterprise clients
- Programs delivered: $4M–$10M cloud transformations for Fortune 500 insurance clients
- Public sector: $15M+ digital modernisation programs

---

## 09 — Decisions Log (Settled — No Revisiting Without Explicit Instruction)

| Decision | Choice made | Rationale |
|---|---|---|
| Project home | Stay in this Claude.ai Project | Context is here; a separate project would require full re-establishment |
| Chat discipline | One deliverable per chat | Prevents context degradation; project files carry state |
| Ecosystem name | APEX | Sits under AIDF; actionable and distinct |
| Brand relationship | APEX as AIDF execution layer | Maintains narrative continuity with existing assets |
| Phase 1 scope | Framework-only, no live integrations | External publish speed; integrations phased in |
| Skill file structure | Clean markdown first, YAML in Phase 2 | Keeps Phase 1 files human-readable and publishable |
| Primary user persona | Individual PM → Team lead → PMO-wide | Design for individual, architecture scales to PMO |
| External access model | Freemium (free framework, gated plugin) | Outreach first, monetise second |
| Consulting tier | Custom APEX deployment | Defensible paid product; not just content |
| Sapiens confidentiality | All internal context in private branch only | No client or employer data in public assets |
| Quality bar | Immediately usable output, not drafts | Differentiator vs prompt library |
| Governance block | Shared cross-skill block (03a): conflicting inputs, disclosure boundary, escalation autonomy, authorization precondition | Prevents drift across 8 skill files; single inherited contract for Layer 3/4 agents; generic now, sharpened per-program via APEX_CONTEXT.md later. Rule 4 (Authorization Precondition) promoted from a pm-release.md local mechanism after pm-governance.md scope review confirmed the Gate pattern is genuinely cross-skill, not release-specific. |

---

*This file is updated at the end of each APEX build session. The build log (APEX_BUILD_LOG.md) tracks execution state. Together they are the complete operating context for APEX.*
