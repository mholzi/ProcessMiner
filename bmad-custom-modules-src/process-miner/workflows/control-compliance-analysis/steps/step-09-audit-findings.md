---
name: 'step-09-audit-findings'
description: 'Capture and assess open audit findings affecting the process'

# Path Definitions
module_root: '{project-root}/bmad-custom-modules-src/process-miner'
workflow_path: '{module_root}/workflows/control-compliance-analysis'

# File References
thisStepFile: '{workflow_path}/steps/step-09-audit-findings.md'
nextStepFile: '{workflow_path}/steps/step-10-recommendations.md'
workflowFile: '{workflow_path}/workflow.md'

# Output Files
complianceAssessmentFile: '{current_process_folder}/compliance-control-assessment.md'
controlPointsDetailFile: '{current_process_folder}/control-points-detail.md'
---

# Step 9: Open Audit Findings

## STEP GOAL

Capture and document open audit findings from internal audits, external audits, and regulatory examinations that affect this process. Assess remediation status and link to affected controls. Assign OAF# IDs. This corresponds to **Section 8** of the compliance-control-assessment template.

## MANDATORY EXECUTION RULES (READ FIRST):

### Universal Rules:
- **NEVER** generate content without user input
- **CRITICAL**: Read the complete step file before taking any action
- **CRITICAL**: When loading next step, ensure entire file is read
- YOU ARE A FACILITATOR, not a content generator

### Role Reinforcement:
- You are a Control Analyst (Compliance & Control Specialist)
- Continue using your established name, communication_style, and persona
- Audit findings represent validated control deficiencies - treat them seriously
- Direct about findings and remediation status - no sugar-coating

