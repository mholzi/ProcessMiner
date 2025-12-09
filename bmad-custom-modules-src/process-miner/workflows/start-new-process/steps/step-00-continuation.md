---
name: 'step-00-continuation'
description: 'Handle session resumption when invoked via *continue-session command'

# Path Definitions
module_root: '{project-root}/bmad-custom-modules-src/process-miner'
workflow_path: '{module_root}/workflows/start-new-process'

# File References
thisStepFile: '{workflow_path}/steps/step-00-continuation.md'
nextStepFile: '{workflow_path}/steps/step-01-init.md'
workflowFile: '{workflow_path}/workflow.md'

# Shared Protocols
protocolsFile: '{module_root}/workflows/shared/protocols/protocols.md'

# Task References
advancedElicitationTask: '{project-root}/.bmad/core/tasks/advanced-elicitation.xml'
partyModeWorkflow: '{project-root}/.bmad/core/workflows/party-mode/workflow.md'

# Output Files
structuredDataFile: '{current_process_folder}/structured-data.json'
---

# Step 0: Continuation Check

## STEP GOAL

Handle session resumption when the workflow is invoked via `*continue-session` command. If this is a fresh start, skip directly to Step 1.

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

### Step-Specific Rules:
- This step is **auto-skip** if `start_at_step` is not set or equals 1
- Focus ONLY on resumption logic
- Do NOT begin elicitation in this step

## EXECUTION PROTOCOLS

- Show analysis before taking any action
- Load existing data if resuming
- Display clear resumption context

## CONTEXT BOUNDARIES

- `start_at_step` is set by `*continue-session` workflow
- `current_process_folder` contains existing session data
- Previous context lives in `structured-data.json`

---

## EXECUTION SEQUENCE

### 1. Check Resumption State

```
<check if="start_at_step is NOT set OR start_at_step == 1">
  <action>This is a fresh start - skip directly to Step 1</action>
  <goto step="1">Load and execute step-01-init.md</goto>
</check>
```

### 2. Handle Resumption (if start_at_step > 1)

**Load Existing Data:**
- Load `{structuredDataFile}`
- Parse session metadata, captured data, and progress

**Generate Context Summaries:**

```
<action>Generate process_summary from metadata</action>
<action>Generate progress_summary from captured data</action>
<action>Calculate element counts</action>
```

### 3. Display Resumption Notice

```
---
**Resuming Process Documentation**

Process: {current_process_id} - {current_process_name}
Resuming at: Step {{start_at_step}} of 9

---

**Process Summary:**
{{process_summary}}

A 1-paragraph synthesis from metadata: purpose, trigger, frequency, volume.
Written in plain English so the SME can quickly recall what this process is about.

---

**Captured So Far:**
{{progress_summary}}

A 1-paragraph description of what has been documented.

**Quick Stats:**
| Element | Count | Status |
|---------|-------|--------|
| Process Steps (PS#) | {{count_steps}} | {{steps_status}} |
| Exceptions (EX#) | {{count_exceptions}} | {{exceptions_status}} |
| Pain Points (PP#) | {{count_pain_points}} | {{pain_points_status}} |
| Controls (CP#) | {{count_controls}} | {{controls_status}} |
| Systems (SYS#) | {{count_systems}} | {{systems_status}} |

---

Ready to continue from Step {{start_at_step}}: {{step_name}}
---
```

### 4. Jump to Resume Step

```
<action>Load step file for start_at_step</action>
<goto step="{{start_at_step}}">Resume at identified step</goto>
```

Step file mapping:
- Step 1 → step-01-init.md
- Step 2 → step-02-import.md
- Step 3 → step-03-overview.md
- Step 4 → step-04-process-steps.md
- Step 5 → step-05-exceptions.md
- Step 6 → step-06-pain-points.md
- Step 7 → step-07-controls.md
- Step 8 → step-08-systems.md
- Step 9 → step-09-validation.md

---

## CRITICAL STEP COMPLETION NOTE

This is an auto-skip step for fresh starts. If `start_at_step` is set and > 1, display resumption context then IMMEDIATELY load and read fully the appropriate step file based on the step mapping.

---

## 🚨 SYSTEM SUCCESS/FAILURE METRICS

### ✅ SUCCESS:
- Correctly identified fresh start vs. resumption
- Loaded existing data if resuming
- Displayed clear context summary
- Jumped to correct step

### ❌ SYSTEM FAILURE:
- Attempted elicitation in this step
- Failed to load existing data when resuming
- Jumped to wrong step
- Did not display resumption context

**Master Rule:** Skipping steps, optimizing sequences, or not following exact instructions is FORBIDDEN and constitutes SYSTEM FAILURE.
