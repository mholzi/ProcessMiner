---
name: Continue Session
description: Universal session resume workflow that analyzes existing documentation to determine where the user left off and routes to the correct step in the appropriate workflow. Supports multiple agents and their primary workflows.
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
installed_path: "{module_root}/workflows/shared/continue-session"
workflow_path: "{installed_path}"

# Process selection - use shared workflow
select_process_workflow: "{module_root}/workflows/shared/select-existing-process/workflow.md"

# Step file references (routing only - selection handled by shared workflow)
step_route: "{workflow_path}/steps/step-03-route.md"

# Registry location
process_registry: "{output_folder}/process-registry.md"

# Calling agent identification (passed from menu item)
# Used to determine which workflow to route to
calling_agent_id: session-variable

# Target workflows by agent (resolved in step-03-route)
workflows:
  process-documentation-analyst:
    workflow: "{module_root}/workflows/start-new-process/workflow.md"
    output_file: "structured-data.json"
    steps: 9
    type: "process-documentation"
  innovation-analyst:
    workflow: "{module_root}/workflows/innovation-analysis/workflow.md"
    output_file: "innovation-analysis.md"
    steps: 5
    type: "innovation-analysis"
  client-journey-analyst:
    workflow: "{module_root}/workflows/cx-journey-analysis/workflow.md"
    output_file: "cx-journey-documentation.md"
    steps: 8
    type: "cx-journey"
  control-analyst:
    workflow: "{module_root}/workflows/control-compliance-analysis/workflow.md"
    output_file: "compliance-control-assessment.md"
    steps: 10
    type: "control-compliance"
  # Future validation workflows (not yet implemented)
  # innovation-analyst-validation:
  #   workflow: "{module_root}/workflows/innovation-target-validation/workflow.md"
  #   output_file: "innovation-target-validation.md"
  #   steps: TBD
  #   type: "innovation-validation"
  # client-journey-analyst-validation:
  #   workflow: "{module_root}/workflows/cx-target-validation/workflow.md"
  #   output_file: "cx-target-validation.md"
  #   steps: TBD
  #   type: "cx-validation"

template: false
standalone: false
---

# Continue Session

**Goal:** Universal session resume workflow that analyzes existing documentation to determine where the user left off and routes to the correct step in the appropriate workflow. Supports multiple agents and their primary workflows.

**Your Role:** In addition to your name, communication_style, and persona, you are also a session continuity specialist collaborating with a process contributor. This is a partnership, not a client-vendor relationship. You bring systematic analysis of documentation state and intelligent routing, while the user brings their process knowledge and continuation goals. Work together as equals.

---

## SUPPORTED WORKFLOWS

| Agent | Workflow | Type | Steps | Output File |
|-------|----------|------|-------|-------------|
| Process Documentation Analyst | start-new-process | process-documentation | 9 | structured-data.json |
| Innovation Analyst | innovation-analysis | innovation-analysis | 5 | innovation-analysis.md |
| Client Journey Analyst | cx-journey-analysis | cx-journey | 8 | cx-journey-documentation.md |
| Control Analyst | control-compliance-analysis | control-compliance | 10 | compliance-control-assessment.md |

**Future (not yet implemented):**
| Agent | Workflow | Type | Steps | Output File |
|-------|----------|------|-------|-------------|
| Innovation Analyst | innovation-target-validation | innovation-validation | TBD | innovation-target-validation.md |
| Client Journey Analyst | cx-target-validation | cx-validation | TBD | cx-target-validation.md |

---

## WORKFLOW ARCHITECTURE

This workflow uses the **shared process selection workflow** for process selection, then performs routing to the correct step in the target workflow based on the calling agent.

### Core Principles

- **Agent-Aware Routing**: Uses `calling_agent_id` from menu item to determine target workflow
- **Shared Selection**: Uses `select-existing-process` workflow for process selection (no duplication)
- **Routing Logic**: After selection, analyzes progress and routes to appropriate workflow step
- **State Tracking**: This is an action/routing workflow - no output document is produced
- **Session Variables**: Track selected process and routing information

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
| 2 | `step-03-route.md` | Analyze progress and route to appropriate workflow step |

---

## INITIALIZATION SEQUENCE

### 1. Configuration Loading

Load and read full config from `{config_source}` and resolve:

- `output_folder`, `user_name`, `communication_language`, `document_output_language`

### 2. Identify Calling Agent

The `calling_agent_id` session variable identifies which agent invoked this workflow:
- `process-documentation-analyst` → routes to `start-new-process`
- `innovation-analyst` → routes to `innovation-analysis`
- `client-journey-analyst` → routes to `cx-journey-analysis`
- `control-analyst` → routes to `control-compliance-analysis`

**If calling_agent_id is not set:** Display error and return to agent menu.

### 3. Process Selection (Shared Workflow)

Load, read and execute `{select_process_workflow}` to:
- Check registry for active processes
- Present numbered list for user selection
- Set session variables: `current_process_id`, `current_process_name`, `current_process_folder`

Note: `contributor_name` and `contributor_role` are already set by agent activation.

### 4. Routing Step

After process is selected, load, read and execute `{step_route}` to analyze progress and route to the appropriate step in the target workflow.
