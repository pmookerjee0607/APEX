# APEX_CONTEXT.md
*Runtime program context for the APEX framework. Skills and agents load this file at session start and operate against its values. Without it, outputs are generic. With it, outputs are program-specific and immediately usable.*

*Template version: v1 (Phase 1). Fill in what you have. Leave optional sections blank if not in scope. Skills handle absence per the conventions in Section 1.*

---

## 1 — How This File Works

This file gives APEX skills and agents the program context they need to produce output that is specific to your program, not generic. Every skill file references this file in its Input Requirements section.

**Section status marking:**
- **Mandatory** sections must be populated for skills to operate. A missing mandatory section means the skill cannot produce reliable output.
- **Strongly recommended** sections produce significantly better output when populated. Skills will operate without them but will state explicitly in output what was missing and what default was used.
- **Optional** sections enrich output where the relevant domain is in scope. Skills fall back to their own stated defaults if absent.

**Field marking inside sections:**
- Fields marked **[Gate-relevant]** feed Governance Block Rule 4 (Authorization Precondition). If a Gate-relevant field is missing or unclear, skills do not silently assume "unregulated" or "no Gate applies." They flag the possibility and ask, per Rule 4's default-to-flagging posture.
- All other fields are configuration. If missing, skills apply their locally-defined defaults and surface what default was used in the output.

**This is durable state, not active deliverable state.** Milestones, RAID entries, current sprint demand, current variance figures, and other volatile data are per-task inputs to skills, not fields in this file. If a field changes weekly, it does not belong here. If it changes once per phase or once per program, it belongs here.

**Population sequence (recommended):** Sections 2 (Program Identity), 3 (Governance Model), and 7 (Compliance) first. These are the mandatory minimum and unblock most skill activity. Sections 4, 9, and 10 next, since they cascade into client, governance, release, and reporting outputs. Domain-specific sections (5, 6, 8) populated by the relevant function as needed.

---

## 2 — Program Identity
*Mandatory.*

