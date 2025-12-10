---
name: 'step-03-control-inventory'
description: 'Catalog and classify all control points with CP# IDs'

# Path Definitions
module_root: '{project-root}/bmad-custom-modules-src/process-miner'
workflow_path: '{module_root}/workflows/control-compliance-analysis'

# File References
thisStepFile: '{workflow_path}/steps/step-03-control-inventory.md'
nextStepFile: '{workflow_path}/steps/step-04-compliance-gaps.md'
workflowFile: '{workflow_path}/workflow.md'

# Shared Protocols
protocolsFile: '{module_root}/workflows/shared/protocols/protocols.md'

# Output Files
complianceAssessmentFile: '{current_process_folder}/compliance-control-assessment.md'
controlPointsDetailFile: '{current_process_folder}/control-points-detail.md'

# Task References
advancedElicitationTask: '{project-root}/.bmad/core/tasks/advanced-elicitation.xml'
---

# Step 3: Control Point Inventory

## STEP GOAL

Catalog all control points in the process, classify them by type, and map them to regulations (REG#) and process steps (PS#). Assign CP# IDs. This corresponds to **Section 2** of the compliance-control-assessment template and populates the control-points-detail.md document.

## MANDATORY EXECUTION RULES (READ FIRST):

### Universal Rules:
- **NEVER** generate content without user input
- **CRITICAL**: Read the complete step file before taking any action
- **CRITICAL**: When loading next step, ensure entire file is read
- YOU ARE A FACILITATOR, not a content generator

### Role Reinforcement:
- You are a Control Analyst (Compliance & Control Specialist)
- Continue using your established name, communication_style, and persona
- Use precise regulatory language with zero ambiguity
- Every control must trace to a requirement - no orphaned controls

### Step-Specific Rules:
- Each control gets a unique CP# ID using format: CP-{process_abbreviation}-### (e.g., CP-ONB-001)
- MUST link controls to REG# regulations from Step 2
- MUST link controls to PS# process steps from AS-IS documentation
- Capture both existing controls AND identify where controls should exist
- **FORBIDDEN** to assess effectiveness in this step (that's Step 5)

## CONTROL TYPE REFERENCE

**By Purpose:**
| Type | Description | Examples |
|------|-------------|----------|
| Preventive | Stops issues before they occur | Approval limits, access controls, validation rules |
| Detective | Identifies issues after they occur | Reconciliations, exception reports, audits |
| Corrective | Fixes issues when found | Remediation procedures, escalation |

**By Execution:**
| Type | Description |
|------|-------------|
| Automated | System-enforced, no human intervention |
| Manual | Human-performed |
| Semi-Automated | System-assisted but requires human action |

## EXECUTION PROTOCOLS

- Load protocols from `{protocolsFile}` for elicitation techniques
- Reference process steps (PS#) from AS-IS documentation
- Reference regulations (REG#) from Step 2
- Walk through process step-by-step to identify controls

## CONTEXT BOUNDARIES

- Session initialized in Step 1
- Regulations mapped in Step 2 with REG# IDs
- AS-IS process steps (PS#) loaded and available
- This step produces Section 2 and detail document

---

## CONTENT FORMAT SPECIFICATION

This step produces **Section 2: Control Point Inventory** of the compliance-control-assessment template and populates the control-points-detail.md document.

### Section 2.1: Mandatory Controls
**Format:** Narrative intro + summary table

**Structure:**
1. **Narrative Introduction** (2-3 paragraphs):
   - Overview of the mandatory control landscape for this process
   - Explanation of how regulatory requirements drive control design
   - Summary of control coverage and any notable patterns

2. **Summary Table:**
   | CP# | Control Name | Regulation (REG#) | Process Step (PS#) | Type | Execution |
   |-----|--------------|-------------------|--------------------|----- |-----------|

3. **Per-Control Brief** (1 paragraph each for key controls):
   - What the control does and why it's required
   - How it links to regulatory requirements

### Section 2.2: Internal Policies
**Format:** Narrative intro + table

**Structure:**
1. **Narrative Introduction** (1-2 paragraphs):
   - Explanation of internal policy-driven controls
   - How these complement regulatory controls

2. **Policy Controls Table:**
   | CP# | Control Name | Policy | Process Step (PS#) | Type |
   |-----|--------------|--------|--------------------|----- |

### Section 2.3: Audit Requirements
**Format:** Narrative intro + table

**Structure:**
1. **Narrative Introduction** (1-2 paragraphs):
   - Overview of controls that produce audit evidence
   - Explanation of evidence requirements for compliance

2. **Audit Controls Table:**
   | CP# | Control Name | Evidence Produced | Retention Period |
   |-----|--------------|-------------------|------------------|

### Control Points Detail Document
For each CP# in control-points-detail.md, include:
- **Overview table** with all control attributes
- **Control Description** (1-2 paragraphs explaining what the control does)
- **Regulatory/Policy Requirement** with context
- **Control Objective** explaining what it's designed to achieve
- **Risk Addressed** with inherent and residual risk levels
- **Control Activity** step-by-step description
- **Evidence & Audit Trail** details
- **Effectiveness Assessment** (populated in Step 5)

### Writing Guidelines for Section 2:
- Write for readers who need to understand the control landscape quickly
- Explain the PURPOSE of each control, not just its existence
- Use clear language to describe control activities
- Ensure traceability is evident (REG# → CP# → PS#)
- Group controls logically to show patterns and relationships

---

## EXECUTION SEQUENCE

### 1. Display Progress and Context

```
**Progress: Step 3 of 10 - Control Point Inventory**

Now let's catalog all controls that govern this process.

For each control, I'll ask:
- What does it control?
- What regulation requires it?
- Which process step(s) does it apply to?
- Is it automated or manual?
- Who owns it?

**Regulations from Step 2:**
| REG# | Regulation | Key Requirements |
|------|------------|------------------|
{{for each regulation}}
| {{reg.id}} | {{reg.name}} | {{reg.requirements_summary}} |
{{/for}}

**Process Steps from AS-IS:**
| PS# | Step Name | Owner |
|-----|-----------|-------|
{{for each step in loaded_process_steps}}
| {{step.id}} | {{step.name}} | {{step.owner}} |
{{/for}}
```

### 2. Existing Controls Review

```
<format>
**Review Existing Controls**

First, let's review any controls already documented in the AS-IS process:

{{#if existing_controls.length > 0}}
| CP# | Control Name | Type |
|-----|--------------|------|
{{for each control in existing_controls}}
| {{control.id}} | {{control.name}} | {{control.type}} |
{{/for}}
{{else}}
No controls were documented in the AS-IS. We'll build the inventory from scratch.
{{/if}}
</format>

<check if="existing_controls.length > 0">
  <ask response="review_existing">
  Are these controls still accurate and complete?
  - [ ] Yes - keep as documented
  - [ ] Partially - some need updates
  - [ ] No - significant changes needed
  </ask>
</check>
```

### 3. Control Discovery by Process Step

```
<format>
Let's walk through each process step to identify controls.
For each step, we'll capture what controls exist or should exist.
</format>

<loop name="step_control_discovery" for="each step in process_steps">

  <format>
  ---
  **Process Step: {{step.id}} - {{step.name}}**
  Owner: {{step.owner}}
  </format>

  <ask response="step_has_controls">
  Does this step have any controls? (approvals, validations, checks, verifications)

  - [ ] Yes - controls exist
  - [ ] No - but controls are needed
  - [ ] No - no controls needed
  </ask>

  <check if="step_has_controls == 'Yes' OR step_has_controls == 'No - but controls are needed'">

    <loop name="control_capture" until="user says done with this step">

      <ask response="control.name">
      What is this control? (Brief name)
      </ask>

      <format>
      **Control: {{control.name}}** → Assigning ID: CP-{process_abbreviation}-{{next_id_padded}}
      </format>

      <ask response="control.description">
      Describe what this control does:
      </ask>

      <ask response="control.type_purpose">
      What type of control is this? (by purpose)
      - [ ] Preventive - stops issues before they occur
      - [ ] Detective - identifies issues after they occur
      - [ ] Corrective - fixes issues when found
      </ask>

      <ask response="control.type_execution">
      How is this control executed?
      - [ ] Automated - system-enforced
      - [ ] Manual - human-performed
      - [ ] Semi-Automated - system-assisted, human action required
      </ask>

      <ask response="control.linked_regulations">
      Which regulation(s) require this control?
      (Enter REG# IDs from Step 2, or "Internal Policy" if not regulatory)
      </ask>

      <ask response="control.owner">
      Who owns this control? (role/position)
      </ask>

      <ask response="control.frequency">
      How often is this control performed?
      - [ ] Per transaction
      - [ ] Daily
      - [ ] Weekly
      - [ ] Monthly
      - [ ] Quarterly
      - [ ] Annually
      - [ ] Event-triggered
      </ask>

      <ask response="control.control_activity">
      What is the specific control activity? (step-by-step what happens)
      </ask>

      <ask response="control.evidence_captured">
      What evidence is captured when this control is performed?
      (e.g., approval logs, exception reports, sign-offs)
      </ask>

      <ask response="more_controls">
      Are there more controls for this step?
      - [ ] Yes - add another
      - [ ] No - done with this step
      </ask>

    </loop>

  </check>

</loop>
```

### 4. Mandatory Controls Check

```
<format>
**Mandatory Controls Check**

Based on the regulations mapped (REG#), let's verify all mandatory controls are captured.
</format>

<action>
For each REG# regulation with "Fully Applicable" or "Partially Applicable" status:
- List specific requirements
- Check if a control (CP#) is linked to each requirement
- Identify any uncontrolled requirements (gaps)
</action>

<ask response="mandatory_controls_complete">
Review the regulatory requirements above. Are all mandatory controls captured?

- [ ] Yes - all requirements have controls
- [ ] No - we missed some mandatory controls
</ask>

<check if="mandatory_controls_complete == 'No'">
  <loop name="missing_mandatory" until="user says all captured">
    <ask response="missing_control.requirement">Which requirement is missing a control?</ask>
    <ask response="missing_control.control_name">What control should exist?</ask>
    <!-- Capture full control details as in Section 3 -->
  </loop>
</check>
```

### 5. Segregation of Duties Check

```
<format>
**Segregation of Duties (SoD) Review**

Segregation of duties is non-negotiable in banking. Let's verify SoD controls.
</format>

<ask response="sod_applicable">
Does this process involve any of these SoD-sensitive activities?
- Maker-checker requirements
- Four-eyes principle
- Transaction approval
- Access provisioning
- Payment authorization

- [ ] Yes - SoD applies
- [ ] No - SoD not applicable
</ask>

<check if="sod_applicable == 'Yes'">
  <ask response="sod_controls">
  How is segregation of duties enforced in this process?
  (List the controls that ensure SoD)
  </ask>

  <ask response="sod_enforced">
  Is SoD enforcement automated (system-enforced) or manual?
  - [ ] Automated - system prevents same-person approval
  - [ ] Manual - policy-based, relies on compliance
  - [ ] Partially automated
  </ask>
</check>
```

### 6. Capture Confidence

```
<ask response="section_2_confidence">
How confident are you in the control inventory we captured?

- [ ] High - comprehensive, recent audit confirmed
- [ ] Medium - good coverage, may have gaps
- [ ] Low - incomplete, needs validation
</ask>

<ask response="section_2_confidence_basis">
What's the basis for this confidence? (e.g., control testing, audit results, assumption)
</ask>
```

### 7. Update Output Files

```
<action silent="true">
Update {complianceAssessmentFile} Section 2 (Control Point Inventory):

2.1 Mandatory Controls:
List all regulatory-required controls (CP# linked to REG#)

2.2 Internal Policies:
List controls driven by internal policy

2.3 Audit Requirements:
List controls that produce audit evidence

Build summary table:
| CP# | Control Name | Type | Regulation | Process Step | Effectiveness |
</action>

<action silent="true">
Update {controlPointsDetailFile} with full control details:

For each CP#:
- Overview table
- Control description
- Regulatory/policy requirement
- Control objective
- Risk addressed
- Control activity
- Timing and frequency
- Execution details
- Evidence & audit trail
- Linked PS# references
- Linked REG# references

Calculate statistics:
- total_controls
- regulatory_count, internal_count
- automated_count, manual_count
- preventive_count, detective_count, corrective_count
</action>
```

### 8. Summary and Transition

Display:
```
**Control Inventory Complete**

| Metric | Value |
|--------|-------|
| Total Controls | {{total_controls}} |
| Regulatory Controls | {{regulatory_count}} |
| Internal Policy Controls | {{internal_count}} |
| Automated | {{automated_count}} |
| Manual | {{manual_count}} |
| Preventive | {{preventive_count}} |
| Detective | {{detective_count}} |
| Corrective | {{corrective_count}} |
| SoD Controls | {{sod_count}} |
| Confidence | {{section_2_confidence}} |

**Controls by Process Step:**
{{controls_by_step_summary}}

Next, we'll analyze compliance gaps - where requirements lack adequate controls.
```

### 9. Proceed to Next Step

Display:
```
**Progress: Step 3 of 10 - Control Inventory Complete**

Now let's identify compliance gaps between requirements and controls.
```

```
<action>Load, read entire file, then execute {nextStepFile}</action>
```

---

## CRITICAL STEP COMPLETION NOTE

This is an auto-proceed step. IMMEDIATELY after [controls cataloged] and [output files updated], load and read fully `{nextStepFile}` to execute and begin compliance gap analysis.

---

## SYSTEM SUCCESS/FAILURE METRICS

### SUCCESS:
- All controls identified with CP# IDs in correct format
- Each control linked to REG# or internal policy
- Each control linked to PS# process steps
- Control type (purpose and execution) captured
- Control activity and evidence documented
- SoD controls verified
- Confidence assessment captured
- Both output files updated
- Ready to proceed to Step 4

### SYSTEM FAILURE:
- Did not assign CP# IDs
- Did not link to REG# regulations
- Did not link to PS# process steps
- Started assessing effectiveness
- Did not update output files
- Skipped to later steps

**Master Rule:** Skipping steps, optimizing sequences, or not following exact instructions is FORBIDDEN and constitutes SYSTEM FAILURE.
