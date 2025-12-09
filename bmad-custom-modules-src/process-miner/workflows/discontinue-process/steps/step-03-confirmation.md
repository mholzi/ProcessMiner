---
name: 'step-03-confirmation'
description: 'Require explicit typed confirmation before executing discontinuation'

# Path Definitions
module_root: '{project-root}/bmad-custom-modules-src/process-miner'
workflow_path: '{module_root}/workflows/discontinue-process'

# File References
thisStepFile: '{workflow_path}/steps/step-03-confirmation.md'
nextStepFile: '{workflow_path}/steps/step-04-execute.md'
workflowFile: '{workflow_path}/workflow.md'

# Task References
advancedElicitationTask: '{project-root}/.bmad/core/tasks/advanced-elicitation.xml'
partyModeWorkflow: '{project-root}/.bmad/core/workflows/party-mode/workflow.md'
---

# Step 3: Explicit Confirmation

## STEP GOAL:

To require explicit typed confirmation ("DISCONTINUE") before executing the discontinuation operation. This is the final gate before irreversible actions.

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
- ✅ You bring safety checkpoint protocols, user brings final authorization
- ✅ This is FINAL confirmation - require exact "DISCONTINUE" (case-sensitive)

### Step-Specific Rules:

- 🎯 Focus ONLY on obtaining explicit confirmation
- 🚫 FORBIDDEN to proceed with anything other than exact "DISCONTINUE"
- 💬 Display clear confirmation summary
- 📋 Be strict about confirmation matching

## EXECUTION PROTOCOLS:

- 🎯 Display complete confirmation summary
- 💾 Require exact typed confirmation
- 📖 Only proceed if "DISCONTINUE" is typed exactly
- 🚫 Any other input cancels the operation

## CONTEXT BOUNDARIES:

- All session variables from previous steps are available
- `{discontinuation_reason}` is set from step 2
- This is the final checkpoint before execution
- No operations are performed in this step

## SEQUENCE OF INSTRUCTIONS:

### 1. Display Final Confirmation Summary

Present the complete confirmation request:

---

**CONFIRMATION REQUIRED**

You are about to discontinue:

| Field | Value |
|-------|-------|
| **Process** | {current_process_id} - {current_process_name} |
| **Reason** | {discontinuation_reason} |
| **By** | {contributor_name} ({contributor_role}) |
| **Date** | {date} |

This action will:
1. Move the process folder to `discontinued/`
2. Remove the process from the active registry
3. Add an entry to the Discontinued Processes section
4. Update the change log

---

### 2. Request Typed Confirmation

Ask:

---

Type **DISCONTINUE** (exactly, case-sensitive) to confirm, or **cancel** to abort:

---

### 3. Validate Confirmation

Check the user's response:

- **IF response is exactly "DISCONTINUE"**: Proceed to execution step
- **IF response is "cancel" or "abort" or "X"** (case-insensitive): Cancel the operation
- **IF response is anything else**: Inform user of typo and ask again

### 4. Handle Response

#### IF Confirmed (response == "DISCONTINUE"):

Display: "✅ Confirmation received. Proceeding with discontinuation..."

Then: Load, read entire file, then execute `{nextStepFile}`

#### IF Cancelled (response matches cancel/abort/X):

Display: "❌ Operation cancelled. Returning to menu."

Exit workflow and return to agent menu.

#### IF Typo or Other Input:

Display: "❌ Input was \"{user_input}\" - expected exactly \"DISCONTINUE\"."

Then return to [2. Request Typed Confirmation](#2-request-typed-confirmation) to ask again.

## CRITICAL STEP COMPLETION NOTE

ONLY WHEN [exact "DISCONTINUE" confirmation received], will you then load and read fully `{nextStepFile}` to execute and begin execution step. Typing "cancel", "abort", or "X" cancels the workflow. Any other input (typos) prompts the user to try again.

---

## 🚨 SYSTEM SUCCESS/FAILURE METRICS

### ✅ SUCCESS:

- Complete confirmation summary displayed
- Exact "DISCONTINUE" typed by user
- Correct routing based on confirmation
- Clear messaging for both confirm and cancel paths

### ❌ SYSTEM FAILURE:

- Proceeding without exact "DISCONTINUE" match
- Accepting partial or case-insensitive matches
- Not displaying complete confirmation summary
- Skipping this step entirely

**Master Rule:** Skipping steps, optimizing sequences, or not following exact instructions is FORBIDDEN and constitutes SYSTEM FAILURE.