**Program name:**
**Program type:** *(enterprise transformation / SaaS migration / public sector modernisation / regulated industry implementation / internal initiative / other)*
**Sponsor organisation:** *(the organisation funding and accountable for outcomes)*
**Delivery organisation:** *(the organisation accountable for execution; may be same as sponsor)*
**Current phase:** *(initiation / planning / execution / closeout / sustain)*
**Program start date:**
**Committed end date:**
**Brief one-line description:** *(what the program is delivering, in one sentence, in the program's own vocabulary)*

---

## 3 — Governance Model
*Mandatory minimum: at least one governance body and at least one named authorizer per active decision type.*

### Governance bodies

For each body, state name, cadence, decision rights, and standing membership.

**[Body name]:**
- Cadence: *(weekly / fortnightly / monthly / quarterly / ad hoc)*
- Decision rights: *(what this body authorizes; what it advises on; what it cannot decide)*
- Standing members:

*Repeat for each body. Default if not specified: a three-tier model is assumed (delivery steering, portfolio/investment review, standards or CoE council). Skills will state this default explicitly in any output that depends on it.*

### Named authorizers per decision type
*[Gate-relevant]*

| Decision type | Named authorizer | Recorded artifact |
|---|---|---|
| Charter approval | | |
| Baseline approval | | |
| Phase-gate / stage-gate progression | | |
| Scope-change approval | | |
| Release go/no-go | | |
| Re-baseline approval | | |
| Commitment sign-off above threshold | | |
| Closure approval | | |

*Rows left blank are treated by skills as Gate-relevant context missing, per Rule 4. Skills will flag the possibility of an applicable Gate and ask, rather than proceeding as if no authorization is required.*

### Escalation conventions
*(How escalations route in this program. Which body for what severity. Standing escalation paths to executive sponsor or steering. Default channel for cross-workstream escalation.)*

---

## 4 — Stakeholder Map
*Strongly recommended.*

For each material stakeholder, state name or role, organisation, formal authority, actual influence if it differs from formal authority, and any known sensitivities or relationship history.

| Stakeholder | Organisation | Formal authority | Actual influence (if different) | Sensitivities / history |
|---|---|---|---|---|
| | | | | |

*If stakeholder seniority or formal authority is unstated for a given stakeholder, skills will not assume the most senior named person is the decision-maker for a given matter. Per pm-client.md and pm-governance.md Input Requirements, skills ask rather than route to a stakeholder who may not have standing to act.*

---

## 5 — Commercial Structure
*Optional. Populate if the program is external or has external vendor components material to delivery.*

**Contract type:** *(fixed-price / time-and-materials / hybrid / outcome-based / master agreement with SOWs / not applicable)* **[Gate-relevant for commitment Gates]**
**Commercial cadence:** *(invoicing cycle, milestone-based vs periodic, billing currency)*
**Currency:** *(operating currency; multi-currency programs state base and reporting currencies)*
**FX treatment:** *(fixed at baseline / floating / hedged / not applicable)*
**Vendor relationships in scope:** *(named or role-only; whether vendors are sub to the delivery org or hold direct contracts with the sponsor; standing notice periods or commitment terms)*

---

## 6 — Methodology, Team, Tooling
*Optional. Populate if any field materially differs from program defaults or affects skill output shape.*

### Methodology

**Primary methodology:** *(Agile/Scrum / SAFe / waterfall / hybrid / discipline-specific)*
*If hybrid, state which functions operate which way.*

*Default if not specified: pm-planning.md and pm-reporting.md default to a hybrid framing and state this explicitly in output.*

### Team composition

**FTE count (delivery side):**
**FTE count (sponsor / business side):**
**Vendor count:** *(number of distinct vendor organisations involved in delivery)*
**Geographies in scope:** *(time zones, working-hour overlap windows)*
**Team structure notes:** *(e.g., dedicated vs shared resources, on-shore vs near-shore vs off-shore splits, known capacity constraints not visible in headcount)*

### Tooling stack

**Project management:** *(Jira / Azure DevOps / ServiceNow / Smartsheet / other)*
**Documentation and collaboration:** *(Confluence / SharePoint / Notion / other)*
**Communications:** *(Teams / Slack / other)*
**Financials and resourcing:** *(SAP / Workday / Oracle / spreadsheet / other)*
**Customer or service management:** *(Salesforce / ServiceNow / other)*
**Any program-specific tooling outputs feed into:**

---

## 7 — Compliance and Risk Environment
*Mandatory minimum: state regulatory regime or explicit "unregulated."*

**Regulatory regime in scope:** *(named regulations, e.g., financial services regulations, public-sector procurement rules, healthcare data rules, privacy frameworks, sector-specific frameworks, or "unregulated")* **[Gate-relevant]**
**Audit obligations:** *(internal audit, external audit, regulator audit, contractually-mandated audit; cadence)* **[Gate-relevant]**
**Compliance Gates that apply:** *(named compliance regimes whose sign-off is a precondition for release; cross-reference Section 10)* **[Gate-relevant]**
**Risk appetite / tolerance signal:** *(conservative / moderate / aggressive on schedule, budget, scope tradeoffs; or program-specific calibration)*

*Default if risk appetite is not specified: pm-risk.md applies a moderate-conservative calibration and states this in output. Schedule and compliance exposure treated as higher priority than cost variance unless input data says otherwise.*

---

## 8 — Thresholds and Triggers
*Optional but high-value if populated. Drives pm-financials.md and pm-governance.md output calibration.*

**Financial materiality threshold for disclosure:** *(percentage variance against baseline at which a variance is reported; default 5%)*
**Re-baseline trigger threshold:** *(percentage variance at which a re-baseline is considered; default 10%)* **[Gate-relevant — re-baseline triggers a Re-Baseline Gate per pm-financials.md]**
**Commitment sign-off threshold:** *(dollar or local-currency amount above which a commitment requires named authorizer sign-off; no default, must be program-specified)* **[Gate-relevant — triggers a Commitment Threshold Gate]**
**Schedule slippage materiality threshold:** *(days or percentage of remaining duration at which slippage becomes reportable; default: 5% of remaining duration or 5 business days, whichever is sooner)*
**Scope-change materiality threshold:** *(effort, cost, or duration impact above which a scope change requires governance routing; program-specific)*
**KPI thresholds for intervention:** *(per KPI, the value at which the governance model triggers intervention or an exception process)*

---

## 9 — Glossary and Conventions
*Strongly recommended. Populated even briefly, this section materially improves the program-specificity of every skill's output.*

### Program-specific terminology
*(Internal names for phases, workstreams, environments, releases, governance bodies, deliverables. Replace generic skill-output terms with program vocabulary wherever populated.)*

| Term used in program | Generic equivalent | Notes |
|---|---|---|
| | | |

### Naming conventions
*(How sprints, releases, environments, milestones, and artifacts are named in this program.)*

### Acronym register
*(Program-specific acronyms and what they expand to. Particularly load-bearing for client and steering outputs, where unexplained acronyms read as either insider sloppiness or external opacity.)*

---

## 10 — Pre-Identified Gates (Rule 4 Inventory)
*Strongly recommended. Pre-loading the Gate inventory lets skills proceed efficiently against known Gates and reserves Rule 4's flag-and-ask posture for Gates not in the inventory.*

For each Gate, state name, scope, named authorizer, recorded artifact required, and any quantitative trigger.

### Compliance and audit Gates
| Gate name | Scope (what it gates) | Named authorizer | Required recorded artifact | Trigger condition |
|---|---|---|---|---|
| | | | | |

### Phase, portfolio, and stage Gates
| Gate name | Scope | Named authorizer | Required recorded artifact | Trigger condition |
|---|---|---|---|---|
| | | | | |

### Contractual Gates
| Gate name | Scope | Named authorizer | Required recorded artifact | Trigger condition |
|---|---|---|---|---|
| | | | | |

### Financial Gates
| Gate name | Scope | Named authorizer | Required recorded artifact | Trigger condition |
|---|---|---|---|---|
| Re-Baseline Gate | EAC variance above re-baseline trigger threshold | | Re-baselined budget and approved variance memo | Variance ≥ threshold in Section 8 |
| Commitment Threshold Gate | Single commitment or aggregate commitments above sign-off threshold | | Signed approval against commitment register | Commitment ≥ threshold in Section 8 |

### Other program-specific Gates
*(Anything not covered by the categories above. Security Gates, data-migration Gates, vendor-transition Gates, etc.)*

*Gates not listed in this section are not assumed absent. Per Rule 4, skills flag the possibility of an unlisted Gate and ask, rather than treating the inventory as complete.*

---

*End of APEX_CONTEXT.md template. Skills load this file at session start. Update fields as the program evolves; this file is the program's durable state.*
