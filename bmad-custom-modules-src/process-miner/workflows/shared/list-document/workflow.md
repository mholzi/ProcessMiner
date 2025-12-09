---
name: List Documents
description: List all documents in a selected process's source-documentation folder with descriptions and links.
web_bundle: true

# Module path
module_root: "{project-root}/bmad-custom-modules-src/process-miner"

# Configuration source - module config
config_source: "{module_root}/config.yaml"

# Variables resolved from config
output_folder: "{config_source}:output_folder"
user_name: "{config_source}:user_name"
communication_language: "{config_source}:communication_language"
installed_path: "{module_root}/workflows/shared/list-document"
workflow_path: "{installed_path}"

# Process selection - use shared workflow
select_process_workflow: "{module_root}/workflows/shared/select-existing-process/workflow.md"

# Step file references (listing only - selection handled by shared workflow)
step_list: "{workflow_path}/steps/step-03-list-documents.md"

# Registry location
process_registry: "{output_folder}/process-registry.md"

template: false
standalone: false
---

# List Documents

**Goal:** Display all documents in a selected process's source-documentation folder with AI-generated descriptions and clickable links.

**Your Role:** In addition to your name, communication_style, and persona, you are also a session utility specialist helping a process contributor quickly view their uploaded documents. This is a simple lookup action - be brief, helpful, and get to the results quickly.

---

## WORKFLOW ARCHITECTURE

This workflow uses the **shared process selection workflow** for process selection, then lists documents.

### Core Principles

- **Shared Selection**: Uses `select-existing-process` workflow for process selection (no duplication)
- **Simple Action**: After selection, lists documents in the process folder
- **State Tracking**: This is an action/display workflow - no output document is produced

### Step Processing Rules

1. **READ COMPLETELY**: Always read the entire step file before taking any action
2. **FOLLOW SEQUENCE**: Execute all numbered sections in order, never deviate
3. **WAIT FOR INPUT**: If a menu is presented, halt and wait for user selection
4. **LOAD NEXT**: When directed, load, read entire file, then execute the next step file

### Critical Rules (NO EXCEPTIONS)

- **NEVER** load multiple step files simultaneously
- **ALWAYS** read entire step file before execution
- **NEVER** skip steps or optimize the sequence
- **ALWAYS** follow the exact instructions in the step file
- **ALWAYS** halt at menus and wait for user input

---

## WORKFLOW FLOW

| Phase | Workflow/Step | Goal |
|-------|---------------|------|
| 1 | `select-existing-process` workflow | Select process from registry (shared) |
| 2 | `step-03-list-documents.md` | Scan folder, read content, display cards with descriptions |

---

## INITIALIZATION SEQUENCE

### 1. Configuration Loading

Load and read full config from `{config_source}` and resolve:

- `output_folder`, `user_name`, `communication_language`

### 2. Process Selection (Shared Workflow)

Load, read and execute `{select_process_workflow}` to:
- Check registry for active processes
- Present numbered list for user selection
- Set session variables: `current_process_id`, `current_process_name`, `current_process_folder`

Note: `contributor_name` and `contributor_role` are already set by agent activation.

### 3. List Documents

After process is selected, load, read and execute `{step_list}` to scan and display documents.
