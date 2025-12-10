---
name: 'step-07-controls'
description: 'Capture controls and compliance requirements with CP# IDs'

# Path Definitions
module_root: '{project-root}/bmad-custom-modules-src/process-miner'
workflow_path: '{module_root}/workflows/start-new-process'

# File References
thisStepFile: '{workflow_path}/steps/step-07-controls.md'
nextStepFile: '{workflow_path}/steps/step-08-systems.md'
workflowFile: '{workflow_path}/workflow.md'

# Shared Protocols
protocolsFile: '{module_root}/workflows/shared/protocols/protocols.md'

# Related Workflows
captureItemWorkflow: '{module_root}/workflows/shared/capture-item/workflow.md'

# Task References
advancedElicitationTask: '{project-root}/.bmad/core/tasks/advanced-elicitation.xml'
partyModeWorkflow: '{project-root}/.bmad/core/workflows/party-mode/workflow.md'
brainstormingWorkflow: '{project-root}/.bmad/core/workflows/brainstorming-session/workflow.md'

# Output Files
structuredDataFile: '{current_process_folder}/structured-data.json'
mainDocumentFile: '{current_process_folder}/as-is-process-documentation.md'
controlPointsDetailFile: '{current_process_folder}/control-points-detail.md'
---

# Step 7: Identify Controls & Compliance Requirements

## STEP GOAL

Capture all compliance controls and regulatory requirements with unique CP# IDs, linked to relevant PS# process steps. Each control must trace to a regulatory requirement — banking compliance is non-negotiable.

## MANDATORY EXECUTION RULES (READ FIRST):

### Universal Rules:
- 🛑 **NEVER** generate content without user input
- 📖 **CRITICAL**: Read the complete step file before taking any action
- 🔄 **CRITICAL**: When loading next step, ensure entire file is read
- 📋 YOU ARE A FACILITATOR, not a content generator

### Role Reinforcement:
- ✅ You are a Process Documentation Analyst
- ✅ Continue using your established name, communication_style, and persona
- ✅ We engage in collaborative dialogue with the SME
- ✅ You bring documentation expertise, SME brings domain knowledge
- ✅ Maintain professional, supportive tone throughout

### Banking Compliance Principle:
- **Banking compliance is non-negotiable**
- Every control MUST trace to a requirement
- Every step rationale must be documented

### Reuse Pattern
- This step invokes the `capture-item` workflow for consistent capture experience

### Step-Specific Rules
- CP# format: `CP-{{process_name_abbrev}}-###` (e.g., CP-CRO-001)
- Each control MUST link to relevant PS# ID(s)
- Each control MUST have control_type (PREVENTIVE/DETECTIVE/CORRECTIVE)
- Each control MUST have regulatory requirement traceability
- Handle "standard controls only" case appropriately
- Focus ONLY on controls — no systems yet

## EXECUTION PROTOCOLS

- Load protocols from `{protocolsFile}`
- Invoke `capture-item` workflow for each control
- Update both main document and control-points-detail.md

## CONTEXT BOUNDARIES

