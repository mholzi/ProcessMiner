---
name: qa-check
description: Adversarial QA validation workflow that identifies 3-10 specific issues per process, challenging documentation completeness, ID consistency, traceability, and compliance coverage. Runs silently until complete, then presents full summary with fix options.
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

# Workflow paths
installed_path: "{module_root}/workflows/shared/qa-check"
workflow_path: "{installed_path}"
steps_folder: "{workflow_path}/steps"

# Process selection - use shared workflow
select_process_workflow: "{module_root}/workflows/shared/select-existing-process/workflow.md"

# Validation artifact
qa_checklist: "{workflow_path}/qa-checklist.md"

# Report template
qa_report_template: "{module_root}/templates/qa-report.md"

# Schema files for validation rules (loaded dynamically based on document type)
schema_folder: "{module_root}/templates"
schemas:
  as_is_process: "{schema_folder}/as-is-process-documentation.schema.yaml"
  compliance_control: "{schema_folder}/compliance-control-assessment.schema.yaml"
  control_points_detail: "{schema_folder}/control-points-detail.schema.yaml"
  cx_journey: "{schema_folder}/cx-journey-documentation.schema.yaml"

# Primary schema - determined by main document type
primary_schema: session-variable

# Process context - set by select-existing-process workflow
current_process_folder: session-variable
current_process_id: session-variable
current_process_name: session-variable

# Contributor tracking - set by agent activation
contributor_name: session-variable
contributor_role: session-variable

# Process documents to validate
process_documents:
  structured_data: "{current_process_folder}/structured-data.json"
  main_document: "{current_process_folder}/as-is-process-documentation.md"
  exceptions_detail: "{current_process_folder}/exceptions-detail.md"
  pain_points_detail: "{current_process_folder}/pain-points-detail.md"
  control_points_detail: "{current_process_folder}/control-points-detail.md"

# Output
qa_report_output: "{current_process_folder}/qa-report.md"

# Execution mode
execution_mode: silent-until-complete

standalone: false
---

# QA Check Workflow

**Goal:** Execute adversarial quality assurance validation on process documentation, identifying 3-10 specific issues minimum. No lazy "looks good" reviews - find real problems.

**Your Role:** In addition to your name, communication_style, and persona, you are also a Senior QA Analyst conducting an adversarial review. This is NOT a rubber-stamp approval process. You bring rigorous validation methodology, while the SME brings domain context. Challenge every claim, verify every reference, find every gap.

---

## EXECUTION MODE: SILENT UNTIL COMPLETE

**CRITICAL:** This workflow runs autonomously after process selection.

```
Process Selection → [SILENT EXECUTION] → Full Summary with Fix Options
        ↑                                           ↑
   User interacts                              User interacts
```

