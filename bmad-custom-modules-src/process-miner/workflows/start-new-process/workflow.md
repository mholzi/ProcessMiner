---
name: Start New Process
description: Interactive progressive elicitation workflow for extracting banking process knowledge from SMEs using adaptive questioning techniques. Captures structured data (process steps, pain points, controls, systems) with configurable approval patterns.
web_bundle: true

# Module root path
module_root: "{project-root}/bmad-custom-modules-src/process-miner"

# Configuration source - process-miner module
config_source: "{module_root}/config.yaml"

# Variables resolved from config
output_folder: "{config_source}:output_folder"
user_name: "{config_source}:user_name"
communication_language: "{config_source}:communication_language"
document_output_language: "{config_source}:document_output_language"

# Process Registry
processes_folder: "{project-root}/docs/processes"
process_registry_file: "{processes_folder}/process-registry.md"
process_registry_template: "{module_root}/templates/process-registry.md"

# Process context - set by agent activation (required)
# Folder pattern: {processes_folder}/{###}-{process-name-kebab-case}
# Example: docs/processes/001-onboarding
current_process_folder: session-variable
current_process_id: session-variable
current_process_name: session-variable

# Contributor tracking - set by agent activation
contributor_name: session-variable
contributor_role: session-variable

# Continuation support
start_at_step: session-variable

# Calling agent identification (passed from menu item)
# Used to determine workflow behavior:
# - process-documentation-analyst: Can create NEW processes
# - All other agents: Must select EXISTING process with AS-IS documentation
calling_agent_id: session-variable

# Agent-provided template override (optional - passed from menu item)
# If set, uses agent-specific template instead of default
agent_template: session-variable
agent_output_file: session-variable

# Workflow paths
installed_path: "{module_root}/workflows/start-new-process"
workflow_path: "{installed_path}"
steps_folder: "{workflow_path}/steps"
first_step: "{workflow_path}/steps/step-01-init.md"
continuation_step: "{workflow_path}/steps/step-00-continuation.md"

# Shared resources (module level)
shared_protocols: "{module_root}/workflows/shared/protocols"

# Validation checklist
validation: "{workflow_path}/validation-checklist.md"

# Output configuration
output_file: "{current_process_folder}/structured-data.json"
schema_version: "1.0.0"

# Output files
output_files:
  structured_data: "{current_process_folder}/structured-data.json"
  main_document: "{current_process_folder}/as-is-process-documentation.md"
  exceptions_detail: "{current_process_folder}/exceptions-detail.md"
  pain_points_detail: "{current_process_folder}/pain-points-detail.md"
  control_points_detail: "{current_process_folder}/control-points-detail.md"

# Templates for document generation
templates:
  process: "{module_root}/templates/as-is-process-documentation.md"
  exceptions: "{module_root}/templates/exceptions-detail.md"
  pain_points: "{module_root}/templates/pain-points-detail.md"
  control_points: "{module_root}/templates/control-points-detail.md"

standalone: false
---

# Start New Process

**Goal:** Extract tacit process knowledge from SMEs through progressive elicitation, producing structured documentation with full traceability.

**Your Role:** In addition to your name, communication_style, and persona, you are also a Process Documentation Analyst collaborating with SMEs. This is a partnership, not a client-vendor relationship. You bring expertise in knowledge extraction and structured documentation, while the SME brings their domain knowledge and process experience. Work together as equals.

---

## WORKFLOW ARCHITECTURE

This workflow uses **step-file architecture** for disciplined execution:

### Core Principles

- **Micro-file Design**: Each step is a self contained instruction file that is a part of an overall workflow that must be followed exactly
- **Just-In-Time Loading**: Only the current step file is in memory - never load future step files until told to do so
- **Sequential Enforcement**: Sequence within the step files must be completed in order, no skipping or optimization allowed
- **State Tracking**: Document progress in output file frontmatter using `stepsCompleted` array when a workflow produces a document
- **Append-Only Building**: Build documents by appending content as directed to the output file

### Step Processing Rules

1. **READ COMPLETELY**: Always read the entire step file before taking any action
2. **FOLLOW SEQUENCE**: Execute all numbered sections in order, never deviate
3. **WAIT FOR INPUT**: If a menu is presented, halt and wait for user selection
4. **CHECK CONTINUATION**: If the step has a menu with Continue as an option, only proceed to next step when user selects 'C' (Continue)
5. **SAVE STATE**: Update `stepsCompleted` in frontmatter before loading next step
6. **LOAD NEXT**: When directed, load, read entire file, then execute the next step file

### Critical Rules (NO EXCEPTIONS)

- 🛑 **NEVER** load multiple step files simultaneously
- 📖 **ALWAYS** read entire step file before execution
- 🚫 **NEVER** skip steps or optimize the sequence
- 💾 **ALWAYS** update frontmatter of output files when writing the final output for a specific step
- 🎯 **ALWAYS** follow the exact instructions in the step file
- ⏸️ **ALWAYS** halt at menus and wait for user input
- 📋 **NEVER** create mental todo lists from future steps

---

## STEP OVERVIEW

| Step | File | Goal |
|------|------|------|
| 0 | step-00-continuation.md | Handle session resumption |
| 1 | step-01-init.md | Session initialization & context gathering |
| 2 | step-02-import.md | Check for existing documentation |
| 3 | step-03-overview.md | High-level process overview (purpose, trigger, frequency, volume) |
| 4 | step-04-process-steps.md | Identify and document process steps with PS# IDs |
| 5 | step-05-exceptions.md | Capture exceptions and variations with EX# IDs |
| 6 | step-06-pain-points.md | Identify pain points with PP# IDs |
| 7 | step-07-controls.md | Document controls and compliance with CP# IDs |
| 8 | step-08-systems.md | Catalog systems and tools with SYS# IDs |
| 9 | step-09-validation.md | Final review and completeness check |

---

## INITIALIZATION SEQUENCE

### 1. Configuration Loading

Load and read full config from `{config_source}` and resolve:

- `output_folder`, `user_name`, `communication_language`, `document_output_language`

### 2. Check for Continuation

If `start_at_step` session variable is set (from *continue-session command):
- Load `{continuation_step}`
- Execute continuation logic

### 3. Fresh Start Execution

If no continuation:
- Load, read the full file, and execute `{first_step}` to begin the workflow.

---

## OUTPUT FILES

All outputs go to `{current_process_folder}/`:

| File | Purpose |
|------|---------|
| `structured-data.json` | Machine-readable data for downstream agents |
| `as-is-process-documentation.md` | Main human-readable documentation |
| `exceptions-detail.md` | Comprehensive exception analysis |
| `pain-points-detail.md` | Comprehensive pain point analysis |
| `control-points-detail.md` | Comprehensive control analysis |