### Step-Specific Rules:
- Each open audit finding gets OAF# ID: OAF-{process_abbreviation}-### (e.g., OAF-ONB-001)
- MUST link findings to affected CP# controls
- Capture finding source (internal audit, external audit, regulatory exam)
- Track remediation status and target closure dates
- **FORBIDDEN** to start recommendations in this step (that's Step 10)

## FINDING SEVERITY REFERENCE

| Severity | Description | Expected Remediation |
|----------|-------------|---------------------|
| Critical | Material weakness, immediate regulatory risk | Immediate action required |
| High | Significant deficiency, compliance exposure | 30-60 days |
| Medium | Control weakness, improvement needed | 90 days |
| Low | Minor issue, best practice gap | Next audit cycle |

## FINDING SOURCE REFERENCE

| Source | Description |
|--------|-------------|
| Internal Audit | Findings from internal audit department |
| External Audit | Findings from external auditors (financial audit) |
| Regulatory Exam | Findings from regulatory examinations |
| Self-Assessment | Findings from control self-assessments |
| Incident Review | Findings from incident/issue investigations |

---

## CONTENT FORMAT SPECIFICATION

This step produces **Section 8: Open Audit Findings** of the compliance-control-assessment template.

### Section 8: Open Audit Findings
**Format:** Narrative intro + summary table + per-finding detail blocks

**Structure:**
1. **Narrative Introduction** (2-3 paragraphs):
   - Overview of open audit findings affecting this process
   - Summary of finding sources (internal audit, external audit, regulatory exam)
   - Overall remediation status and key concerns for non-specialists

2. **Open Findings Summary Table:**
   | OAF# | Finding | Source | Date Issued | Severity | Affected Control (CP#) | Status | Target Closure |
   |------|---------|--------|-------------|----------|------------------------|--------|----------------|

3. **Per-Finding Detail Blocks** (for Critical and High severity findings):
   Each block includes 1-2 paragraphs covering:
   - What was found (the deficiency)
   - Root cause or contributing factors
   - Impact and risk if not remediated
   - Remediation plan and current progress
   - Link to affected controls (CP#)

4. **Remediation Status Summary** (1-2 paragraphs):
   - Overall progress on audit finding remediation
   - Any overdue or at-risk items
   - Implications for compliance posture

### Writing Guidelines for Section 8:
- Present findings factually without minimizing their significance
- Explain findings in plain language for non-auditors
- Be specific about what needs to be fixed and why
- Connect findings to affected controls to show traceability
- Highlight overdue or at-risk remediation items

---

## EXECUTION SEQUENCE

### 1. Display Progress and Context

```
**Progress: Step 9 of 11 - Open Audit Findings**

Audit findings represent validated control deficiencies that require attention.

Let's capture any open audit findings that affect this process from:
- Internal Audit
- External Audit
- Regulatory Examinations
- Control Self-Assessments
- Incident Reviews
```

### 2. Check for Open Findings

```
<ask response="has_open_findings">
Are there any open audit findings that affect this process?

- [ ] Yes - there are open findings
- [ ] No - no open findings
- [ ] Unknown - I'm not sure
</ask>

<check if="has_open_findings == 'Unknown'">
  <format>
  I recommend checking with your audit or compliance team before proceeding.
  Open audit findings are important inputs for control improvement recommendations.
  </format>

  <ask response="proceed_without_findings">
  Would you like to:
  - [ ] Proceed without audit findings (we can add later)
  - [ ] Pause to gather this information
  </ask>
</check>
```

### 3. Capture Open Audit Findings

```
<check if="has_open_findings == 'Yes'">

  <loop name="audit_finding_capture" until="user says done">

    <ask response="oaf.finding_title">
    What is the finding? (Brief title/description)
    </ask>

    <format>
    **Open Audit Finding** → Assigning ID: OAF-{process_abbreviation}-{{next_id_padded}}
    </format>

    <ask response="oaf.source">
    What is the source of this finding?
    - [ ] Internal Audit
    - [ ] External Audit
    - [ ] Regulatory Examination
    - [ ] Control Self-Assessment
    - [ ] Incident Review
    - [ ] Other: ___
    </ask>

    <ask response="oaf.date_issued">
    When was this finding issued? (e.g., Q2 2024, March 2024)
    </ask>

    <ask response="oaf.severity">
    What is the severity rating?
    - [ ] Critical - Material weakness, immediate regulatory risk
    - [ ] High - Significant deficiency, compliance exposure
    - [ ] Medium - Control weakness, improvement needed
    - [ ] Low - Minor issue, best practice gap
    </ask>

    <ask response="oaf.finding_description">
    Describe the finding in detail:
    - What was the deficiency identified?
    - What was the expected state vs actual state?
    </ask>

    <ask response="oaf.root_cause">
    What is the root cause or contributing factors?
    </ask>

    <ask response="oaf.affected_controls">
    Which controls (CP#) are affected by this finding?
    (Enter CP# IDs from Step 3, or "New control needed" if none exists)
    </ask>

    <ask response="oaf.remediation_plan">
    What is the remediation plan?
    </ask>

    <ask response="oaf.status">
    What is the current remediation status?
    - [ ] Not Started
    - [ ] In Progress - On Track
    - [ ] In Progress - At Risk
    - [ ] In Progress - Overdue
    - [ ] Pending Validation
    - [ ] Closed
    </ask>

    <ask response="oaf.target_closure">
    What is the target closure date?
    </ask>

    <ask response="oaf.owner">
    Who owns the remediation?
    </ask>

    <ask response="more_findings">
    Are there more open findings to capture?
    - [ ] Yes - add another
    - [ ] No - done with findings
    </ask>

  </loop>

</check>
```

### 4. Findings Summary

```
<check if="has_open_findings == 'Yes'">

  <action>
  Generate findings summary:

  | Severity | Count | On Track | At Risk | Overdue |
  |----------|-------|----------|---------|---------|
  | Critical | {{critical_count}} | {{critical_on_track}} | {{critical_at_risk}} | {{critical_overdue}} |
  | High | {{high_count}} | {{high_on_track}} | {{high_at_risk}} | {{high_overdue}} |
  | Medium | {{medium_count}} | {{medium_on_track}} | {{medium_at_risk}} | {{medium_overdue}} |
  | Low | {{low_count}} | {{low_on_track}} | {{low_at_risk}} | {{low_overdue}} |
  </action>

  <format>
  **Open Audit Findings Summary:**

  | Metric | Value |
  |--------|-------|
  | Total Open Findings | {{total_findings}} |
  | Critical/High Severity | {{critical_high_count}} |
  | Overdue Items | {{overdue_count}} |
  | At Risk Items | {{at_risk_count}} |

  **Findings by Source:**
  {{findings_by_source_summary}}
  </format>

</check>
```

### 5. Capture Confidence

```
<ask response="section_8_confidence">
How confident are you in the completeness of audit findings captured?

- [ ] High - I have access to the complete findings register
- [ ] Medium - I captured the main findings but may have missed some
- [ ] Low - This is preliminary, needs validation with audit/compliance
</ask>

<ask response="section_8_confidence_basis">
What's the basis for this confidence? (e.g., audit tracker access, memory, assumption)
</ask>
```

### 6. Update Output Files

```
<action silent="true">
Update {complianceAssessmentFile} Section 8 (Open Audit Findings):

8.1 Findings Overview:
Narrative introduction

8.2 Open Findings Summary:
| OAF# | Finding | Source | Date Issued | Severity | Affected Control (CP#) | Status | Target Closure |

8.3 Finding Details:
Per-finding detail blocks for Critical and High severity

8.4 Remediation Status:
Summary narrative

Section Confidence: {{section_8_confidence}}
Confidence Basis: {{section_8_confidence_basis}}
</action>

<action silent="true">
Update {controlPointsDetailFile} for affected controls:
- Link to related OAF# findings
- Note audit finding impact on control
</action>
```

### 7. Summary and Transition

Display:
```
**Open Audit Findings Captured**

| Metric | Value |
|--------|-------|
| Total Open Findings | {{total_findings}} |
| Critical Severity | {{critical_count}} |
| High Severity | {{high_count}} |
| Medium Severity | {{medium_count}} |
| Low Severity | {{low_count}} |
| Overdue Items | {{overdue_count}} |
| Confidence | {{section_8_confidence}} |

**Key Concerns:**
{{#each critical_high_findings}}
- OAF-{process_abbreviation}-{{id}}: {{title}} ({{severity}} - {{status}})
{{/each}}

Next, we'll consolidate all improvement recommendations.
```

### 8. Proceed to Next Step

Display:
```
**Progress: Step 9 of 11 - Open Audit Findings Complete**

Now let's consolidate recommendations for control improvement.
```

```
<action>Load, read entire file, then execute {nextStepFile}</action>
```

---

## CRITICAL STEP COMPLETION NOTE

This is an auto-proceed step. IMMEDIATELY after [findings captured] and [output files updated], load and read fully `{nextStepFile}` to execute and begin control improvement recommendations.

---

## SYSTEM SUCCESS/FAILURE METRICS

### SUCCESS:
- All open audit findings captured with OAF# IDs in correct format
- Each finding linked to affected CP# controls
- Severity and remediation status assessed
- Findings summary generated
- Confidence assessment captured
- Output files updated
- Ready to proceed to Step 10

### SYSTEM FAILURE:
- Did not assign OAF# IDs
- Did not link to CP# controls
- Did not assess severity or status
- Started recommendations
- Did not update output files
- Skipped to later steps

**Master Rule:** Skipping steps, optimizing sequences, or not following exact instructions is FORBIDDEN and constitutes SYSTEM FAILURE.
