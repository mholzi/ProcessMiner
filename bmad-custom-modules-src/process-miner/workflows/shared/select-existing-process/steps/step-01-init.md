---
name: 'step-01-init'
description: 'Capture contributor info and verify documented processes exist'

# Path Definitions
module_root: '{project-root}/bmad-custom-modules-src/process-miner'
workflow_path: '{module_root}/workflows/shared/select-existing-process'

# File References
thisStepFile: '{workflow_path}/steps/step-01-init.md'
nextStepFile: '{workflow_path}/steps/step-02-process-selection.md'
workflowFile: '{workflow_path}/workflow.md'

# Output folder for process registry
output_folder: '{config_source}:output_folder'
process_registry: '{output_folder}/process-registry.md'
---

# Step 1: Initialization

## STEP GOAL:

Verify that documented processes exist for selection. Contributor info (`contributor_name`, `contributor_role`) is already captured during agent activation.

## MANDATORY EXECUTION RULES (READ FIRST):

### Universal Rules:

- CRITICAL: Read the complete step file before taking any action
- CRITICAL: When loading next step, ensure entire file is read
- YOU ARE A FACILITATOR, not a content generator
- IMPORTANT: `contributor_name` and `contributor_role` are already set by agent activation - DO NOT ask again

### Role Reinforcement:

- You are maintaining your agent persona (Client Journey Analyst, etc.)
- If you already have been given communication or persona patterns, continue to use those
- We engage in collaborative dialogue, not command-response

### Step-Specific Rules:

- Focus ONLY on registry check
- FORBIDDEN to start any analysis in this step
- If no processes exist, explain and exit gracefully
- DO NOT ask for name or role - use existing session variables

## EXECUTION PROTOCOLS:

- Greet user by name (using {contributor_name} from session)
- Verify process registry has documented processes
- Report findings and proceed

## Sequence of Instructions

### 1. Greet Contributor

Display greeting using your agent persona and the contributor's name from session:

```
Alright {contributor_name}, let me check what processes are available for analysis...
```

### 2. Check Process Registry

Scan `{output_folder}/processes/` directory for existing process folders.

**Process folder naming convention:** `{ID} - {Name}` (e.g., `P001 - Onboarding of Corporate Clients`)

**If NO process folders found:**

Display:
```
No documented processes found yet.

Before I can analyze client experience, we need existing process documentation.
Please run the **Process Documentation Analyst** first to document your AS-IS process.

[Return to menu]
```

**EXIT workflow gracefully.**

**If process folders found:**

Build list of available processes:
- Extract process ID and name from folder names
- Store as `{available_processes}` list

Display:
```
Found {count} documented process(es) ready for analysis.
```

### 3. Load Next Step

Load, read entire file, then execute `{nextStepFile}` (step-02-process-selection.md)

Pass session context:
- `{contributor_name}` (from agent activation)
- `{contributor_role}` (from agent activation)
- `{available_processes}`

---

## SYSTEM SUCCESS/FAILURE METRICS

### SUCCESS:

- Used contributor_name from agent session (not asked again)
- Process registry scanned correctly
- Available processes identified (or graceful exit if none)
- Session variables passed correctly

### SYSTEM FAILURE:

- Asked for contributor name or role (already captured by agent)
- Proceeding without checking for existing processes
- Not exiting gracefully when no processes exist

**Master Rule:** contributor_name and contributor_role are ALREADY SET by agent activation. DO NOT ask for them again.
