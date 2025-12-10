---
name: Control & Compliance Analysis
description: Interactive progressive elicitation workflow for capturing regulatory compliance, control points, and risk assessment from SMEs. Requires existing AS-IS process documentation as a prerequisite. Produces comprehensive compliance assessment with control effectiveness analysis.
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
current_process_folder: session-variable
current_process_id: session-variable
current_process_name: session-variable
process_abbreviation: session-variable

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
installed_path: "{module_root}/workflows/control-compliance-analysis"
workflow_path: "{installed_path}"
steps_folder: "{workflow_path}/steps"
first_step: "{workflow_path}/steps/step-01-init.md"
continuation_step: "{workflow_path}/steps/step-00-continuation.md"

# Shared resources (module level)
shared_protocols: "{module_root}/workflows/shared/protocols"

# Schema references
schemas:
  compliance_assessment: "{module_root}/templates/compliance-control-assessment.schema.yaml"
  control_points_detail: "{module_root}/templates/control-points-detail.schema.yaml"

# Output files
output_files:
  compliance_assessment: "{current_process_folder}/compliance-control-assessment.md"
  control_points_detail: "{current_process_folder}/control-points-detail.md"

# Templates for document generation
templates:
  compliance_assessment: "{module_root}/templates/compliance-control-assessment.md"
  control_points_detail: "{module_root}/templates/control-points-detail.md"

standalone: false
---

# Control & Compliance Analysis

**Goal:** Capture regulatory compliance requirements, control points, and risk assessment through progressive elicitation, producing comprehensive compliance documentation with control effectiveness analysis.

**Prerequisites:** This workflow REQUIRES existing AS-IS process documentation. The following files must exist:
- `structured-data.json` - Machine-readable process data
- `as-is-process-documentation.md` - Human-readable process documentation

**Your Role:** In addition to your name, communication_style, and persona, you are also a Control Analyst collaborating with SMEs. This is a partnership. You bring expertise in regulatory compliance and control frameworks, while the SME brings their knowledge of the process and its controls.

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
| 2 | step-02-regulatory-framework.md | Regulatory framework mapping - applicable regulations | Section 1 |
| 3 | step-03-control-inventory.md | Control point inventory - catalog all controls | Section 2 |
| 4 | step-04-compliance-gaps.md | Compliance gap analysis - current vs required | Section 3 |
| 5 | step-05-effectiveness.md | Control effectiveness assessment | Section 4 |
| 6 | step-06-audit-trail.md | Audit trail requirements | Section 5 |
| 7 | step-07-risk-matrix.md | Risk & compliance matrix | Section 6 |
| 8 | step-08-regulatory-change.md | Regulatory change impact assessment | Section 7 |
| 9 | step-09-audit-findings.md | Open audit findings capture | Section 8 |
| 10 | step-10-recommendations.md | Control improvement recommendations | Section 9 |
| 11 | step-11-validation.md | Final review, gap analysis, and document generation | - |

## SCHEMA REFERENCE

This workflow produces output aligned with:
- `compliance-control-assessment.schema.yaml`
- `control-points-detail.schema.yaml`

**ID Patterns** (Format: PREFIX-PROCESSABBREV-SEQ):
- Regulations: `REG-{ABBREV}-###` (e.g., REG-ONB-001)
- Control Points: `CP-{ABBREV}-###` (e.g., CP-ONB-001)
- Compliance Gaps: `GAP-{ABBREV}-###` (e.g., GAP-ONB-001)
- Control Effectiveness: `CEA-{ABBREV}-###` (e.g., CEA-ONB-001)
- Audit Trail Requirements: `ATR-{ABBREV}-###` (e.g., ATR-ONB-001)
- Risk & Compliance Matrix: `RCM-{ABBREV}-###` (e.g., RCM-ONB-001)
- Regulatory Change Impact: `RCI-{ABBREV}-###` (e.g., RCI-ONB-001)
- Open Audit Findings: `OAF-{ABBREV}-###` (e.g., OAF-ONB-001)
- Control Improvement Recommendations: `CIR-{ABBREV}-###` (e.g., CIR-ONB-001)

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
| `compliance-control-assessment.md` | Main compliance assessment with regulatory mapping |
| `control-points-detail.md` | Detailed control point analysis |

---

## DATA FLOW

This workflow READS from existing AS-IS documentation:
- Process steps (PS#) from structured-data.json
- Pain points (PP#) from structured-data.json
- Exceptions (EX#) from structured-data.json
- Existing controls (if any) from structured-data.json

This workflow PRODUCES new compliance-focused data:
- Regulations (REG#) - applicable regulatory requirements
- Control Points (CP#) - controls mapped to regulations and process steps
- Compliance Gaps (GAP#) - gaps between requirements and controls
- Control Effectiveness Assessments (CEA#) - effectiveness ratings
- Audit Trail Requirements (ATR#) - evidence and retention needs
- Risk & Compliance Matrix (RCM#) - risk-control mapping
- Regulatory Change Impact (RCI#) - upcoming regulatory changes
- Open Audit Findings (OAF#) - unresolved audit findings affecting the process
- Control Improvement Recommendations (CIR#) - improvement opportunities

---

## CROSS-REFERENCE STRATEGY

All compliance elements must be linked:
- Each CP# control links to one or more REG# regulations
- Each CP# control links to one or more PS# process steps
- Each GAP# gap links to REG# requirement and affected CP# controls
- Each CEA# assessment links to CP# control
- Each RCM# entry links to risks, REG# regulations, and CP# controls
- Each OAF# audit finding links to affected CP# controls
- Each CIR# recommendation links to CP# control it improves

This ensures full regulatory traceability from requirements to controls to evidence.
