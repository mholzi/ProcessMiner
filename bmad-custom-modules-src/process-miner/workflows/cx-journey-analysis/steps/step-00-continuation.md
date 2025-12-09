---
name: 'step-00-continuation'
description: 'Handle session resumption for CX Journey Analysis workflow'

# Path Definitions
module_root: '{project-root}/bmad-custom-modules-src/process-miner'
workflow_path: '{module_root}/workflows/cx-journey-analysis'

# File References
thisStepFile: '{workflow_path}/steps/step-00-continuation.md'
workflowFile: '{workflow_path}/workflow.md'

# Step Files for resumption
step1: '{workflow_path}/steps/step-01-init.md'
step2: '{workflow_path}/steps/step-02-journey-overview.md'
step3: '{workflow_path}/steps/step-03-touchpoints.md'
step4: '{workflow_path}/steps/step-04-friction.md'
step5: '{workflow_path}/steps/step-05-moments.md'
step6: '{workflow_path}/steps/step-06-channels.md'
step7: '{workflow_path}/steps/step-07-research.md'
step8: '{workflow_path}/steps/step-08-validation.md'

# Output Files
cxJourneyFile: '{current_process_folder}/cx-journey-documentation.md'
frictionPointsFile: '{current_process_folder}/friction-points-detail.md'
clientTouchpointsFile: '{current_process_folder}/client-touchpoints-detail.md'
---

# Step 0: Session Continuation

## STEP GOAL

Resume a previously started CX Journey Analysis session. Load previous state and continue from where the user left off.

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
**Resuming CX Journey Analysis Session**

Welcome back, {contributor_name}! Let me restore your previous session.
```

### 2. Load Previous State

```
<action>
Load state from output files:
1. Read {cxJourneyFile} - extract completed sections
2. Read {frictionPointsFile} - extract captured friction points (FP#)
3. Read {clientTouchpointsFile} - extract captured touchpoints (JT#)
4. Parse frontmatter for `stepsCompleted` array
</action>
```

### 3. Display Session Summary

```
<format>
**Previous Session Summary:**

Process: {current_process_id} - {current_process_name}
Client Segment: {{client_segment}}

**Progress:**
{{for each completed_step}}
- [x] Step {{step.number}}: {{step.name}}
{{/for}}

**Captured So Far:**
| Element | Count |
|---------|-------|
| Touchpoints (JT#) | {{count_touchpoints}} |
| Friction Points (FP#) | {{count_friction_points}} |
| Enhancement Ideas (EI#) | {{count_enhancement_ideas}} |
| Moments That Matter | {{count_mtm}} |

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
