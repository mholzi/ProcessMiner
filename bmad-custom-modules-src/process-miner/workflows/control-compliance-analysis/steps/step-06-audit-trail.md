---
name: 'step-06-audit-trail'
description: 'Document audit trail requirements and evidence retention'

# Path Definitions
module_root: '{project-root}/bmad-custom-modules-src/process-miner'
workflow_path: '{module_root}/workflows/control-compliance-analysis'

# File References
thisStepFile: '{workflow_path}/steps/step-06-audit-trail.md'
nextStepFile: '{workflow_path}/steps/step-07-risk-matrix.md'
workflowFile: '{workflow_path}/workflow.md'

# Output Files
complianceAssessmentFile: '{current_process_folder}/compliance-control-assessment.md'
controlPointsDetailFile: '{current_process_folder}/control-points-detail.md'
---

# Step 6: Audit Trail Requirements

## STEP GOAL

Document audit trail requirements, evidence retention needs, and data elements that must be captured for compliance. Assign ATR# IDs. This corresponds to **Section 5** of the compliance-control-assessment template.

## MANDATORY EXECUTION RULES (READ FIRST):

### Universal Rules:
- **NEVER** generate content without user input
- **CRITICAL**: Read the complete step file before taking any action
- YOU ARE A FACILITATOR, not a content generator

### Role Reinforcement:
- You are a Control Analyst
- Audit trail is control evidence - controls without evidence are unverifiable
- Every control must have traceable evidence

### Step-Specific Rules:
- Each audit trail requirement gets ATR# ID: ATR-{process_abbreviation}-###
- MUST link to CP# controls that produce the evidence
- Capture data elements, retention periods, and storage
- **FORBIDDEN** to start risk matrix in this step (that's Step 7)

---

## CONTENT FORMAT SPECIFICATION

This step produces **Section 5: Audit Trail Requirements** of the compliance-control-assessment template.

### Section 5: Audit Trail Requirements
**Format:** Narrative intro + summary table + audit readiness assessment

**Structure:**
1. **Narrative Introduction** (2-3 paragraphs):
   - Explanation of why audit trail matters ("controls without evidence are unverifiable")
   - Overview of evidence capture across the process
   - Key audit trail considerations for readers unfamiliar with compliance auditing

2. **Audit Trail Summary Table:**
   | ATR# | Control (CP#) | Data Elements Captured | Retention Period | Storage System | Completeness |
   |------|---------------|------------------------|------------------|----------------|--------------|

3. **Audit Readiness Narrative** (2-3 paragraphs):
   - Overall assessment of audit readiness
   - Areas where evidence capture is strong
   - Gaps in audit trail that need attention
   - Accessibility of evidence for auditors

4. **Per-Control Evidence Details** (for controls with gaps or notable requirements):
   Each block includes 1 paragraph covering:
   - What evidence should be captured
   - Current state of evidence capture
   - Any gaps or improvements needed

### Writing Guidelines for Section 5:
- Explain audit trail in practical terms for non-auditors
- Emphasize the connection between evidence and control verification
- Be specific about what data elements are captured
- Highlight any retention period mismatches with regulatory requirements
- Make audit readiness assessment clear and actionable

---

## EXECUTION SEQUENCE

### 1. Display Progress and Context

```
**Progress: Step 6 of 10 - Audit Trail Requirements**

Audit trail is the evidence that controls were performed. Without evidence, controls cannot be verified.

For each control, we need to document:
- What evidence is captured
- Where it's stored
- How long it's retained
- Who can access it
```

### 2. Audit Trail by Control

```
<loop name="audit_trail_capture" for="each control in controls">

  <format>
  ---
  **Control: {{control.id}} - {{control.name}}**
  Evidence from Step 3: {{control.evidence_captured}}
  </format>

  <format>
  **Audit Trail Requirement** → Assigning ID: ATR-{process_abbreviation}-{{next_id_padded}}
  </format>

  <ask response="atr.data_elements">
  What specific data elements are captured as evidence?
  (e.g., user ID, timestamp, action taken, approval status, document reference)
  </ask>

  <ask response="atr.retention_period">
  What is the required retention period?
  - [ ] 1 year
  - [ ] 3 years
  - [ ] 5 years
  - [ ] 7 years
  - [ ] 10+ years
  - [ ] Permanent
  - [ ] Regulation-specific: ___
  </ask>

  <ask response="atr.storage_location">
  Where is this evidence stored?
  (e.g., core banking system, document management, workflow system)
  </ask>

  <ask response="atr.access_control">
  Who can access this audit trail?
  (e.g., control owner, audit, compliance, IT admin)
  </ask>

  <ask response="atr.completeness">
  Is the audit trail complete and adequate for compliance?
  - [ ] Complete - all required evidence captured
  - [ ] Partial - some gaps exist
  - [ ] Inadequate - significant gaps
  </ask>

</loop>
```

### 3. Audit Readiness Assessment

```
<format>
**Audit Readiness Assessment**
</format>

<ask response="audit_trail_gaps">
Are there any controls where audit trail is missing or inadequate?
</ask>

<ask response="audit_accessibility">
Can auditors easily access and retrieve audit evidence?
- [ ] Yes - self-service access
- [ ] Partially - requires IT support
- [ ] No - manual extraction required
</ask>
```

### 4. Update Output Files

```
<action silent="true">
Update {complianceAssessmentFile} Section 5 (Audit Trail Requirements):

Build table:
| ATR# | Requirement | Data Elements | Retention Period | System |

Section Confidence: {{section_5_confidence}}
</action>

<action silent="true">
Update {controlPointsDetailFile} for each control:
- Evidence & audit trail section
- Retention period
- Storage location
- Audit trail quality
</action>
```

### 5. Proceed to Next Step

Display:
```
**Progress: Step 6 of 10 - Audit Trail Complete**

Now let's build the risk and compliance matrix.
```

```
<action>Load, read entire file, then execute {nextStepFile}</action>
```

---

## SYSTEM SUCCESS/FAILURE METRICS

### SUCCESS:
- All audit trail requirements documented with ATR# IDs
- Data elements, retention, and storage captured
- Audit readiness assessed
- Output files updated

**Master Rule:** Skipping steps is FORBIDDEN and constitutes SYSTEM FAILURE.
