# APEX — Build Log
*Tracks execution state across all build sessions*
*Owner: Projit Mookerjee | Repo: TBD (GitHub Pages, private until Phase 1 complete)*

---

## How to Use This File

Read this at the start of every APEX build session after reading APEX_MASTER.md. It tells you exactly what has been built, what instruction was used, where the output lives, and what the next task is. Update it at the end of every session before closing the chat.

**Standing principle:** governance rules, scoring logic, and design decisions in this build reflect best-current judgment, not a final specification. Once skills and agents are functional, Projit runs real program scenarios against them as user testing. Rules get refined or scaled based on what that testing surfaces, not by trying to pre-solve every edge case at design time. Ship the sharpest reasonable default, note where it might bend, move forward.

**Standing principle — industry-agnostic public skills, no client data in v1:** every public skill file under /apex/skills/ must be fully industry-agnostic in its core logic — no single vertical (insurance, Workers' Comp, etc.) load-bearing in role definition, scoring logic, anti-patterns, or quality bar. Worked examples use illustrative, swappable industry references only. No Sapiens, client (WCB), or named vendor (KPMG, Microsoft) content appears anywhere in the public file. All such content lives exclusively in a paired file under /apex/skills-internal/, named `pm-<domain>-sapiens-extension.md`, which references the public skill rather than duplicating its logic. The internal file is never merged into the public file and never published. See Repo Structure below for the directory convention.

**Status codes:**
- `DESIGNED` — drafted and approved in Claude.ai, not yet built in Claude Code
- `BUILT` — Claude Code instruction executed, file exists in repo
- `TESTED` — output validated against quality bar
- `PUBLISHED` — live on GitHub Pages or deployed internally
- `BLOCKED` — dependency not yet met (reason noted)

---

## Current State Snapshot

**Active phase:** Phase 1 — Foundation  
**Last session:** June 2026 — Full validation pass run against all 8 public skill files and all 8 Sapiens extensions, checked against APEX_MASTER.md Section 06 (Quality Standard), Section 08 (proof points), Section 03a (Governance Block), and the standing confidentiality rule. Three findings surfaced and all three corrected in this session; see Validation and Corrections Record below for full detail. Summary: (1) pm-planning.md had a full Sapiens-internal section embedded directly in the public file from an incomplete cleanup during its original industry-agnostic rework — content was already correctly present in pm-planning-sapiens-extension.md, so this was a deletion-only fix with no content loss. (2) pm-release.md had been logged in three places (APEX_MASTER.md Decisions Log, the Rule 4 build log entry, and pm-release.md's own build log entry) as refactored to inherit Gate properties from Governance Block Rule 4, but the actual file still defined the Gate mechanism standalone and never named Rule 4 — the refactor described in the log had not actually been performed on the file. Now corrected to match pm-governance.md's and pm-financials.md's inheritance pattern. (3) The 22%-to-under-8% proof point, which Section 08 names as belonging in pm-risk.md's public file, was absent from every public file and existed only in two extension files tied to "the CGI era" — added a generic, employer-unattributed version to pm-risk.md's Role Definition. All three fixes verified clean of confidential terms post-correction.  
**Next task:** With the validation pass and corrections complete, Phase 1's skill layer is genuinely closed, not just logged as closed. The next session is the same checkpoint described previously, now unblocked: (1) resolve the long-standing /apex/skills-internal/ private-branch-vs-gitignore question, now the single open item before repo work, (2) decide repo scaffold vs. apex.plugin build first, recommend scaffold first since the plugin's slash commands need real files to register against, (3) update the Claude Code scaffold instruction to reflect all eight corrected public skill files. No further file-content validation is needed before that session; this session's pass was the final check the standing sanity-check discipline was building toward.  
**Blocking items:** None. Phase 1 has no external dependencies. Note: eight extension files (reporting, risk, planning, release, governance, financials, resources, client) now exist as DRAFTED but are not yet committed to any repo path — /apex/skills-internal/ has not been scaffolded in Claude Code yet, and the private-branch-vs-gitignore question for that directory is unresolved. This is now the single largest open item blocking a clean Phase 1 close and should be resolved in the next Claude Code session rather than deferred further.

---

## Validation and Corrections Record

**Session:** June 2026, following completion of pm-client.md (full Phase 1 skill set).

**Scope of validation:** all 8 public skill files and all 8 Sapiens extension files, checked against APEX_MASTER.md Section 06 (Quality Standard), Section 08 (Key Proof Points), Section 03a (Governance Block), and the standing confidentiality rule (industry-agnostic public layer, zero Sapiens/client/vendor content in public files).

**Finding 1 — Confidentiality violation, corrected.** pm-planning.md contained a full "Sapiens Extension (Internal Only)" section (Coresuite phasing, Digital Suite sequencing, KPMG/Microsoft/WCB vendor ownership, multi-geography capacity planning) embedded directly in the public file, roughly 19 lines, with a header stating it must never appear in the published version while sitting inside the file that gets published. This was leftover content from the original industry-agnostic rework session: the content had already been correctly copied into pm-planning-sapiens-extension.md, confirmed via diff to be present and intact there, so the fix was a clean deletion from the public file with zero content loss. This was the only one of the eight public files with an embedded internal-only section; all eight were checked for this pattern specifically.

**Finding 2 — Logged state did not match actual file content, corrected.** pm-release.md was logged in three separate places (APEX_MASTER.md's Decisions Log, the Governance Block Rule 4 build log entry, and pm-release.md's own build log entry) as having been refactored to inherit the Gate mechanism's general properties from Rule 4. The actual file had not been refactored: it still defined the Gate mechanism as a standalone concept ("this skill calls this a Gate") and related it only to Rule 3, never naming Rule 4 anywhere in the file. pm-release.md's Role Definition paragraph and Compliance and Audit Gates section have been rewritten to match the inheritance pattern already correctly used in pm-governance.md and pm-financials.md: general Gate properties inherited from Rule 4 and not restated, only release-domain Gate instances (Compliance, Audit, Contractual, Security) and release-domain output conventions stated locally. The Rule 3-versus-Gate distinction, which was already correctly stated, is preserved and now correctly cross-referenced against Rule 4 rather than standing alone. Anti-pattern entries updated to match.

**Finding 3 — Missed deliverable against Section 08, corrected.** The signature proof point (program slippage reduced from over 20% to under 8%) did not appear in any of the 8 public skill files. Section 08 names pm-risk.md's public file as its intended home, as a generic, industry-agnostic credibility anchor with no employer attribution. The proof point existed only in two extension files (pm-risk-sapiens-extension.md, pm-reporting-sapiens-extension.md), both explicitly tied to "the CGI era," which is correct for the internal-only files but left the public layer without the proof point Section 08 calls for. Added a generic, employer-unattributed version to pm-risk.md's Role Definition section: the mechanism (disciplined risk identification with assignable, tracked mitigation) is stated as what drives the outcome, with no reference to any employer, client, or named program.

**Verification performed on all three fixes:** each corrected file re-checked for the eight confidentiality terms (Sapiens, WCB, Saskatchewan, KPMG, Microsoft, Coresuite, Digital Suite, Azure) plus "CGI" — zero matches in all three corrected public files post-fix. pm-release.md's Rule reference counts re-tallied post-fix (Rule 4 now appears 7 times, matching the density already present in pm-governance.md and pm-financials.md for their respective Gate sections; previously zero).

**Not found:** no other public file had an embedded internal-only section. No other skill file had a logged-versus-actual mismatch of this kind (spot-checked pm-governance.md and pm-financials.md's Rule 4 claims against their actual text; both correct as logged). No other proof point from Section 08 was checked for public-layer presence this session (portfolio managed, programs delivered, public sector figures) since those are tied to the landing page and README, neither yet built; revisit when those are drafted.

---

## Phase 1 — Foundation

### Repo Structure
**Status:** BUILT (partial, verified) — /apex/skills/ confirmed in repo with all 8 expected filenames present. /agents/, /context/, /plugin/, /examples/, README.md, and index.html not yet verified — confirm in next Claude Code session before marking this fully BUILT. /skills-internal/ added to target structure this session (not yet scaffolded in repo — see updated Claude Code instruction below).  
**Target structure:**
```
/apex/
  /skills/
    pm-planning.md
    pm-risk.md
    pm-reporting.md
    pm-release.md
    pm-resources.md
    pm-financials.md
    pm-client.md
    pm-governance.md
  /skills-internal/                 [private branch only — never published]
    pm-planning-sapiens-extension.md
    pm-risk-sapiens-extension.md
    pm-reporting-sapiens-extension.md
    pm-release-sapiens-extension.md
    pm-resources-sapiens-extension.md
    pm-financials-sapiens-extension.md
    pm-client-sapiens-extension.md
    pm-governance-sapiens-extension.md
  /agents/
    program-intelligence-agent.md   [Phase 2]
    raid-agent.md                   [Phase 2]
    release-readiness-agent.md      [Phase 2]
  /context/
    APEX_CONTEXT.md                 [Phase 1 — template]
    APEX_CONTEXT_WCB.md             [Phase 3 — internal only, private branch]
  /plugin/
    apex.plugin                     [Phase 1]
  /examples/
    [worked examples per skill]     [Phase 1–2]
README.md                           [Phase 1]
index.html                          [Phase 1 — landing page]
```

**Naming convention:** every internal extension file is named `pm-<domain>-sapiens-extension.md`, matching its public counterpart's domain name exactly (e.g. `pm-release.md` pairs with `pm-release-sapiens-extension.md`). This is a fixed convention, not per-file judgment.

**Directory handling:** `/apex/skills-internal/` is never present in the public repo or public GitHub Pages build. It exists only on a private branch (same handling as APEX_CONTEXT_WCB.md, Phase 3). Until the private branch exists, internal extension files are held in Claude.ai project files / outputs and tracked in this log as DRAFTED, not committed to the public repo under any path.

**Claude Code instruction to run (when ready):**
```
Create the following directory structure and placeholder files. 
Do not add content yet — just the structure with a one-line comment in each file.

mkdir -p apex/skills apex/skills-internal apex/agents apex/context apex/plugin apex/examples

touch apex/skills/pm-planning.md
touch apex/skills/pm-risk.md
touch apex/skills/pm-reporting.md
touch apex/skills/pm-release.md
touch apex/skills/pm-resources.md
touch apex/skills/pm-financials.md
touch apex/skills/pm-client.md
touch apex/skills/pm-governance.md
touch apex/skills-internal/.gitkeep
touch apex/agents/.gitkeep
touch apex/context/APEX_CONTEXT.md
touch apex/plugin/apex.plugin
touch README.md
touch index.html

Confirm the structure with a tree output.

Note: apex/skills-internal/ must be added to .gitignore in the public 
repo, or scaffolded only on a private branch — confirm which approach 
before committing.
```

---

### Skill Files

**Build order (priority sequence):**
1. pm-reporting.md — highest-value first demonstrator; directly feeds Sapiens PMO pilot — BUILT
2. pm-risk.md — connects to 22-to-8% proof point; strongest external hook — BUILT
3. pm-planning.md — foundational; required by most other skills — BUILT
4. pm-release.md — WCB variant needed for Phase 3 internal deployment — BUILT
5. pm-governance.md — WCB variant needed for Phase 3 internal deployment — BUILT
6. pm-financials.md — BUILT
7. pm-resources.md — BUILT
8. pm-client.md — BUILT

All eight Phase 1 skill files are now BUILT. Phase 1 skill layer complete.

---

#### pm-reporting.md
**Status:** BUILT — drafted, hardened, reworked to industry-agnostic, confirmed in repo at /apex/skills/pm-reporting.md  
**Session built:** June 2026  
**Key outputs this skill produces:** RAG status report, executive narrative, weekly steering brief, sprint-to-board translation, multi-workstream steering pack, escalation check  
**Proof point embedded:** 22% to under 8% program slippage, framed as the outcome of standardized milestone visibility — proof point itself is generic in the public file; the CGI-era / Sapiens-piloting connection lives in the paired extension file  
**Sapiens extension:** Split out this session into a separate paired file — DRAFTED — pm-reporting-sapiens-extension.md (WCB steering committee format, Coresuite/Digital Suite milestone phase-gate framing, KPMG/Microsoft/WCB internal IT dependency separation, multi-geography delivery notes). Not yet committed to /apex/skills-internal/ pending private branch setup.  
**Governance Block applied:** References APEX_MASTER.md Section 03a throughout rather than restating logic — conflicting input resolution (system data vs. qualitative signal), disclosure boundary (audience tone vs. mandatory disclosure), escalation autonomy (critical-path sign-off gate)  
**Notes:** Output is built to paste into a steering deck without edits. Includes a default RAG roll-up rule (critical-path-weighted) for multi-workstream consolidation, overridable per program via APEX_CONTEXT.md. Worked example confirmed already industry-agnostic, no rework needed there.

---

#### Governance Block (APEX_MASTER.md, Section 03a)
**Status:** BUILT — added to APEX_MASTER.md, verified single occurrence after a duplication artifact was caught and corrected  
**Session built:** June 2026, during pm-reporting.md hardening pass  
**What it is:** Cross-skill rule set inherited by all eight skill files rather than restated in each: (1) Conflicting Input Resolution, (2) Disclosure Boundary, (3) Escalation Autonomy. Generic by design, with each rule carrying a stated default and an override path through APEX_CONTEXT.md for industry/program-specific sharpening.  
**Why it exists:** Reporting, risk, financials, client, and governance skills all hit the same three decision points. Defining once prevents drift across files and gives Layer 3/4 agents a single inherited contract instead of eight slightly different ones.  
**Notes:** Rule 3 (Escalation Autonomy) carries an explicit inheritance note: when invoked by a human, these are prompt instructions; when invoked by a Domain Agent or the Delivery Command Agent in Layer 3/4, Rule 3 must be implemented as a hard stop, not a soft suggestion. This is binding on agent design, not just skill-file wording.

---

#### pm-risk.md
**Status:** BUILT — drafted, then reworked to industry-agnostic, confirmed ready for /apex/skills/pm-risk.md. Correction applied this session — see Validation and Corrections Record above.  
**Session built:** June 2026 (proof point correction applied in the validation session, several sessions later)  
**Key outputs this skill produces:** RAID log, pre-mortem risk list, mitigation plan, risk narrative for exec reporting  
**Proof point embedded:** Generic, employer-unattributed version (program slippage from over 20% to under 8%) now present in the Role Definition, correcting a gap caught by validation — the public file previously had no proof point at all despite Section 08 naming pm-risk.md as its intended home; only the two CGI-attributed extension files had it. Fixed by adding a mechanism-focused statement with zero employer or client attribution.  
**Sapiens extension:** Split out this session into a separate paired file — DRAFTED — pm-risk-sapiens-extension.md (WCB risk register structure with three-vendor dependency-line separation, Azure AI model-behavior risk sub-category, phase-gate pre-mortem cadence). Not yet committed to /apex/skills-internal/ pending private branch setup.  
**Design question resolved:** Risk severity scoring (probability × impact matrix) is domain-specific logic, separate from Governance Block Rule 1. Rule 1 governs the inputs feeding the score, not the scoring mechanism itself — if a stated mitigant or PM's qualitative call disagrees with observed reality before scoring, Rule 1 resolves that disagreement first, and the resolved (more cautious) input is what gets scored. This scope note was added to APEX_MASTER.md Section 03a, Rule 1.  
**Notes:** The pre-mortem prompt from the AI PM Guide is the starting reference. APEX version goes deeper. Worked example reworked this session from a Workers' Comp insurer scenario to an illustrative, industry-swappable enterprise migration scenario.

---

#### pm-planning.md
**Status:** BUILT — drafted, then reworked to industry-agnostic, confirmed ready for /apex/skills/pm-planning.md. Correction applied this session — see Validation and Corrections Record above.  
**Session built:** June 2026 (confidentiality fix applied in the validation session, several sessions later)  
**Key outputs this skill produces:** WBS, dependency map, sprint decomposition, PI Planning prep, effort estimates  
**Confidentiality correction:** Validation caught a full "Sapiens Extension (Internal Only)" section (roughly 19 lines: Coresuite phasing, Digital Suite sequencing, KPMG/Microsoft/WCB vendor ownership, multi-geography capacity planning) still embedded in the public file from the original rework session — content was correctly present in the paired extension file but had never been deleted from the public source. Removed. Zero content loss; the extension file already had the clean, correctly-attributed version.  
**Sapiens extension:** Split out this session into a separate paired file — DRAFTED — pm-planning-sapiens-extension.md (Coresuite phase-gate vs. Agile nesting, Digital Suite sequencing dependency on Coresuite stability, three-vendor dependency ownership, multi-geography capacity planning). Not yet committed to /apex/skills-internal/ pending private branch setup.  
**Notes:** Builds on WBS examples in the AI PM Guide but scoped for large enterprise programs, not generic projects. Worked example reworked this session from a SaaS insurance claims-processing scenario to an illustrative, industry-swappable enterprise migration scenario.

---

#### pm-release.md
**Status:** BUILT — drafted in prior session. The Rule 4 inheritance refactor logged several sessions ago as having been completed had not actually been applied to the file; corrected for real in this validation session — see Validation and Corrections Record above. Ready for /apex/skills/pm-release.md.  
**Session built:** June 2026 (drafted prior session; Rule 4 refactor logged but not executed two sessions ago; actually executed in this validation session)  
**Key outputs this skill produces:** Go/no-go checklist, UAT plan, cutover runbook, release readiness brief, readiness gap audit  
**Proof point embedded:** Implicitly via the severity-weighted go/no-go framing (the readiness discipline that supports the proof point now stated directly in pm-risk.md). The proof point itself is not restated in this public file.  
**Sapiens extension:** DRAFTED — pm-release-sapiens-extension.md (WCB compliance gates, Coresuite/Digital Suite cutover sequencing, three-vendor sign-off tracking, stricter rollback procedure standard for regulated cutover steps). Not yet committed to /apex/skills-internal/ pending private branch setup.  
**Governance Block applied:** References APEX_MASTER.md Section 03a throughout rather than restating logic. Rule 4 (Authorization Precondition) inheritance is now actually implemented in the file as of this session — the Role Definition names Rule 4 as the dominant rule, and the Compliance and Audit Gates section inherits the Gate mechanism's general properties from Rule 4 and only states release-domain instances (Compliance, Audit, Contractual, Security Gate categories) and release-domain output conventions, matching the pattern already correct in pm-governance.md and pm-financials.md. Anti-pattern entries updated to attribute Gate-flagging to Rule 4 and escalation-on-bypass to Rule 3, rather than leaving Rule 4 unnamed throughout.  
**Design question resolved this session (Framing C):** The Gate mechanism originally defined locally in pm-release.md was confirmed cross-skill after pm-governance.md scope review surfaced portfolio stage gates, Charter Gate, Baseline Change Gate, Scope-Change Gate, Closure Gate, and CoE Exception Gate as structurally identical instances. Promoted to Governance Block Rule 4. pm-release.md refactored to inherit — this refactor was logged as complete at the time but the actual file edit was missed; both the original promotion decision and the file-level correction are recorded here for a complete history. See "Governance Block Rule 4 — Authorization Precondition" entry below for the promotion record.  
**Notes:** Output is built to support a go/no-go meeting without re-derivation. Severity-weighted recommendation (not completion-percentage) is the central discipline. Worked example confirmed already industry-agnostic in the prior session.

---

#### pm-governance.md
**Status:** BUILT — drafted this session, industry-agnostic from the start, confirmed ready for /apex/skills/pm-governance.md  
**Session built:** June 2026  
**Key outputs this skill produces:** Portfolio KPI dashboard, CoE framework, governance pack for an authorization event, PMO reporting standards, portfolio reporting narrative  
**Sapiens extension:** DRAFTED — pm-governance-sapiens-extension.md (WCB Saskatchewan governance structure resolution into three named bodies, Coresuite/Digital Suite phase-gate overlay, three-vendor governance lines, multi-geography reporting cadence, Sapiens CoE and internal standards overlay, Azure AI workstream governance tier). Not yet committed to /apex/skills-internal/ pending private branch setup.  
**Governance Block applied:** References APEX_MASTER.md Section 03a throughout. Rule 4 (Authorization Precondition) is the most active rule in this skill — the Portfolio Gates and Authorization Artifacts section names six governance-domain Gate instances (Phase-Gate, Charter Gate, Baseline Change Gate, Scope-Change Gate, Closure Gate, CoE Exception Gate) as domain-local applications of the general Rule 4 pattern. Rule 1 (Conflicting Input Resolution) is the second most active rule: system KPI values cannot silently override qualitative portfolio signals.  
**Design discipline embedded:** Every metric in the dashboard either has a threshold triggering a defined intervention or a documented decision it informs. Metrics meeting neither criterion are out of scope for the dashboard. Every governance pack names the decision being requested in one sentence, names the authorizer, states the Gate status, and states the recommendation with the deciding factor first.  
**Notes:** Worked example uses an illustrative Customer platform modernization scenario with explicit "applies equally to insurance, financial services, healthcare, retail, or public sector contexts" framing, consistent with the worked-example style established in pm-risk.md and pm-planning.md after their industry-agnostic rework. Output is built to support a portfolio review meeting without re-derivation of what is being authorized.

---

#### Governance Block Rule 4 — Authorization Precondition (added to APEX_MASTER.md, Section 03a)
**Status:** BUILT — added to APEX_MASTER.md, Decisions Log entry refreshed to reflect four rules, Inheritance note for Layer 3/4 extended to make Rule 4 a hard stop alongside Rule 3  
**Session built:** June 2026  
**What it is:** Fourth cross-skill rule in the Governance Block. Defines the general properties of a Gate (binary authorization precondition, named authorizer, recorded artifact, blocking by default, flagged when unconfirmed) as a shared mechanism rather than re-stating it per skill.  
**Why it was promoted:** Originally articulated as a release-domain mechanism in pm-release.md's prior-session draft. Provisional recommendation (Framing C) was to promote if pm-governance.md surfaced a structurally identical pattern. This session confirmed: pm-governance.md contains six Gate instances (Phase-Gate, Charter Gate, Baseline Change Gate, Scope-Change Gate, Closure Gate, CoE Exception Gate), all matching the Gate properties exactly. Two domains with five-plus instances and a near-certain third (pm-financials.md commitment-threshold gates, baseline change authorization, EAC variance gates) justified promotion over per-skill restatement. Standing principle applied: ship the sharpest reasonable default, note where it might bend.  
**Cascading changes made this session:** pm-release.md Compliance and Audit Gates section refactored from standalone definition to Rule 4 inheritance plus release-domain instances. pm-release.md Role Definition paragraph updated to reference Rule 4 explicitly. pm-governance.md drafted with Rule 4 inheritance already in place. APEX_MASTER.md Section 03a Inheritance note extended to cover Rule 4 (Layer 3/4 agents implement as a hard stop, not a prompt suggestion). Decisions Log entry refreshed.  
**Where Rule 4 might bend:** if pm-financials.md surfaces a Gate-shaped mechanism with materially different mechanics (e.g., a quantitative threshold rather than a named-authorizer artifact), the rule may need a scope note distinguishing authorization Gates from threshold-trigger Gates. Watch-item for the next session.  
**Notes:** Rule 4 wording deliberately mirrors Rules 1–3 in structure: general statement, default reasoning, scope note distinguishing the general pattern from domain-specific instances, relationship note with adjacent rules (Rule 3). Industry-agnostic — examples reference categories (compliance, audit, contractual, security; phase, charter, baseline, scope, closure) not verticals.

---

#### pm-financials.md
**Status:** BUILT — drafted, industry-agnostic from the start, confirmed ready for /apex/skills/pm-financials.md. Backfilled into this log — see Process Gap note below.  
**Session built:** June 2026 (prior session; build log entry was not written at the time)  
**Key outputs this skill produces:** EAC/ETC model, budget variance narrative, monthly cost report, billable vs non-billable breakdown, forecast commitment pack  
**Sapiens extension:** DRAFTED — pm-financials-sapiens-extension.md. Not yet committed to /apex/skills-internal/ pending private branch setup.  
**Governance Block applied:** References APEX_MASTER.md Section 03a throughout. Rule 4 (Authorization Precondition) is heavily active — Budget Approval Gate, Re-Baseline Gate, and Commitment Threshold Gate are defined as financial-domain Gate instances. The watch-item carried from the pm-governance.md session (whether quantitatively-triggered Gates, e.g. an EAC variance crossing a re-baseline threshold, are a domain-local Rule 4 application or a materially different mechanism) resolved cleanly: they are domain-local. The skill explicitly distinguishes the Rule 2 materiality threshold (triggers mandatory disclosure) from the Rule 4 Gate trigger threshold (triggers a blocking authorization requirement) as two separate mechanisms that must not be conflated, rather than proposing a new rule. Rule 1 (Conflicting Input Resolution) governs reconciliation of ledger value, PM-stated forecast, and observed burn rate when they disagree. Rule 3 (Escalation Autonomy) governs surfacing a deteriorating EAC to the authorizer.  
**Process gap:** This skill file and its extension were drafted in the session immediately following pm-governance.md, but that session's build log update was never made — the Current State Snapshot and skill file entry continued to show pm-financials.md as NOT STARTED for one full additional session (the session that produced pm-resources.md) before this gap was caught during that session's start-of-session sanity check. Backfilled in this update. Same failure pattern as the earlier pm-release.md backfill; both gaps were caught by the standing start-of-session sanity check rather than by a process change, since the discipline of updating the log at session close is the actual fix and was simply skipped in both cases.  
**Notes:** Monthly report generation is a key use case. Output is built to be Excel-ready in structure and exec-ready in narrative simultaneously. Worked example uses an illustrative enterprise transformation program scenario, consistent with the industry-agnostic worked-example style established across the other five skill files.

---

#### pm-resources.md
**Status:** BUILT — drafted this session, industry-agnostic from the start, confirmed ready for /apex/skills/pm-resources.md  
**Session built:** June 2026  
**Key outputs this skill produces:** Resource conflict map, allocation plan, capacity model, cross-program dependency flag, resource risk narrative  
**Sapiens extension:** DRAFTED — pm-resources-sapiens-extension.md (India/EU/North America multi-geography resource pool, three-vendor resource pool separation, the program-specific two-signal vs. three-signal capacity pattern for vendor-supplied resourcing, Azure AI workstream resourcing as a non-fungible pool). Not yet committed to /apex/skills-internal/ pending private branch setup.  
**Governance Block applied:** References APEX_MASTER.md Section 03a throughout. Rule 1 (Conflicting Input Resolution) is the dominant rule in this skill — the carried-forward watch-item from the pm-financials.md session (system-reported allocation vs. vendor-stated availability vs. observed delivery throughput) is resolved in full in the new Capacity Signal Conflicts section, in the same shape as pm-risk.md's Rule 1 scope note treatment of severity scoring: a domain-local explanation of how three commonly-disagreeing signals resolve under the existing rule, not a new mechanism. Rule 3 (Escalation Autonomy) governs cross-program conflicts this program does not have unilateral authority to resolve. Rule 2 (Disclosure Boundary) applies when a resourcing gap is material to a committed deliverable. Rule 4 (Authorization Precondition) is addressed narrowly and deliberately bounded away from the Rule 1 signal-conflict pattern, since the two are easy to conflate in this domain — the public skill states the distinguishing test directly (is a named authorizer's sign-off missing, or do the inputs simply disagree about a fact) rather than letting the boundary stay implicit.  
**Design question resolved this session:** Confirmed that the three-way capacity signal conflict is a Rule 1 question, not a Rule 4 question, and that resource management does contain a small number of genuine Rule 4 Gate instances (e.g. formal resource release between programs pending named sponsor sign-off) that are structurally distinct from the signal-conflict pattern. No new Governance Block rule or scope note required at the APEX_MASTER.md level; the explanation lives entirely in the skill file, consistent with how Rule 1's pm-risk.md scope note was also kept domain-local rather than promoted into Section 03a.  
**Notes:** Worked example uses an illustrative enterprise platform migration scenario with explicit "applies equally to insurance, financial services, healthcare, retail, or public sector contexts" framing, consistent with the worked-example style established across the other six skill files. Output is built to support a sprint planning or resourcing review meeting without re-derivation of who is actually double-booked.

---

#### pm-client.md
**Status:** BUILT — drafted this session, industry-agnostic from the start, confirmed ready for /apex/skills/pm-client.md. Completes the full Phase 1 skill set (8 of 8 public skills, 8 of 8 Sapiens extensions, all DRAFTED or BUILT, none yet committed to a repo path).  
**Session built:** June 2026  
**Key outputs this skill produces:** Client governance pack, escalation framework, stakeholder communication plan, executive briefing, tactical message draft  
**Sapiens extension:** DRAFTED — pm-client-sapiens-extension.md (WCB three-body governance structure mapped as the client-side stakeholder map, parallel client-side and internal-side escalation tier structures, three-vendor communication boundary distinguishing client-visible commitment facts from internal vendor-management detail, Azure AI workstream disclosure treatment, multi-geography tactical communication consideration). Not yet committed to /apex/skills-internal/ pending private branch setup.  
**Governance Block applied:** References APEX_MASTER.md Section 03a throughout. Rule 2 (Disclosure Boundary) and Rule 3 (Escalation Autonomy) are the two dominant rules, as anticipated in the prior session's pointer. Rule 1 (Conflicting Input Resolution) applies to relationship-signal-versus-delivery-data conflicts (a client's stated satisfaction lagging current delivery status). Rule 4 is not materially active in this domain; no Gate-shaped mechanism was identified as central to client management the way it is in release, governance, and financials.  
**Design question resolved this session:** Rule 2 required no new mechanism, the skill's audience and stakeholder calibration section is additive guidance on top of the existing disclosure floor, consistent with how pm-reporting.md already treats Rule 2. Rule 3 required an explicit domain-local clarification: this skill's own "escalation framework" output and Governance Block Rule 3 ("Escalation Autonomy") share vocabulary but answer different questions, and the skill states the distinction directly in a dedicated Escalation Framework Mechanics section, in the same pattern as pm-release.md's Gate-versus-Rule-3 distinction. No promotion to Section 03a was needed; this stayed domain-local, consistent with how pm-risk.md's and pm-resources.md's Rule 1 scope notes also stayed domain-local rather than being promoted.  
**Design decision specific to this skill:** Introduced a dual-altitude framing (seasoned delivery leader / structural outputs versus day-to-day PM or delivery manager / tactical outputs) not present in the other seven skill files, per explicit session instruction. The Role Definition states how the skill identifies which altitude a given request is operating at and asks rather than guessing when ambiguous. This is a skill-specific design pattern, not a Governance Block change, and does not need to be retrofitted into the other seven skills unless a similar dual-audience need surfaces there during user testing.  
**Notes:** Worked example uses an illustrative enterprise platform program scenario with explicit "applies equally to insurance, financial services, healthcare, retail, or public sector contexts" framing, consistent with the worked-example style established across the other seven skill files. Worked example operates at the delivery-leader altitude (stakeholder communication plan); Template 5 (Tactical Message Draft) covers the day-to-day altitude but was not separately worked through a full example in this session, consistent with how other skills' templates are not all individually worked. Output is built to support a client conversation, steering meeting, or internal briefing without re-derivation of who should hear what, in what order.

---

### APEX_CONTEXT.md Template
**Status:** NOT STARTED  
**Session to build:** Same chat as repo scaffold (Chat 1 in Claude Code)  
**Key fields to include:**
- Program name and type (dropdown: enterprise transformation / SaaS migration / public sector / regulated industry)
- Client governance model (exec sponsor, steering committee, PMO structure)
- Active tooling stack (Jira yes/no, M365 yes/no, ServiceNow yes/no, Salesforce yes/no)
- Team structure (total FTEs, vendor count, geographies)
- Active milestones with target dates
- Known risks and constraints
- Compliance environment (regulated / non-regulated)
- Reporting cadence (weekly / fortnightly / monthly)
- Program-specific terminology glossary (free text)

---

### apex.plugin
**Status:** UNBLOCKED — all 8 skill files now BUILT (DRAFTED/ready, not yet committed to repo). Dependency satisfied as of this session's pm-client.md completion. Not yet started; sequencing question (scaffold repo first vs. build plugin first) is the next session's checkpoint decision.  
**Dependency:** All pm-*.md files built — SATISFIED  
**Slash commands to register:**
- /status-report → invokes pm-reporting.md
- /raid-extract → invokes pm-risk.md
- /risk-premortem → invokes pm-risk.md (pre-mortem variant)
- /go-no-go → invokes pm-release.md
- /resource-conflict → invokes pm-resources.md
- /financial-variance → invokes pm-financials.md
- /release-readiness → invokes pm-release.md
- /meeting-intel → invokes pm-governance.md + pm-risk.md in sequence

---

### README.md
**Status:** NOT STARTED  
**Session to build:** Can be drafted in Claude.ai alongside skill files; Claude Code writes it to disk at Phase 1 close  
**Content to cover:** What APEX is, how it fits in the AIDF ecosystem, how to use it, the three access tiers, link to landing page, link to PM Guide and Prompt Kit

---

### index.html (Landing Page)
**Status:** NOT STARTED  
**Session to build:** Dedicated Claude Code session after README is finalised  
**Design system:** Must match portfolio site exactly — Fraunces + Epilogue + JetBrains Mono, ink/paper/cream/accent palette  
**Key sections:**
- Hero: APEX name, positioning statement, relationship to AIDF
- What it is: the four-layer architecture
- What you get: skill domains with output descriptions
- How to access: three tiers (free / practitioner / consulting)
- CTA: email capture for practitioner tier, link to Claude Code plugin
- Footer: matches portfolio site format, links back to PM Guide and Prompt Kit

---

## Phase 2 — Domain Agents

### Program Intelligence Agent
**Status:** NOT STARTED — blocked on pm-reporting.md and pm-risk.md  
**Input schema:** Program context + Jira sprint data or free-text weekly update  
**Output schema:** JSON with fields: rag_status (R/A/G per workstream), top_risks (array, max 3), escalation_flag (bool + description), recommended_action (string), narrative_brief (string, 150 words max)  
**Test case to build:** WCB Saskatchewan weekly brief (internal only)

---

### RAID Agent
**Status:** NOT STARTED — blocked on pm-risk.md  
**Input schema:** Unstructured text (meeting transcript, email thread, notes)  
**Output schema:** JSON with RAID entries, each containing: id, category (R/A/I/D), description, owner, impact (H/M/L), due_date, status  
**Test case to build:** Sample steering committee transcript → RAID log

---

### Release Readiness Agent
**Status:** NOT STARTED — blocked on pm-release.md  
**Input schema:** Release definition (scope, team, environment, target date, release type)  
**Output schema:** JSON checklist with items grouped by category, each containing: item, owner_role, verification_method, hard_stop (bool)  
**Test case to build:** SaaS platform go-live in regulated (insurance) environment

---

## Phase 3 — Orchestration + Sapiens Internal

*All Phase 3 items blocked until Sapiens Claude Enterprise license is active and Phase 2 is complete.*

### Delivery Command Agent
**Status:** BLOCKED — Phase 2 dependency  
**Design session:** Not yet scheduled

### Jira MCP Integration
**Status:** BLOCKED — Phase 3

### M365 MCP Integration
**Status:** BLOCKED — Phase 3

### ServiceNow API Integration
**Status:** BLOCKED — Phase 3

### Cowork Plugin Configuration
**Status:** BLOCKED — Phase 3

### WCB Context File (APEX_CONTEXT_WCB.md)
**Status:** BLOCKED — Sapiens license + Phase 2 complete  
**Location:** Private repo branch only. Never in public repo.

---

## Phase 4 — External Product

*Planning only. Execution begins when Phase 1 is published.*

### LinkedIn Launch Sequence (APEX)
**Status:** NOT STARTED  
**Post count:** 6-post sequence  
**Framing:** APEX as the execution layer of AIDF — not a standalone announcement  
**Draft session:** Schedule after Phase 1 landing page is live

### Email Capture Gate (Practitioner Tier)
**Status:** NOT STARTED  
**Mechanism:** TBD — GitHub form, Substack, or simple email link  
**Trigger:** Phase 1 complete

### Consulting Engagement Tier
**Status:** NOT STARTED  
**Trigger:** Phase 2 agents demonstrably working; at least one external pilot user

---

## Session Log

| Date | Chat topic | Outputs produced | Build log updated |
|---|---|---|---|
| June 2026 | Architecture, planning, tool roles, brand decisions | APEX_MASTER.md, APEX_BUILD_LOG.md | Yes |
| June 2026 | pm-reporting.md draft, multi-stakeholder hardening pass, Governance Block (03a) added to APEX_MASTER.md, duplication bug found and fixed during repo verification | APEX_MASTER.md (updated), pm-reporting.md (built), APEX_BUILD_LOG.md (this update) | Yes |
| June 2026 | pm-risk.md and pm-planning.md drafted and built. Standing rule established: public skills industry-agnostic, zero client/vendor data in v1, Sapiens content split into paired extension files. pm-reporting.md, pm-risk.md, pm-planning.md reworked under this rule; three extension files drafted. Repo structure and Claude Code scaffold instruction updated with /apex/skills-internal/ and naming convention. | pm-risk.md (built), pm-planning.md (built), pm-reporting.md (reworked), pm-reporting-sapiens-extension.md (drafted), pm-risk-sapiens-extension.md (drafted), pm-planning-sapiens-extension.md (drafted), APEX_BUILD_LOG.md (this update) | Yes |
| June 2026 | pm-release.md and pm-release-sapiens-extension.md drafted. Compliance and audit gate concept introduced as a release-domain mechanism. Framing C surfaced as a watch-item: whether the Gate mechanism should be promoted to a fourth Governance Block rule, deferred to pm-governance.md scope review for confirmation. | pm-release.md (drafted), pm-release-sapiens-extension.md (drafted). Note: build log entry for this session was not written at the time and is backfilled in the current session's update. | Backfilled in next session |
| June 2026 | pm-governance.md and pm-governance-sapiens-extension.md drafted. Framing C resolved this session: Gate mechanism promoted to Governance Block Rule 4 — Authorization Precondition. APEX_MASTER.md Section 03a updated with Rule 4 wording, Inheritance note extended to cover Rule 4 as a Layer 3/4 hard stop, Decisions Log refreshed. pm-release.md Compliance and Audit Gates section refactored to inherit from Rule 4. pm-governance.md drafted with Rule 4 inheritance already in place. Missing pm-release.md build log entry backfilled. | APEX_MASTER.md (updated — Rule 4 added, Inheritance note extended, Decisions Log refreshed), pm-release.md (refactored), pm-governance.md (built), pm-governance-sapiens-extension.md (drafted), APEX_BUILD_LOG.md (this update — backfill plus current session) | Yes |
| June 2026 | pm-financials.md and pm-financials-sapiens-extension.md drafted, industry-agnostic from the start. Watch-item from prior session resolved: quantitatively-triggered Gates (Re-Baseline Gate, Commitment Threshold Gate) confirmed as domain-local Rule 4 applications, distinguished explicitly from the Rule 2 materiality-disclosure threshold rather than treated as the same mechanism. Build log update was not performed at session close. | pm-financials.md (drafted), pm-financials-sapiens-extension.md (drafted). Note: build log entry for this session was not written at the time and is backfilled in a later session's update. | Backfilled two sessions later |
| June 2026 | Start-of-session sanity check caught the missed pm-financials.md build log update from the prior session; backfilled here. pm-resources.md and pm-resources-sapiens-extension.md drafted, industry-agnostic from the start. Carried-forward Rule 1 watch-item (system allocation vs. vendor availability vs. observed throughput) resolved as a domain-local explanation in pm-resources.md's new Capacity Signal Conflicts section, same shape as pm-risk.md's Rule 1 scope note. Explicit boundary drawn between this Rule 1 pattern and genuine Rule 4 resource-release Gates, to prevent the two being conflated in future sessions. No new Governance Block rule required. | pm-financials.md build log entry (backfilled), pm-resources.md (built), pm-resources-sapiens-extension.md (drafted), APEX_BUILD_LOG.md (this update) | Yes |
| June 2026 | pm-client.md and pm-client-sapiens-extension.md drafted, industry-agnostic from the start. Completes the full Phase 1 skill set (8 of 8). Dual-altitude design introduced (delivery-leader structural needs vs. day-to-day PM/DM tactical needs) per explicit session instruction, skill-specific pattern not retrofitted into other skills. Carried-forward open question on Rule 2/Rule 3 resolved: Rule 2 needed no new mechanism; Rule 3 needed a domain-local Escalation Framework Mechanics section distinguishing the skill's own escalation-framework output from Rule 3's autonomy restriction, same pattern as pm-release.md's Gate distinction. apex.plugin status updated from BLOCKED to UNBLOCKED now that its dependency is satisfied. | pm-client.md (built), pm-client-sapiens-extension.md (drafted), APEX_BUILD_LOG.md (this update, including apex.plugin status update) | Yes |
| June 2026 | Full validation pass run across all 8 public skill files and 8 extensions against Section 06, Section 08, Section 03a, and the confidentiality rule, per explicit request. Three findings, all corrected in the same session: pm-planning.md had a leftover Sapiens-internal section embedded in the public file (deleted, no content loss); pm-release.md had been logged as Rule-4-refactored three separate times without the refactor actually being applied to the file (now actually applied, matching pm-governance.md and pm-financials.md's pattern); pm-risk.md was missing the public-layer proof point Section 08 calls for (added, generic and employer-unattributed). All three files re-verified clean of confidential terms post-fix. | pm-planning.md (corrected), pm-release.md (corrected), pm-risk.md (corrected), APEX_BUILD_LOG.md (this update — new Validation and Corrections Record section added, three skill entries updated) | Yes |

*Add a row at the end of every session.*

---

## How to Start the Next Chat

Copy and paste this block at the start of your next APEX build session:

```
Read APEX_MASTER.md and APEX_BUILD_LOG.md from the project files. 

Current task: [INSERT TASK — e.g., "Draft pm-reporting.md skill file"]

Do not re-establish architecture, naming, or decisions already logged in APEX_MASTER.md. 
Treat everything in the Decisions Log as settled. 
Start from the current state shown in the build log.
```

Replace [INSERT TASK] with the specific deliverable for that session. Everything else is already in the files.
