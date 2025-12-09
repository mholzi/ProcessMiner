---
name: 'step-02-process-selection'
description: 'Allow user to select which documented process to analyze'

# Path Definitions
module_root: '{project-root}/bmad-custom-modules-src/process-miner'
workflow_path: '{module_root}/workflows/shared/select-existing-process'

# File References
thisStepFile: '{workflow_path}/steps/step-02-process-selection.md'
nextStepFile: '{workflow_path}/steps/step-03-load-context.md'
workflowFile: '{workflow_path}/workflow.md'
---

# Step 2: Process Selection

## STEP GOAL:

Allow the user to select which documented process they want to analyze.

## MANDATORY EXECUTION RULES (READ FIRST):

### Universal Rules:

- NEVER assume which process the user wants
- CRITICAL: Read the complete step file before taking any action
- CRITICAL: When loading next step, ensure entire file is read
- YOU ARE A FACILITATOR, not a content generator

### Role Reinforcement:

- You are maintaining your agent persona
- If you already have been given communication or persona patterns, continue to use those
- We engage in collaborative dialogue, not command-response
- Present clear options, let user decide

### Step-Specific Rules:

- Focus ONLY on process selection
- FORBIDDEN to analyze process content in this step
- Present numbered list for easy selection
- WAIT for user input before proceeding

## EXECUTION PROTOCOLS:

- Display numbered list of available processes
- Capture user selection
- Set session variables for selected process
- Do NOT proceed without valid selection

## Sequence of Instructions

### 1. Display Process Selection Menu

**If only ONE process available:**

Display:
```
Found 1 documented process:

[1] {process_id} - {process_name}

Press Enter or type 1 to select this process:
```

**If MULTIPLE processes available:**

Display:
```
Select a process to analyze:

[1] {process_id_1} - {process_name_1}
[2] {process_id_2} - {process_name_2}
...
[N] {process_id_N} - {process_name_N}

Enter the number of the process you want to analyze:
```

### 2. Wait for User Input

**HALT and WAIT** for user to enter their selection.

### 3. Validate Selection

**If invalid input (not a valid number):**
```
Please enter a valid number from the list above.
```
Return to step 1 and redisplay the menu.

**If valid selection:**
Proceed to set session variables.

### 4. Set Process Session Variables

Upon valid selection, set these session variables:

- `{current_process_id}` = Selected process ID (e.g., P004)
- `{current_process_name}` = Selected process name (e.g., "Onboarding of Corporate Clients")
- `{current_process_folder}` = `{output_folder}/processes/{current_process_id} - {current_process_name}`

**IMPORTANT:** The folder naming convention is `processes/{ID} - {Name}`.

Display confirmation:
```
Selected: {current_process_name} ({current_process_id})

Loading process context...
```

### 5. Load Next Step

Load, read entire file, then execute `{nextStepFile}` (step-03-load-context.md)

Pass the following session context:
- `{contributor_name}`
- `{contributor_role}`
- `{current_process_id}`
- `{current_process_name}`
- `{current_process_folder}`

---

## SYSTEM SUCCESS/FAILURE METRICS

### SUCCESS:

- Available processes displayed in numbered list
- User process selection captured correctly
- All session variables set correctly
- Process folder path constructed correctly

### SYSTEM FAILURE:

- Not waiting for user input
- Accepting invalid selection
- Incorrect session variable values
- Proceeding without confirmed selection

**Master Rule:** Always WAIT for user input after displaying each selection menu. Never assume or auto-select.
