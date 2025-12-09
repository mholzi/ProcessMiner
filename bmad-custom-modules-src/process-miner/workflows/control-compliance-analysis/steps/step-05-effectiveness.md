---
name: 'step-05-effectiveness'
description: 'Assess control effectiveness for each control point'

# Path Definitions
module_root: '{project-root}/bmad-custom-modules-src/process-miner'
workflow_path: '{module_root}/workflows/control-compliance-analysis'

# File References
thisStepFile: '{workflow_path}/steps/step-05-effectiveness.md'
nextStepFile: '{workflow_path}/steps/step-06-audit-trail.md'
workflowFile: '{workflow_path}/workflow.md'

# Shared Protocols
protocolsFile: '{module_root}/workflows/shared/protocols/protocols.md'

# Output Files
complianceAssessmentFile: '{current_process_folder}/compliance-control-assessment.md'
controlPointsDetailFile: '{current_process_folder}/control-points-detail.md'

# Task References
advancedElicitationTask: '{project-root}/.bmad/core/tasks/advanced-elicitation.xml'
---

# Step 5: Control Effectiveness Assessment

## STEP GOAL

Assess the effectiveness of each control point. Rate consistency, detection capability, evidence quality, accountability, and timeliness. Assign CEA# IDs to assessments. This corresponds to **Section 4** of the compliance-control-assessment template.

## MANDATORY EXECUTION RULES (READ FIRST):

### Universal Rules:
- **NEVER** generate content without user input
- **CRITICAL**: Read the complete step file before taking any action
- **CRITICAL**: When loading next step, ensure entire file is read
- YOU ARE A FACILITATOR, not a content generator

### Role Reinforcement:
- You are a Control Analyst (Compliance & Control Specialist)
- Continue using your established name, communication_style, and persona
- Control effectiveness over control existence - having a control doesn't mean it works
- Direct about weaknesses - no sugar-coating

