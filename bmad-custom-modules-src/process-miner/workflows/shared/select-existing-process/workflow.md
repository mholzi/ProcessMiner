---
name: Select Existing Process
description: Allows secondary agents (CX Analyst, etc.) to select from existing documented processes and load their context for analysis.
web_bundle: false

# Configuration source - process-miner module
config_source: "{module_root}/config.yaml"

# Variables resolved from config
output_folder: "{config_source}:output_folder"
user_name: "{config_source}:user_name"
communication_language: "{config_source}:communication_language"
document_output_language: "{config_source}:document_output_language"

# Module path and workflow files
module_root: "{project-root}/bmad-custom-modules-src/process-miner"
installed_path: "{module_root}/workflows/shared/select-existing-process"
workflow_path: "{installed_path}"

# Step file references
step_01: "{workflow_path}/steps/step-01-init.md"
step_02: "{workflow_path}/steps/step-02-process-selection.md"
step_03: "{workflow_path}/steps/step-03-load-context.md"

# Registry location
process_registry: "{output_folder}/process-registry.md"

template: false
standalone: false
---

# Select Existing Process

**Goal:** Allow secondary agents (Client Journey Analyst, etc.) to select from existing documented processes and load their context for analysis. This is NOT for creating new processes - that's what `start-new-process` is for.

**Your Role:** In addition to your name, communication_style, and persona, you are helping the user select an existing process to analyze. You bring systematic process selection, while the user brings their analysis goals. Work together as equals.

---

## USE CASE

This workflow is for **secondary agents** that analyze existing processes:
- Client Journey Analyst (CX analysis)
- Other future analysts

These agents should NOT create new processes - they analyze processes already documented by the Process Documentation Analyst.

---

## WORKFLOW ARCHITECTURE

This uses **step-file architecture** for disciplined execution:

### Core Principles

- **Micro-file Design**: Each step is a self contained instruction file
- **Just-In-Time Loading**: Only the current step file is in memory
- **Sequential Enforcement**: Steps must be completed in order
- **Session Variables**: Track contributor and selected process

### Step Processing Rules

1. **READ COMPLETELY**: Always read the entire step file before taking any action
2. **FOLLOW SEQUENCE**: Execute all numbered sections in order, never deviate
3. **WAIT FOR INPUT**: If a menu is presented, halt and wait for user selection
4. **LOAD NEXT**: When directed, load, read entire file, then execute the next step file

### Critical Rules (NO EXCEPTIONS)

- **NEVER** load multiple step files simultaneously
- **ALWAYS** read entire step file before execution
- **NEVER** skip steps or optimize the sequence
- **ALWAYS** halt at menus and wait for user input

---

## STEP OVERVIEW

| Step | File | Goal |
|------|------|------|
| 1 | step-01-init.md | Capture contributor info and verify processes exist |
| 2 | step-02-process-selection.md | Allow user to select which process to analyze |
| 3 | step-03-load-context.md | Load process context and return control to agent |

---

## INITIALIZATION SEQUENCE

### 1. Configuration Loading

Load and read full config from `{config_source}` and resolve:

- `output_folder`, `user_name`, `communication_language`, `document_output_language`

### 2. First Step EXECUTION

Load, read the full file and then execute `{workflow_path}/steps/step-01-init.md` to begin the workflow.
