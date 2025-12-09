---
name: 'step-00-continuation'
description: 'Handle session resumption for transformation workflow'

# Path Definitions
module_root: '{project-root}/bmad-custom-modules-src/process-miner'
workflow_path: '{module_root}/workflows/transformation'
processes_folder: '{project-root}/docs/processes'

# File References
thisStepFile: '{workflow_path}/steps/step-00-continuation.md'
workflowFile: '{workflow_path}/workflow.md'

# Step Files
step_01: '{workflow_path}/steps/step-01-init.md'
step_02: '{workflow_path}/steps/step-02-synthesize.md'
step_03: '{workflow_path}/steps/step-03-elicit.md'
step_04: '{workflow_path}/steps/step-04-design.md'
step_05: '{workflow_path}/steps/step-05-validate.md'
step_06: '{workflow_path}/steps/step-06-resolve.md'
step_07: '{workflow_path}/steps/step-07-finalize.md'

# Output Files
transformationDataFile: '{current_process_folder}/transformation-data.json'
targetStateFile: '{current_process_folder}/target-state-documentation.md'

# Template References
# (No templates used in this continuation step)
---

# Step 0: Session Continuation

## STEP GOAL

Handle resumption of an interrupted transformation session, restoring context and navigating to the appropriate step.

## MANDATORY EXECUTION RULES (READ FIRST):

### Universal Rules:
- 🛑 **NEVER** generate content without user input
- 📖 **CRITICAL**: Read the complete step file before taking any action
- 🔄 **CRITICAL**: When loading next step, ensure entire file is read
- 📋 YOU ARE A FACILITATOR, not a content generator

### Role Reinforcement:
- ✅ You are a Process Transformation Orchestrator
- ✅ Continue using your established name, communication_style, and persona
- ✅ We are resuming a collaborative transformation session
- ✅ Restore context smoothly without re-asking for known information

### Step-Specific Rules:
- Focus ONLY on session restoration
- **FORBIDDEN** to restart from scratch if session data exists
- Load previous context before proceeding

## EXECUTION SEQUENCE

### 1. Check Session State

```
<action>
Check if {transformationDataFile} exists:

IF transformation-data.json exists:
  1. Read transformation-data.json
  2. Extract session state:
     - current_step: Last completed step number
     - process_id: {current_process_id}
     - process_name: {current_process_name}
     - contributor: {contributor_name}, {contributor_role}
     - validation_iteration: Current iteration number
     - gaps_open: Number of open validation gaps
  3. Continue to Section 2

IF transformation-data.json does NOT exist:
  <action>
  Display: "No existing transformation session found for this process."
  Load and execute {step_01} to start fresh.
  </action>
</action>
```

### 2. Display Session Summary

```
<format>
Welcome back, {contributor_name}!

**Resuming Transformation Session:**
- **Process:** {current_process_id} - {current_process_name}
- **Last Step Completed:** Step {{current_step}}
- **Validation Iteration:** {{validation_iteration}}
- **Open Gaps:** {{gaps_open}}

**Progress Overview:**
| Step | Status |
|------|--------|
| 1. Initialize & Load Context | {{step_1_status}} |
| 2. Synthesize AS-IS | {{step_2_status}} |
| 3. Elicit Target State | {{step_3_status}} |
| 4. Design TO-BE | {{step_4_status}} |
| 5. Validate with Specialists | {{step_5_status}} |
| 6. Resolve Gaps | {{step_6_status}} |
| 7. Finalize Documentation | {{step_7_status}} |
</format>
```

### 3. Offer Continuation Options

```
<ask response="continuation_choice">
How would you like to proceed?

1. **Continue from Step {{next_step}}** - Resume where you left off
2. **Review current TO-BE state** - See what's been designed so far
3. **Review open gaps** - See validation gaps requiring resolution
4. **Start over** - Discard progress and begin fresh transformation

Select an option [1-4]:
</ask>
```

### 4. Handle User Choice

```
<check if="continuation_choice == 1">
  <action>
  Display: "Resuming transformation from Step {{next_step}}..."

  Load appropriate step file based on {{next_step}}:
  - 1 → Load {step_01}
  - 2 → Load {step_02}
  - 3 → Load {step_03}
  - 4 → Load {step_04}
  - 5 → Load {step_05}
  - 6 → Load {step_06}
  - 7 → Load {step_07}
  </action>
</check>

<check if="continuation_choice == 2">
  <action>
  Read {targetStateFile} and display current TO-BE state summary:
  - Executive summary
  - Key metrics comparison (AS-IS vs TO-BE)
  - Transformation decisions made
  - Validation status

  Then return to Section 3 for next action.
  </action>
</check>

<check if="continuation_choice == 3">
  <action>
  Read gap-resolution-log.md (if exists) and display:
  - Open gaps by source agent
  - Gap severity breakdown
  - Days open for each gap

  Then return to Section 3 for next action.
  </action>
</check>

<check if="continuation_choice == 4">
  <ask response="confirm_restart">
  ⚠️ **Warning:** This will discard all transformation progress.

  Are you sure you want to start over? [y/n]
  </ask>

  <check if="confirm_restart == 'y'">
    <action>
    Archive existing transformation files with timestamp.
    Load and execute {step_01} to start fresh.
    </action>
  </check>

  <check if="confirm_restart == 'n'">
    Return to Section 3 for next action.
  </check>
</check>
```

#### EXECUTION RULES:

- ALWAYS halt and wait for user input after presenting continuation options
- ONLY proceed to selected step when user confirms choice
- After displaying status or reviews, redisplay the continuation menu
- User can chat or ask questions - always respond, then redisplay the menu

---

## CRITICAL STEP COMPLETION NOTE

This step routes to the appropriate workflow step based on session state. It should NOT be reached during normal flow - only via continue-session command.

---

## 🚨 SYSTEM SUCCESS/FAILURE METRICS

### ✅ SUCCESS:
- Session state loaded from transformation-data.json
- Progress summary displayed to user
- User given clear continuation options
- Appropriate step loaded based on user choice
- Context fully restored before proceeding

### ❌ SYSTEM FAILURE:
- Ignoring existing session state
- Restarting from scratch without user consent
- Failing to load previous context
- Losing transformation progress

**Master Rule:** Skipping steps, optimizing sequences, or not following exact instructions is FORBIDDEN and constitutes SYSTEM FAILURE.
