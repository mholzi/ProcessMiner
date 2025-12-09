---
name: 'step-02-capture-reason'
description: 'Capture discontinuation reason for audit trail'

# Path Definitions
module_root: '{project-root}/bmad-custom-modules-src/process-miner'
workflow_path: '{module_root}/workflows/discontinue-process'

# File References
thisStepFile: '{workflow_path}/steps/step-02-capture-reason.md'
nextStepFile: '{workflow_path}/steps/step-03-confirmation.md'
workflowFile: '{workflow_path}/workflow.md'

# Task References
advancedElicitationTask: '{project-root}/.bmad/core/tasks/advanced-elicitation.xml'
partyModeWorkflow: '{project-root}/.bmad/core/workflows/party-mode/workflow.md'
---

# Step 2: Capture Discontinuation Reason

## STEP GOAL:

To capture a meaningful discontinuation reason for the audit trail before proceeding to confirmation.

## MANDATORY EXECUTION RULES (READ FIRST):

### Universal Rules:

- 🛑 NEVER generate content without user input
- 📖 CRITICAL: Read the complete step file before taking any action
- 🔄 CRITICAL: When loading next step with 'C', ensure entire file is read
- 📋 YOU ARE A FACILITATOR, not a content generator

### Role Reinforcement:

- ✅ You are a process management facilitator
- ✅ If you already have been given communication or persona patterns, continue to use those while playing this new role
- ✅ We engage in collaborative dialogue, not command-response
- ✅ You bring audit trail expertise, user brings discontinuation context
- ✅ Guide the user to provide a meaningful reason for the audit trail

### Step-Specific Rules:

- 🎯 Focus ONLY on capturing the discontinuation reason
- 🚫 FORBIDDEN to accept empty or meaningless reasons
- 💬 Provide examples to help user formulate reason
- 📋 Store reason in session variable `{discontinuation_reason}`

## EXECUTION PROTOCOLS:

- 🎯 Request reason with helpful examples
- 💾 Validate reason is not empty
- 📖 Store reason in session variable
- 🚫 FORBIDDEN to proceed without valid reason

## CONTEXT BOUNDARIES:

- Session variables from step 1 are available
- User has already acknowledged impact summary
- Focus ONLY on capturing the reason
- Do not execute any operations in this step

## SEQUENCE OF INSTRUCTIONS:

### 1. Request Discontinuation Reason

Ask the user:

---

**Please provide a reason for discontinuing this process:**

Examples:
- "Duplicate of P002 - consolidating documentation"
- "Process replaced by new automated workflow"
- "Project cancelled - no longer needed"
- "Created in error during testing"
- "Process merged into P005"

**Reason:**

---

### 2. Validate Reason

- Check that the provided reason is not empty
- If empty or just whitespace, ask again: "Please provide a reason for the audit trail. This helps track why processes were discontinued."
- Store valid reason as `{discontinuation_reason}`

### 3. Present MENU OPTIONS

Display: **Select an Option:** [C] Continue to confirmation | [E] Edit reason | [X] Cancel

#### EXECUTION RULES:

- ALWAYS halt and wait for user input after presenting menu
- ONLY proceed to next step when user selects 'C'
- If user selects 'E', return to step 1 of this file to re-capture reason
- If user selects 'X', exit workflow and return to agent menu
- User can ask questions - respond and then redisplay menu

#### Menu Handling Logic:

- IF C: Load, read entire file, then execute `{nextStepFile}`
- IF E: Return to [1. Request Discontinuation Reason](#1-request-discontinuation-reason)
- IF X: Display "❌ Operation cancelled. Returning to menu." and exit workflow
- IF Any other comments or queries: help user respond then redisplay menu options

## CRITICAL STEP COMPLETION NOTE

ONLY WHEN [C continue option] is selected and [valid non-empty reason captured and stored in session variable], will you then load and read fully `{nextStepFile}` to execute and begin confirmation step.

---

## 🚨 SYSTEM SUCCESS/FAILURE METRICS

### ✅ SUCCESS:

- Non-empty reason captured from user
- Reason stored in session variable
- User confirmed or edited reason
- Correct navigation to next step or exit

### ❌ SYSTEM FAILURE:

- Proceeding without a reason
- Accepting empty reason
- Not storing reason in session variable
- Skipping validation

**Master Rule:** Skipping steps, optimizing sequences, or not following exact instructions is FORBIDDEN and constitutes SYSTEM FAILURE.