### Step-Specific Rules:
- Each assessment gets a unique CEA# ID using format: CEA-{process_abbreviation}-### (e.g., CEA-ONB-001)
- MUST link assessments to CP# controls
- Rate multiple dimensions of effectiveness
- Identify strengths and weaknesses
- **FORBIDDEN** to start audit trail analysis in this step (that's Step 6)

## EFFECTIVENESS RATING SCALE

| Rating | Score | Description |
|--------|-------|-------------|
| Highly Effective | 5 | Control consistently operates as designed with strong evidence |
| Effective | 4 | Control operates as designed with minor variations |
| Partially Effective | 3 | Control operates but with notable deficiencies |
| Ineffective | 2 | Control does not reliably achieve its objective |
| Not Operating | 1 | Control is not being performed |

## ASSESSMENT DIMENSIONS

| Dimension | What It Measures |
|-----------|-----------------|
| Consistency | Is the control performed every time it should be? |
| Detection | Does it catch exceptions when they occur? |
| Evidence Quality | Is there adequate proof the control was performed? |
| Accountability | Is there clear ownership and follow-up? |
| Timeliness | Is the control performed when it should be? |

## EXECUTION PROTOCOLS

- Load protocols from `{protocolsFile}` for elicitation techniques
- Reference controls (CP#) from Step 3
- Assess each control across multiple dimensions
- Use advanced-elicitation-task for probing on weaknesses

## CONTEXT BOUNDARIES

- Session initialized in Step 1
- Controls cataloged in Step 3 with CP# IDs
- Gaps identified in Step 4
- This step assesses how well existing controls work

---

## EXECUTION SEQUENCE

### 1. Display Progress and Context

```
**Progress: Step 5 of 10 - Control Effectiveness Assessment**

Now let's assess how effective your existing controls are.

Having a control doesn't mean it works. I'll assess each control on:
- Consistency - performed every time?
- Detection - catches exceptions?
- Evidence - proof it was performed?
- Accountability - clear ownership?
- Timeliness - performed on time?

**Controls to Assess:**
| CP# | Control Name | Type | Execution |
|-----|--------------|------|-----------|
{{for each control}}
| {{control.id}} | {{control.name}} | {{control.type}} | {{control.execution}} |
{{/for}}
```

### 2. Control Effectiveness Assessment Loop

```
<loop name="effectiveness_assessment" for="each control in controls">

  <format>
  ---
  **Control: {{control.id}} - {{control.name}}**
  Type: {{control.type_purpose}} | Execution: {{control.type_execution}}
  Owner: {{control.owner}}
  Frequency: {{control.frequency}}
  </format>

  <format>
  **Assessment** → Assigning ID: CEA-{process_abbreviation}-{{next_id_padded}}
  </format>

  <ask response="cea.last_tested">
  When was this control last tested or audited?
  (e.g., "Q3 2024", "Never tested", "Monthly self-assessment")
  </ask>

  <format>
  **Rate each dimension (1-5):**
  </format>

  <ask response="cea.consistency_rating">
  **Consistency** - Is this control performed every time it should be?
  - [ ] 5 - Always performed without exception
  - [ ] 4 - Almost always, rare exceptions
  - [ ] 3 - Usually performed, some gaps
  - [ ] 2 - Inconsistently performed
  - [ ] 1 - Rarely or never performed
  </ask>

  <ask response="cea.consistency_notes">
  Notes on consistency (e.g., why gaps occur, compensating factors):
  </ask>

  <ask response="cea.detection_rating">
  **Detection** - Does this control catch exceptions when they occur?
  - [ ] 5 - Catches all exceptions
  - [ ] 4 - Catches most exceptions
  - [ ] 3 - Catches some exceptions
  - [ ] 2 - Misses many exceptions
  - [ ] 1 - Does not detect exceptions
  </ask>

  <ask response="cea.detection_notes">
  Notes on detection (e.g., known misses, detection rate if known):
  </ask>

  <ask response="cea.evidence_rating">
  **Evidence Quality** - Is there adequate proof the control was performed?
  - [ ] 5 - Complete, auditable evidence
  - [ ] 4 - Good evidence, minor gaps
  - [ ] 3 - Partial evidence
  - [ ] 2 - Weak evidence
  - [ ] 1 - No evidence captured
  </ask>

  <ask response="cea.evidence_notes">
  Notes on evidence (e.g., what's captured, what's missing):
  </ask>

  <ask response="cea.accountability_rating">
  **Accountability** - Is there clear ownership and follow-up on exceptions?
  - [ ] 5 - Clear owner, exceptions always followed up
  - [ ] 4 - Clear owner, most exceptions followed up
  - [ ] 3 - Owner defined but follow-up inconsistent
  - [ ] 2 - Unclear ownership
  - [ ] 1 - No accountability
  </ask>

  <ask response="cea.accountability_notes">
  Notes on accountability:
  </ask>

  <ask response="cea.timeliness_rating">
  **Timeliness** - Is the control performed when it should be?
  - [ ] 5 - Always on time
  - [ ] 4 - Usually on time
  - [ ] 3 - Sometimes delayed
  - [ ] 2 - Often delayed
  - [ ] 1 - Chronically late or not performed
  </ask>

  <ask response="cea.timeliness_notes">
  Notes on timeliness:
  </ask>

  <action>
  Calculate overall effectiveness:
  overall_score = average(consistency, detection, evidence, accountability, timeliness)

  Map to rating:
  - 4.5-5.0 = Highly Effective
  - 3.5-4.4 = Effective
  - 2.5-3.4 = Partially Effective
  - 1.5-2.4 = Ineffective
  - 1.0-1.4 = Not Operating
  </action>

  <format>
  **{{control.id}} Overall Effectiveness: {{overall_rating}} ({{overall_score}}/5)**
  </format>

  <ask response="cea.findings">
  Any additional findings or observations about this control?
  </ask>

</loop>
```

### 3. Identify Strengths and Weaknesses

```
<action>
Categorize controls by effectiveness:

**Control Strengths (Highly Effective / Effective):**
{{for each control where rating >= 3.5}}
- {{control.id}}: {{control.name}} ({{rating}})
{{/for}}

**Control Weaknesses (Partially Effective or worse):**
{{for each control where rating < 3.5}}
- {{control.id}}: {{control.name}} ({{rating}}) - {{key_issue}}
{{/for}}
</action>

<ask response="strengths_validation">
Do you agree with this categorization of strengths and weaknesses?
- [ ] Yes - accurate
- [ ] Partially - some adjustments needed
- [ ] No - significant disagreement
</ask>

<check if="strengths_validation != 'Yes'">
  <ask response="adjustments">What adjustments are needed?</ask>
</check>
```

### 4. Improvement Opportunities

```
<format>
**Improvement Opportunities**

Based on the effectiveness assessments, here are improvement opportunities:
</format>

<action>
For each control with rating < 4.0:
Generate improvement opportunity based on lowest-rated dimensions.
</action>

<ask response="improvement_priorities">
Which controls are the highest priority for improvement?
(Consider risk, effort, and impact)
</ask>
```

### 5. Capture Confidence

```
<ask response="section_4_confidence">
How confident are you in these effectiveness assessments?

- [ ] High - based on recent audit/testing
- [ ] Medium - based on operational knowledge
- [ ] Low - preliminary, needs testing
</ask>

<ask response="section_4_confidence_basis">
What's the basis for this confidence? (e.g., audit results, testing, observation)
</ask>
```

### 6. Update Output Files

```
<action silent="true">
Update {complianceAssessmentFile} Section 4 (Control Effectiveness Assessment):

4.1 Control Strengths:
List controls rated Effective or Highly Effective

4.2 Control Weaknesses:
List controls rated Partially Effective or worse

4.3 Improvement Opportunities:
Prioritized list of improvements

Build summary table:
| CEA# | Control | Effectiveness Rating | Last Tested | Findings |

Section Confidence: {{section_4_confidence}}
Confidence Basis: {{section_4_confidence_basis}}
</action>

<action silent="true">
Update {controlPointsDetailFile} for each control:
- effectiveness_assessment section
- Overall effectiveness rating
- Dimension ratings and notes
- Gaps and weaknesses
</action>
```

### 7. Summary and Transition

Display:
```
**Control Effectiveness Assessment Complete**

| Rating | Count | % of Controls |
|--------|-------|---------------|
| Highly Effective | {{highly_effective_count}} | {{highly_effective_pct}}% |
| Effective | {{effective_count}} | {{effective_pct}}% |
| Partially Effective | {{partial_count}} | {{partial_pct}}% |
| Ineffective | {{ineffective_count}} | {{ineffective_pct}}% |
| Not Operating | {{not_operating_count}} | {{not_operating_pct}}% |

**Average Effectiveness:** {{average_effectiveness}}/5

**Top Improvement Priorities:**
{{#each improvement_priorities}}
- {{control.id}}: {{improvement_area}}
{{/each}}

Next, we'll document audit trail requirements.
```

### 8. Proceed to Next Step

Display:
```
**Progress: Step 5 of 10 - Effectiveness Assessment Complete**

Now let's document the audit trail and evidence requirements.
```

```
<action>Load, read entire file, then execute {nextStepFile}</action>
```

---

## CRITICAL STEP COMPLETION NOTE

This is an auto-proceed step. IMMEDIATELY after [effectiveness assessed] and [output files updated], load and read fully `{nextStepFile}` to execute and begin audit trail analysis.

---

## SYSTEM SUCCESS/FAILURE METRICS

### SUCCESS:
- All controls assessed with CEA# IDs
- Each dimension rated (consistency, detection, evidence, accountability, timeliness)
- Overall effectiveness calculated
- Strengths and weaknesses categorized
- Improvement opportunities identified
- Confidence assessment captured
- Both output files updated
- Ready to proceed to Step 6

### SYSTEM FAILURE:
- Did not assign CEA# IDs
- Did not rate all dimensions
- Did not identify weaknesses
- Started audit trail analysis
- Did not update output files
- Skipped to later steps

**Master Rule:** Skipping steps, optimizing sequences, or not following exact instructions is FORBIDDEN and constitutes SYSTEM FAILURE.