**Silent Execution Rules:**
- NO menus or pauses during Steps 1-3
- NO waiting for user input until summary
- Log errors as findings and continue (don't stop)
- Auto-proceed through all validation phases
- Only present output at the end

---

## REVIEW PHILOSOPHY

**Core Principle:** Find 3-10 specific issues in every review minimum.

- **Validate every claim** - Cross-reference structured data against documentation
- **Challenge completeness** - Missing rationale, orphaned references, gaps in coverage
- **Verify traceability** - All IDs consistent, all controls traced, no orphans
- **Question compliance** - Are all required fields populated? Are standards met?

---

## WORKFLOW ARCHITECTURE

This uses **step-file architecture** with **silent execution mode**:

### Core Principles

- **Micro-file Design**: Each step is a self-contained instruction file
- **Just-In-Time Loading**: Only the current step file is in memory
- **Sequential Enforcement**: Steps must be completed in order
- **Adversarial Mindset**: Actively look for problems, don't assume correctness
- **Silent Execution**: No user interaction until final summary

### Step Processing Rules

1. **READ COMPLETELY**: Always read the entire step file before taking any action
2. **FOLLOW SEQUENCE**: Execute all numbered sections in order, never deviate
3. **NO PAUSES**: Do NOT halt for menus - auto-proceed to next step
4. **FIND ISSUES**: Minimum 3-10 findings per review - no exceptions
5. **LOG ERRORS**: If something fails, record as finding and continue
6. **LOAD NEXT**: Immediately load and execute next step file after completion

### Critical Rules (NO EXCEPTIONS)

- 🛑 **NEVER** load multiple step files simultaneously
- 📖 **ALWAYS** read entire step file before execution
- 🚫 **NEVER** skip steps or optimize the sequence
- ⚔️ **NEVER** give a clean bill of health without thorough validation
- 🎯 **ALWAYS** find minimum 3-10 specific issues
- 🔇 **NEVER** pause for user input until Step 4 (Summary)
- ⚡ **ALWAYS** auto-proceed after completing each step

---

## STEP OVERVIEW

| Step | File | Mode | Goal |
|------|------|------|------|
| 1 | step-01-init.md | SILENT | Load documents, verify existence, initialize findings |
| 2 | step-02-build-review-plan.md | SILENT | Analyze documents, build attack plan |
| 3 | step-03-execute-checks.md | SILENT | Execute all 40 validation checks |
| 4 | step-04-summary.md | INTERACTIVE | Present full summary, offer fix options, generate report |

---

## VALIDATION CATEGORIES

### 1. Documentation Completeness
- All required sections present
- No placeholder or TODO content
- Rationale provided for all steps
- Confidence levels assigned

### 2. ID Consistency & Traceability
- PS# (Process Steps) sequential and complete
- EX# (Exceptions) linked to parent steps
- PP# (Pain Points) linked to sources
- CP# (Control Points) traced to requirements
- SYS# (Systems) referenced correctly
- No orphaned or duplicate IDs

### 3. Cross-Document Integrity
- structured-data.json matches markdown documents
- Detail documents match main document references
- All cross-references resolve correctly

### 4. Compliance Coverage
- Required controls documented
- Regulatory requirements addressed
- Audit trail complete

### 5. Data Quality
- No empty or null required fields
- Dates and timestamps valid
- Status values correct

---

## SEVERITY LEVELS

- **CRITICAL** - Must fix before approval (missing required data, broken references, compliance gaps)
- **HIGH** - Should fix soon (incomplete sections, unclear content, weak traceability)
- **MEDIUM** - Should fix eventually (minor inconsistencies, style issues)
- **LOW** - Nice to fix (suggestions, enhancements)

---

## ERROR HANDLING

During silent execution, if any error occurs:

1. **DO NOT STOP** - Continue with remaining checks
2. **LOG AS FINDING** - Record error as a finding with appropriate severity
3. **CONTINUE** - Proceed to next check/step

Example errors to handle:
- File not found → CRITICAL finding
- JSON parse error → CRITICAL finding
- Missing expected field → HIGH/MEDIUM finding depending on field
- Reference doesn't resolve → HIGH finding

---

## INITIALIZATION SEQUENCE

### 1. Configuration Loading

Load and read full config from `{config_source}` and resolve:

- `output_folder`, `user_name`, `communication_language`, `document_output_language`

### 2. Process Selection (Shared Workflow) - INTERACTIVE

Load, read and execute `{select_process_workflow}` to:
- Check registry for active processes
- Present numbered list for user selection
- Set session variables: `current_process_id`, `current_process_name`, `current_process_folder`

Note: `contributor_name` and `contributor_role` are already set by agent activation.

### 3. Silent QA Execution

Display once:
```
Starting QA validation for {current_process_name}...
This will take a moment. Full results will be displayed when complete.
```

Then immediately load and execute `{workflow_path}/steps/step-01-init.md` in SILENT mode.

### 4. Summary Presentation

After all checks complete, Step 4 presents the full interactive summary with fix options.
