---
name: 'step-04-execute'
description: 'Execute the discontinuation - move folder and update registry'

# Path Definitions
module_root: '{project-root}/bmad-custom-modules-src/process-miner'
workflow_path: '{module_root}/workflows/discontinue-process'

# File References
thisStepFile: '{workflow_path}/steps/step-04-execute.md'
nextStepFile: '{workflow_path}/steps/step-05-complete.md'
workflowFile: '{workflow_path}/workflow.md'

# Registry and Folders
process_registry: '{output_folder}/process-registry.md'
discontinued_folder: '{output_folder}/discontinued'

# Task References
advancedElicitationTask: '{project-root}/.bmad/core/tasks/advanced-elicitation.xml'
partyModeWorkflow: '{project-root}/.bmad/core/workflows/party-mode/workflow.md'
---

# Step 4: Execute Discontinuation

## STEP GOAL:

To execute the discontinuation by moving the process folder and updating the process registry.

## MANDATORY EXECUTION RULES (READ FIRST):

### Universal Rules:

- 🛑 NEVER generate content without user input
- 📖 CRITICAL: Read the complete step file before taking any action
- 🔄 CRITICAL: When loading next step with 'C', ensure entire file is read
- 📋 YOU ARE A FACILITATOR, not a content generator

### Role Reinforcement:

- ✅ You are a process management facilitator executing confirmed operations
- ✅ If you already have been given communication or persona patterns, continue to use those while playing this new role
- ✅ We engage in collaborative dialogue, not command-response
- ✅ You bring systematic execution protocols, user has already authorized
- ✅ Follow exact sequence - folder first, then registry; report progress

### Step-Specific Rules:

- 🎯 Execute operations in exact order specified
- 🚫 FORBIDDEN to skip any operation
- 💬 Report progress after each major operation
- 📋 Handle errors and report to user

## EXECUTION PROTOCOLS:

- 🎯 Execute folder move operation
- 💾 Update process registry file
- 📖 Report progress after each step
- 🚫 FORBIDDEN to skip registry update

## CONTEXT BOUNDARIES:

- User has typed "DISCONTINUE" in step 3
- All session variables are available
- This step performs actual file operations
- Errors should be reported and handled

## SEQUENCE OF INSTRUCTIONS:

### 1. Create Discontinued Folder (If Needed)

Check if `{discontinued_folder}` exists:
- If NOT exists: Create the directory
- Report: "📁 Created discontinued folder: `{discontinued_folder}`"

### 2. Move Process Folder

Move the process folder:
- FROM: `{output_folder}/{current_process_id} - {current_process_name}/`
- TO: `{discontinued_folder}/{current_process_id} - {current_process_name}/`

Report: "📁 Moved process folder to discontinued/"

**Error Handling:**
- If source folder doesn't exist: Report error and exit
- If destination already exists: Report error and exit
- If move fails: Report error and exit

### 3. Update Process Registry

Read and update `{process_registry}`:

#### 3.1 Remove from Active Processes

Find and remove the entry from `## Processes` section:
```
- **{current_process_id}** - {current_process_name}
  {description}
```

#### 3.2 Add/Update Discontinued Processes Section

If `## Discontinued Processes` section doesn't exist, create it after `## Processes`:

```markdown
---

## Discontinued Processes

Archived processes no longer active in the workflow.

```

Add entry to the section:

```markdown
- **{current_process_id}** - {current_process_name}
  Discontinued: {date} by {contributor_name}
  Reason: {discontinuation_reason}
```

#### 3.3 Update Registry Information

- Update "Last Updated" date to `{date}`
- Decrement "Total Processes" count by 1 (active processes only)

#### 3.4 Append to Change Log

If `## Change Log` section doesn't exist, create it at end of document:

```markdown
---

## Change Log

| Date | Contributor | Role | Changes |
|------|-------------|------|---------|
```

Append new row at TOP of table (most recent first):

```markdown
| {date} | {contributor_name} | {contributor_role} | Discontinued {current_process_id} - {current_process_name} (Reason: {discontinuation_reason}) |
```

#### 3.5 Save Registry

Save the updated registry file.

Report: "📋 Updated process registry"

### 4. Proceed to Completion

Display: "✅ Discontinuation executed successfully."

Then: Load, read entire file, then execute `{nextStepFile}`

## CRITICAL STEP COMPLETION NOTE

ONLY WHEN [all file operations completed successfully - folder moved, registry updated, change log appended], will you then load and read fully `{nextStepFile}` to execute and begin completion step.

---

## 🚨 SYSTEM SUCCESS/FAILURE METRICS

### ✅ SUCCESS:

- Discontinued folder exists or was created
- Process folder moved successfully
- Process entry removed from active section
- Discontinued section created/updated
- Registry information updated
- Change log entry added
- Progress reported to user

### ❌ SYSTEM FAILURE:

- File operations executed without confirmation
- Folder move failed silently
- Registry not updated after folder move
- Missing change log entry
- Missing discontinued section entry
- Skipping any operation

**Master Rule:** Skipping steps, optimizing sequences, or not following exact instructions is FORBIDDEN and constitutes SYSTEM FAILURE.