- Process steps (PS#) captured in Step 4
- Exceptions (EX#) captured in Step 5
- Pain points (PP#) captured in Step 6
- Controls link to one or more PS# IDs

---

## CONTENT FORMAT SPECIFICATION

This section defines the exact formatting requirements for Section 4: Control Points and Compliance. The AI MUST follow these specifications when generating content.

### 4.1 Control Summary

**Format:**
- **Structure**: 2+ paragraphs minimum
- **Content**: Overview of control landscape (count, types, key regulations) + compliance posture/gaps

**Example:**
```
The Client Onboarding process has 8 documented control points ensuring regulatory compliance and operational integrity. Controls are distributed across preventive (5), detective (2), and corrective (1) categories, with the majority implemented as manual controls requiring human judgment.

The process addresses requirements from multiple regulatory frameworks including AML/KYC regulations, GDPR data protection requirements, and internal credit policy standards. Current coverage is comprehensive for AML/KYC requirements, with one identified gap in automated sanctions screening refresh frequency. All controls have been mapped to specific process steps and assigned clear ownership.
```

### 4.2 Control Point Summary Table

**Table Format:**
| CP# | Control Name | Type | Regulation | Process Step | Effectiveness |
|-----|--------------|------|------------|--------------|---------------|

**Column Specifications:**

| Column | Format | Example |
|--------|--------|---------|
| **CP#** | `CP-{{abbrev}}-###` where abbrev is 2-3 characters | CP-CRO-001, CP-ONB-002 |
| **Control Name** | Descriptive phrase | "Four-eyes verification of client data", "Automated sanctions screening" |
| **Type** | Type + execution method | "PREVENTIVE - MANUAL", "DETECTIVE - AUTOMATED", "CORRECTIVE - HYBRID" |
| **Regulation** | Regulatory code OR internal policy (context-dependent) | "AML/KYC Reg 4.2", "Credit Policy 3.1", "GDPR Art. 17" |
| **Process Step** | PS# + step name | "PS-002: Verify ID" |
| **Effectiveness** | Label + brief note | "HIGH — No breaches in 12 months", "MEDIUM — Manual process prone to error" |

**Example Table:**
| CP# | Control Name | Type | Regulation | Process Step | Effectiveness |
|-----|--------------|------|------------|--------------|---------------|
| CP-CRO-001 | Four-eyes verification of client data | PREVENTIVE - MANUAL | AML/KYC Reg 4.2 | PS-002: Verify ID | HIGH — No breaches in 12 months |
| CP-CRO-002 | Automated sanctions screening | DETECTIVE - AUTOMATED | AML Directive Art. 13 | PS-002: Verify ID | HIGH — Real-time screening with 99.9% uptime |
| CP-CRO-003 | Risk classification review | PREVENTIVE - MANUAL | Credit Policy 3.1 | PS-004: Risk assessment | MEDIUM — Subjective criteria, inconsistent application |

**Per-Control Detail (below table):**

For each control point, include 2-3 paragraphs covering:
- Background on the control — what it does and why it exists
- Impact — what happens if this control fails or is bypassed

**Example - Per-Control Detail:**
```markdown
#### CP-CRO-001: Four-eyes verification of client data

The four-eyes principle requires that all client data entered during onboarding be reviewed and approved by a second qualified staff member before the application can proceed. This control exists to prevent data entry errors and detect potential fraud attempts where a single staff member might collude with a client to bypass verification requirements.

This control is mandated by AML/KYC regulations which require independent verification of client identity data. Failure of this control could result in incorrect client records being established, potential sanctions breaches if client details are inaccurate, and regulatory penalties during audit. The bank has invested in training to ensure all KYC Operations staff understand the importance of thorough secondary review.
```

### 4.3 Regulatory Coverage

**Table Format:**
| Regulation | Controls Mapped | Coverage Status |
|------------|-----------------|-----------------|

**Column Specifications:**

| Column | Format | Example |
|--------|--------|---------|
| **Regulation** | Flexible — whatever is relevant to the process | "AML/KYC Directive", "GDPR", "Internal Credit Policy" |
| **Controls Mapped** | Count + CP# references | "3 (CP-001, CP-002, CP-005)" |
| **Coverage Status** | Label + note if gaps exist | "FULL", "PARTIAL — 1 gap identified", "GAP — No controls mapped" |

**Example Table:**
| Regulation | Controls Mapped | Coverage Status |
|------------|-----------------|-----------------|
| AML/KYC Directive | 4 (CP-001, CP-002, CP-003, CP-005) | FULL |
| GDPR Data Protection | 2 (CP-004, CP-006) | FULL |
| Internal Credit Policy | 2 (CP-003, CP-007) | PARTIAL — Risk appetite documentation gap |

**Per-Regulation Detail (below table):**

For each regulation, include 2-3 paragraphs covering:
- Background on the regulation — what it requires and why it matters
- Impact on this process — how it shapes control requirements

**Example - Per-Regulation Detail:**
```markdown
#### AML/KYC Directive

The Anti-Money Laundering and Know Your Customer Directive establishes requirements for financial institutions to verify client identity, assess money laundering risk, and maintain ongoing monitoring of client relationships. These requirements apply to all new client onboarding and periodic reviews of existing relationships.

For the Client Onboarding process, AML/KYC requirements drive the majority of verification activities including identity document validation, beneficial ownership identification, sanctions screening, and risk classification. Non-compliance can result in significant regulatory penalties, reputational damage, and potential criminal liability for responsible officers. The bank's compliance framework treats AML/KYC as the highest priority control domain.
```

### 4.4 Control Statistics

**Table Format:**
| Metric | Value |
|--------|-------|
| Total Control Points | {{total_control_points}} |
| Regulatory Controls | {{regulatory_controls}} |
| Internal Controls | {{internal_controls}} |
| Automated Controls | {{automated_controls}} |

### Control Detail Document (control-points-detail.md)

**Per-Control Detail Block Format:**

```markdown
## CP-XXX-###: [Control Name]

| Attribute | Value |
|-----------|-------|
| **Control ID** | CP-XXX-### |
| **Type** | [PREVENTIVE / DETECTIVE / CORRECTIVE] - [MANUAL / AUTOMATED / HYBRID] |
| **Regulation** | [Regulatory reference or internal policy] |
| **Process Step** | [PS# + step name] |
| **Effectiveness** | [Label + description] |
| **Owner** | [Business Unit / Role] |

### Description

[1-2 paragraphs describing the control — what it does, how it works, who performs it]

### Control Activities

[Narrative paragraph describing the specific activities performed as part of this control]

### Testing/Validation Approach

[Paragraph describing how this control is tested, validated, or audited]

### Regulatory Requirement Source

[Paragraph identifying the specific regulatory requirement this control addresses, with citation]

### Gap Analysis

[Paragraph identifying any gaps in control design or operation, or stating "No gaps identified"]

### Improvement Recommendations

[Bullet list or paragraph describing potential improvements to control effectiveness]
```

**Example - Control Detail:**
```markdown
## CP-CRO-002: Automated sanctions screening

| Attribute | Value |
|-----------|-------|
| **Control ID** | CP-CRO-002 |
| **Type** | DETECTIVE - AUTOMATED |
| **Regulation** | AML Directive Art. 13, OFAC Requirements |
| **Process Step** | PS-002: Verify ID |
| **Effectiveness** | HIGH — Real-time screening with 99.9% uptime |
| **Owner** | Compliance / AML Team |

### Description

All client applications are automatically screened against global sanctions lists, PEP databases, and adverse media sources before proceeding past the verification stage. The screening is performed by the WorldCheck system integrated with the CRM, providing real-time results within seconds of application submission.

Positive matches are flagged for manual review by the AML team, while clear results allow the application to proceed automatically. The system screens client names, beneficial owners, and connected parties against continuously updated watchlists.

### Control Activities

Upon application submission, the CRM triggers an API call to WorldCheck containing client identification data. The system performs fuzzy matching against sanctions lists (OFAC, EU, UN), PEP databases, and adverse media sources. Results are returned with match scores and supporting evidence. Matches above the 80% threshold are queued for AML analyst review, while lower scores are logged but allow processing to continue.

### Testing/Validation Approach

The control is tested quarterly through the submission of known test cases including names on sanctions lists and known PEP individuals. System uptime and response times are monitored continuously with alerts for degradation. Annual penetration testing validates that the integration cannot be bypassed. Internal Audit reviews screening effectiveness annually as part of the AML control assessment.

### Regulatory Requirement Source

AML Directive Article 13 requires credit institutions to apply customer due diligence measures including identification and verification of the customer's identity. OFAC regulations require US-connected institutions to screen all parties against the SDN list. The bank's AML Policy Section 4.2 mandates automated screening for all new client relationships.

### Gap Analysis

Current gap: Sanctions lists are refreshed daily, but regulatory guidance suggests real-time refresh for high-risk clients. Additionally, the current system does not screen against all regional sanctions lists, specifically missing coverage for certain Asian jurisdictions where the bank has growing exposure.

### Improvement Recommendations

- Implement real-time sanctions list refresh for high-risk client categories
- Expand screening coverage to include additional regional sanctions lists
- Enhance matching algorithms to reduce false positive rate (currently ~15%)
- Add automated re-screening trigger when client data is modified
```

### Section Confidence Statement

**Format:**
```
> **Section Confidence:** {{percentage}}% | **Basis:** {{ai_inferred_basis}}
```

- **Confidence**: AI-inferred percentage (0-100%)
- **Basis**: AI-inferred assessment explaining the confidence level

**Example:**
```
> **Section Confidence:** 88% | **Basis:** All controls mapped to regulatory requirements with clear ownership. Effectiveness assessments based on SME input. Gap analysis for 2 controls requires validation with Compliance team.
```

---

## EXECUTION SEQUENCE

### 1. Display Progress

```
**Progress: Step 7 of 9 - Controls & Compliance**

Now let's document the compliance controls and regulatory requirements.
In banking, every control must trace to a requirement — this is non-negotiable.
```

### 2. Check for Existing Controls (from Import)

```
<action>Load existing controls from {structuredDataFile} and {controlPointsDetailFile}</action>

<check if="existing_controls.length > 0">
  <!-- Complete imported controls -->
</check>

<check if="existing_controls.length == 0">
  <ask response="controls_exist">
  Are there compliance controls or regulatory requirements in this process?

  - **[A] Add** — I know a control to document
  - **[E] Explore** — Help me discover controls using elicitation techniques
  - **[S] Standard only** — Standard controls apply (we'll note that)
  </ask>
</check>
```

### 3. Handle "Standard Controls Only"

```
<check if="controls_exist == 'S' or 'Standard'">
  <format>Noted — standard controls apply. We can add specific controls later if needed.</format>
  <action>Store controls array with note: "Standard controls apply"</action>
</check>
```

### 4. Capture Controls (Fresh or Additional)

```
<loop name="control_capture" until="user indicates no more controls">
  <!-- Invoke the capture-item workflow for each control -->
  <invoke-workflow path="{captureItemWorkflow}">
    <param name="item_type">control_point</param>
    <param name="current_process_folder">{current_process_folder}</param>
    <param name="mode">create</param>
  </invoke-workflow>

  <ask response="more_controls">
  Any other controls to capture?

  - **[A] Add another** — I know another control to document
  - **[E] Explore** — Help me discover more controls (Regulatory Scan, Party Mode)
  - **[D] Done** — No more controls
  </ask>
</loop>
```

### 5. Update Output Files (Silent) — RECOVERY-SAFE

**🚨 CRITICAL: Incremental Save for Recovery**

After controls are captured (or noted as standard only), you MUST update ALL THREE files to enable session recovery:

```
<action silent="true">Update {structuredDataFile}:
  - controls array
  - Each control: id, name, description, control_type, requirement_source, links.process_steps, confidence
  - session.checkpoint.step = 7
  - session.last_updated = {{timestamp}}
</action>

<action silent="true" critical="RECOVERY">Update {mainDocumentFile} - APPEND Section 4:

  APPEND the following content to the main document:

  ---
  ## 4. Control Points and Compliance

  > **About this section:** Summary of controls. For full regulatory mapping and effectiveness analysis, see [Control Point Details](./control-points-detail.md).

  ### 4.1 Control Summary

  {{controls_summary_paragraph}}

  ### 4.2 Control Point Summary Table

  | CP# | Control Name | Type | Regulation | Process Step | Effectiveness |
  |-----|--------------|------|------------|--------------|---------------|
  {{Generate table row for each approved control}}

  ### 4.3 Regulatory Coverage

  | Regulation | Controls Mapped | Coverage Status |
  |------------|-----------------|-----------------|
  {{Generate regulatory coverage summary}}

  ### 4.4 Control Statistics

  | Metric | Value |
  |--------|-------|
  | Total Control Points | {{total_control_points}} |
  | Regulatory Controls | {{count regulatory}} |
  | Internal Controls | {{count internal}} |
  | Automated Controls | {{count automated}} |

  > **Full Analysis:** [View Control Point Details](./control-points-detail.md)
  >
  > **Section Confidence:** {{assessed_confidence}} | **Basis:** SME-validated during elicitation

  ---
</action>

<action silent="true" critical="RECOVERY">Update {controlPointsDetailFile} - WRITE FULL CONTENT:

  WRITE the full control-points-detail.md file with ALL captured control data:

  # Control Points & Compliance: {{process_name}}

  **Process ID:** {{process_id}}
  **Document Type:** Control Point Detail Analysis
  **Last Updated:** {{date}}
  **Related Document:** [AS-IS Process Documentation](./as-is-process-documentation.md)

  ---

  ## Executive Summary

  {{controls_executive_summary}}

  ---

  ## Control Point Summary Table

  | CP# | Control Name | Type | Regulation | Process Step | Effectiveness | Owner |
  |-----|--------------|------|------------|--------------|---------------|-------|
  {{Generate full table}}

  ---

  ## Detailed Control Analysis

  {{For each control, generate full detail block with:
    - Overview table (ID, Name, Type, Regulation, Process Step, Effectiveness, Owner)
    - Control Description
    - Regulatory Requirement Source
    - Control Activities
    - Testing/Validation Approach
    - Gap Analysis (if captured)
  }}

  ---

  ## Regulatory Coverage Matrix

  {{Generate matrix showing regulations vs controls}}

  ---

  This incremental save ensures:
  - If session aborts after Step 7, all controls are recoverable
  - Both summary (main doc) and detail (control-points-detail.md) are saved
  - SME work is never lost
</action>
```

### 6. Proceed to Next Step

```
**Controls & Compliance Complete!**
{{total_controls}} control points documented with CP# IDs.
Proceeding to Step 8: Systems & Tools...
```

```
<action>Load, read entire file, then execute {nextStepFile}</action>
```

---

## 🚨 SYSTEM SUCCESS/FAILURE METRICS

### ✅ SUCCESS:
- Controls captured with CP# IDs (or noted standard only)
- Each control has control_type and requirement traceability
- Each control linked to relevant PS# IDs
- Updated structured-data.json
- **APPENDED Section 4 to as-is-process-documentation.md (RECOVERY-SAFE)**
- **WROTE full control-points-detail.md (RECOVERY-SAFE)**
- Ready to proceed to Step 8

### ❌ SYSTEM FAILURE:
- Controls missing control_type or requirement traceability
- Controls not linked to PS# IDs
- Updated JSON but not control-points-detail.md (or vice versa)
- Started capturing systems in this step

**Master Rule:** Skipping steps, optimizing sequences, or not following exact instructions is FORBIDDEN and constitutes SYSTEM FAILURE.
