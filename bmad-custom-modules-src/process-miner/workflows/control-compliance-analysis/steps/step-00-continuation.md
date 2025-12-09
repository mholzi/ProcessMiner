---
name: 'step-00-continuation'
description: 'Handle session resumption for Control & Compliance Analysis workflow'

# Path Definitions
module_root: '{project-root}/bmad-custom-modules-src/process-miner'
workflow_path: '{module_root}/workflows/control-compliance-analysis'

# File References
thisStepFile: '{workflow_path}/steps/step-00-continuation.md'
workflowFile: '{workflow_path}/workflow.md'

# Step Files for resumption
step1: '{workflow_path}/steps/step-01-init.md'
step2: '{workflow_path}/steps/step-02-regulatory-framework.md'
step3: '{workflow_path}/steps/step-03-control-inventory.md'
step4: '{workflow_path}/steps/step-04-compliance-gaps.md'
step5: '{workflow_path}/steps/step-05-effectiveness.md'
step6: '{workflow_path}/steps/step-06-audit-trail.md'
step7: '{workflow_path}/steps/step-07-risk-matrix.md'
step8: '{workflow_path}/steps/step-08-regulatory-change.md'
step9: '{workflow_path}/steps/step-09-recommendations.md'
step10: '{workflow_path}/steps/step-10-validation.md'

# Output Files
complianceAssessmentFile: '{current_process_folder}/compliance-control-assessment.md'
controlPointsDetailFile: '{current_process_folder}/control-points-detail.md'
---

# Step 0: Session Continuation

## STEP GOAL

Resume a previously started Control & Compliance Analysis session. Load previous state and continue from where the user left off.

## MANDATORY EXECUTION RULES (READ FIRST):

### Universal Rules:
- **NEVER** generate content without user input
- **CRITICAL**: Read the complete step file before taking any action
- YOU ARE A FACILITATOR, not a content generator

### Step-Specific Rules:
- This step is ONLY executed when `start_at_step` session variable is set
- Must restore full context from previous session
- Must validate that prerequisite files still exist

---

## EXECUTION SEQUENCE

### 1. Display Continuation Message

```
**Resuming Control & Compliance Analysis Session**

Welcome back, {contributor_name}! Let me restore your previous session.
```

### 2. Load Previous State

```
<action>
Load state from output files:
1. Read {complianceAssessmentFile} - extract completed sections
2. Read {controlPointsDetailFile} - extract captured controls (CP#)
3. Parse frontmatter for `stepsCompleted` array
4. Extract all IDs: REG#, CP#, GAP#, CEA#, ATR#, RCM#, RCI#, CIR#
</action>
```

### 3. Display Session Summary

```
<format>
**Previous Session Summary:**

Process: {current_process_id} - {current_process_name}
Region: {region}

**Progress:**
{{for each completed_step}}
- [x] Step {{step.number}}: {{step.name}}
{{/for}}

**Captured So Far:**
| Element | Count |
|---------|-------|
| Regulations (REG#) | {{reg_count}} |
| Control Points (CP#) | {{cp_count}} |
| Compliance Gaps (GAP#) | {{gap_count}} |
| Assessments (CEA#) | {{cea_count}} |
| Audit Trail (ATR#) | {{atr_count}} |
| Risk Matrix (RCM#) | {{rcm_count}} |
| Regulatory Changes (RCI#) | {{rci_count}} |
| Recommendations (CIR#) | {{cir_count}} |

**Last Checkpoint:** Step {{last_step_completed}}
</format>
```

### 4. Confirm Continuation Point

```
<ask response="continue_from">
Where would you like to continue from?

{{for each remaining_step}}
- [ ] Step {{step.number}}: {{step.name}}
{{/for}}
- [ ] Start over from beginning
</ask>
```

### 5. Load Appropriate Step

```
<check if="continue_from == 'Start over'">
  <action>Load, read entire file, then execute {step1}</action>
</check>

<check if="continue_from == 'Step 2'">
  <action>Load, read entire file, then execute {step2}</action>
</check>

<check if="continue_from == 'Step 3'">
  <action>Load, read entire file, then execute {step3}</action>
</check>

<check if="continue_from == 'Step 4'">
  <action>Load, read entire file, then execute {step4}</action>
</check>

<check if="continue_from == 'Step 5'">
  <action>Load, read entire file, then execute {step5}</action>
</check>

<check if="continue_from == 'Step 6'">
  <action>Load, read entire file, then execute {step6}</action>
</check>

<check if="continue_from == 'Step 7'">
  <action>Load, read entire file, then execute {step7}</action>
</check>

<check if="continue_from == 'Step 8'">
  <action>Load, read entire file, then execute {step8}</action>
</check>

<check if="continue_from == 'Step 9'">
  <action>Load, read entire file, then execute {step9}</action>
</check>

<check if="continue_from == 'Step 10'">
  <action>Load, read entire file, then execute {step10}</action>
</check>
```

---

## SYSTEM SUCCESS/FAILURE METRICS

### SUCCESS:
- Previous state loaded from output files
- Session summary displayed accurately
- User selected continuation point
- Correct step file loaded and executed

### SYSTEM FAILURE:
- Failed to load previous state
- Did not display session summary
- Loaded wrong step file
- Lost previously captured data

**Master Rule:** Skipping steps, optimizing sequences, or not following exact instructions is FORBIDDEN and constitutes SYSTEM FAILURE.
