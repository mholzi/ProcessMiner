---
name: CX Journey Analysis
description: Interactive progressive elicitation workflow for capturing client experience journey, touchpoints, and friction points from SMEs. Requires existing AS-IS process documentation as a prerequisite. Produces CX-focused documentation with Client Effort Score (CES) analysis.
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

# Process context - set during initialization (required)
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

# Prerequisite files (MUST exist before workflow can proceed)
prerequisite_files:
  structured_data: "{current_process_folder}/structured-data.json"
  as_is_documentation: "{current_process_folder}/as-is-process-documentation.md"

# Workflow paths
installed_path: "{module_root}/workflows/cx-journey-analysis"
workflow_path: "{installed_path}"
steps_folder: "{workflow_path}/steps"
first_step: "{workflow_path}/steps/step-01-init.md"
continuation_step: "{workflow_path}/steps/step-00-continuation.md"

# Shared resources (module level)
shared_protocols: "{module_root}/workflows/shared/protocols"

# Validation checklist
validation: "{workflow_path}/validation-checklist.md"

# Output files (CX-focused)
output_files:
  cx_journey: "{current_process_folder}/cx-journey-documentation.md"
  friction_points: "{current_process_folder}/friction-points-detail.md"
  client_touchpoints: "{current_process_folder}/client-touchpoints-detail.md"

# Templates for document generation
templates:
  cx_journey: "{module_root}/templates/cx-journey-documentation.md"
  friction_points: "{module_root}/templates/friction-points-detail.md"
  client_touchpoints: "{module_root}/templates/client-touchpoints-detail.md"

standalone: false
---

# CX Journey Analysis

**Goal:** Capture the client experience perspective of an existing documented process through progressive elicitation, producing CX-focused documentation with touchpoints, friction points, and Client Effort Score (CES) analysis.

**Prerequisites:** This workflow REQUIRES existing AS-IS process documentation. The following files must exist:
- `structured-data.json` - Machine-readable process data
- `as-is-process-documentation.md` - Human-readable process documentation

**Your Role:** In addition to your name, communication_style, and persona, you are also a Client Journey Analyst collaborating with SMEs. This is a partnership. You bring expertise in client experience analysis and journey mapping, while the SME brings their knowledge of how clients actually experience the process.

---

## WORKFLOW ARCHITECTURE

This workflow uses **step-file architecture** for disciplined execution:

### Core Principles

- **Micro-file Design**: Each step is a self-contained instruction file that is part of an overall workflow that must be followed exactly
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

- **NEVER** load multiple step files simultaneously
- **ALWAYS** read entire step file before execution
- **NEVER** skip steps or optimize the sequence
- **ALWAYS** update frontmatter of output files when writing the final output for a specific step
- **ALWAYS** follow the exact instructions in the step file
- **ALWAYS** halt at menus and wait for user input
- **NEVER** create mental todo lists from future steps

---

## STEP OVERVIEW

| Step | File | Goal | Template Section |
|------|------|------|------------------|
| 0 | step-00-continuation.md | Handle session resumption | - |
| 1 | step-01-init.md | Process selection, prerequisite validation, session initialization | - |
| 2 | step-02-journey-overview.md | Journey identification, client persona, journey context | Section 1 |
| 3 | step-03-touchpoints.md | Identify and document client touchpoints with JT# IDs | Section 2 |
| 4 | step-04-friction.md | Capture friction points with FP# IDs and enhancement ideas | Sections 4 & 7 |
| 5 | step-05-moments.md | Identify moments that matter and CES analysis | Sections 3 & 5 |
| 6 | step-06-channels.md | Channel analysis and switching patterns | Section 6 |
| 7 | step-07-research.md | Industry research and benchmarks | Section 8 |
| 8 | step-08-validation.md | Final review, gap analysis, and document generation | Sections 9 & 10 |

## SCHEMA REFERENCE

This workflow produces output aligned with `cx-journey-documentation.schema.yaml`:

**ID Patterns** (Format: PREFIX-PROCESSABBREV-SEQ):
- Journey Touchpoints: `JT-{ABBREV}-###` (e.g., JT-ONB-001)
- Friction Points: `FP-{ABBREV}-###` (e.g., FP-ONB-001)
- Channels: `CH-{ABBREV}-###` (e.g., CH-ONB-001)
- Enhancement Ideas: `EI-{ABBREV}-###` (e.g., EI-ONB-001)

**Process Abbreviation**: Derived from process name (e.g., "Onboarding" → "ONB", "Credit Origination" → "CRO")

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

## PREREQUISITE VALIDATION

**CRITICAL:** Before proceeding past Step 1, the workflow MUST verify:

1. User has selected an existing process from the registry
2. `{current_process_folder}/structured-data.json` EXISTS and is readable
3. `{current_process_folder}/as-is-process-documentation.md` EXISTS and is readable

If prerequisites are not met, the workflow MUST:
- Display a clear error message
- Advise user to run Process Documentation Analyst first
- ABORT the workflow - do not proceed

---

## OUTPUT FILES

All outputs go to `{current_process_folder}/`:

| File | Purpose |
|------|---------|
| `cx-journey-documentation.md` | Main CX journey analysis with CES metrics |
| `friction-points-detail.md` | Comprehensive friction point analysis |
| `client-touchpoints-detail.md` | Detailed touchpoint analysis |

---

## DATA FLOW

This workflow READS from existing AS-IS documentation:
- Process steps (PS#) from structured-data.json
- Pain points (PP#) from structured-data.json and pain-points-detail.md
- Exceptions (EX#) from structured-data.json and exceptions-detail.md
- Controls (CP#) from structured-data.json and control-points-detail.md

This workflow PRODUCES new CX-focused data:
- Journey Touchpoints (JT#) - client interaction points
- Friction Points (FP#) - client experience friction
- Enhancement Ideas (EI#) - improvement opportunities
- Channel Analysis (CH#) - channel usage patterns
- Client Effort Score (CES) - quantified effort metrics

---

## CROSS-REFERENCE STRATEGY

All CX elements must be linked back to AS-IS elements:
- Each JT# touchpoint links to one or more PS# process steps
- Each FP# friction point links to JT# touchpoints AND may link to PP# pain points
- Enhancement ideas link to FP# friction points they address

This ensures traceability from client experience back to operational process.
