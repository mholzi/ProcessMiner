---
name: Discontinue Process
description: Safely archive a process by moving it to the discontinued folder and updating the registry. Captures discontinuation reason for audit trail. Reversible action - all documentation preserved.
web_bundle: false
---

# Discontinue Process

**Goal:** Safely archive a process by moving its folder to the discontinued directory and updating the process registry, while maintaining a complete audit trail.

**Your Role:** In addition to your name, communication_style, and persona, you are also a process management facilitator collaborating with a process owner. This is a partnership, not a client-vendor relationship. You bring systematic safety protocols and audit trail expertise, while the user brings process context and discontinuation authority. Work together as equals. Note: This is a DESTRUCTIVE operation requiring explicit confirmation.

---

## WORKFLOW ARCHITECTURE

This uses **step-file architecture** for disciplined execution:

### Core Principles

- **Micro-file Design**: Each step is a self contained instruction file that is a part of an overall workflow that must be followed exactly
- **Just-In-Time Loading**: Only the current step file is in memory - never load future step files until told to do so
- **Sequential Enforcement**: Sequence within the step files must be completed in order, no skipping or optimization allowed
- **State Tracking**: This is an action workflow - state is tracked through session variables
- **Confirmation Required**: This workflow requires explicit typed confirmation before executing

### Step Processing Rules

1. **READ COMPLETELY**: Always read the entire step file before taking any action
2. **FOLLOW SEQUENCE**: Execute all numbered sections in order, never deviate
3. **WAIT FOR INPUT**: If a menu is presented, halt and wait for user selection
4. **CHECK CONTINUATION**: If the step has a menu with Continue as an option, only proceed to next step when user selects 'C' (Continue)
5. **SAVE STATE**: Update session variables and track progress before loading next step
6. **LOAD NEXT**: When directed, load, read entire file, then execute the next step file

### Critical Rules (NO EXCEPTIONS)

- 🛑 **NEVER** load multiple step files simultaneously
- 📖 **ALWAYS** read entire step file before execution
- 🚫 **NEVER** skip steps or optimize the sequence
- 🎯 **ALWAYS** follow the exact instructions in the step file
- ⏸️ **ALWAYS** halt at menus and wait for user input
- 📋 **NEVER** create mental todo lists from future steps
- ⚠️ **NEVER** execute file operations without explicit "DISCONTINUE" confirmation

---

## WORKFLOW TYPE

**Action Workflow** - Performs file system operations and registry updates. Does not produce a document output.

---

## SESSION VARIABLES

These variables are set by:
- **Agent activation:** `contributor_name`, `contributor_role`
- **select-existing-process workflow:** `current_process_id`, `current_process_name`, `current_process_folder`

| Variable | Source | Description |
|----------|--------|-------------|
| `current_process_id` | select-existing-process | Process ID (e.g., P001) |
| `current_process_name` | select-existing-process | Process name |
| `current_process_folder` | select-existing-process | Full path to process folder |
| `contributor_name` | Agent activation | Name of person performing action |
| `contributor_role` | Agent activation | Role of contributor |

---

## INITIALIZATION SEQUENCE

### 1. Configuration Loading

Load and read full config from `{module_root}/config.yaml` and resolve:

- `output_folder`, `user_name`, `communication_language`

Set path variables:
- `module_root`: `{project-root}/bmad-custom-modules-src/process-miner`
- `select_process_workflow`: `{module_root}/workflows/shared/select-existing-process/workflow.md`

### 2. Derived Variables

Calculate these from config:

- `discontinued_folder`: `{output_folder}/discontinued`
- `process_registry`: `{output_folder}/process-registry.md`

### 3. Process Selection (Shared Workflow)

Load, read and execute `{select_process_workflow}` to:
- Check registry for active processes
- Present numbered list for user selection
- Set session variables: `current_process_id`, `current_process_name`, `current_process_folder`

Note: `contributor_name` and `contributor_role` are already set by agent activation.

### 4. First Step EXECUTION

After process is selected, load, read the full file and then execute `{workflow_path}/steps/step-01-impact-summary.md` to begin the discontinuation process.
