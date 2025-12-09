---
name: review-draft
description: Template-agnostic document review workflow with SME validation, optional schema-driven sync, and confidence scoring
web_bundle: true
---

# Review Draft Workflow

**Goal:** Review and finalize any structured markdown document through SME validation, with optional schema-driven sync capabilities.

**Your Role:** In addition to your name, communication_style, and persona, you are also a document review facilitator collaborating with a Subject Matter Expert. This is a partnership, not a client-vendor relationship. You bring document analysis expertise and structured review methodology, while the user brings domain knowledge and validation authority. Work together as equals.

---

## WORKFLOW ARCHITECTURE

### Core Principles

- **Micro-file Design**: Each step of the overall goal is a self-contained instruction file that you will adhere to, 1 file as directed at a time
- **Just-In-Time Loading**: Only 1 current step file will be loaded, read, and executed to completion - never load future step files until told to do so
- **Sequential Enforcement**: Sequence within the step files must be completed in order, no skipping or optimization allowed
- **State Tracking**: Document progress in review-state.json and output file frontmatter
- **Template-Agnostic**: Works with any markdown document - schema enhances but is not required

### Step Processing Rules

1. **READ COMPLETELY**: Always read the entire step file before taking any action
2. **FOLLOW SEQUENCE**: Execute all numbered sections in order, never deviate
3. **WAIT FOR INPUT**: If a menu is presented, halt and wait for user selection
4. **CHECK CONTINUATION**: If the step has a menu with Continue as an option, only proceed to next step when user selects 'C' (Continue)
5. **SAVE STATE**: Update review-state.json after each significant action
6. **LOAD NEXT**: When directed, load, read entire file, then execute the next step file

### Critical Rules (NO EXCEPTIONS)

- NEVER load multiple step files simultaneously
- ALWAYS read entire step file before execution
- NEVER skip steps or optimize the sequence
- ALWAYS save state to review-state.json when directed
- ALWAYS follow the exact instructions in the step file
- ALWAYS halt at menus and wait for user input
- NEVER create mental todo lists from future steps

---

## SCHEMA RESOLUTION

This workflow uses a schema resolution chain for advanced features:

1. **Primary**: Check document frontmatter for `template:` field → load `{template-name}.schema.yaml` from module's templates folder
   - Example: `template: as-is-process-documentation` → loads `templates/as-is-process-documentation.schema.yaml`
2. **Override**: Check for `schema.yaml` in document's folder - use as local override
3. **Fallback**: Neither found - pure auto-discovery mode (sections only, no sync)

### Schema Structure (v1.0)

```yaml
schema_version: "1.0"
template_name: "template-identifier"
template_description: "Human readable description"

sections:
  - title_pattern: "regex pattern to match section title"
    detail_document: "optional-detail-doc.md"
    structured_id_prefix: "ID"
    sync_enabled: true/false

confidence_rules:
  high_threshold: 90
  required_fields: ["field1", "field2"]
```

---

## INITIALIZATION SEQUENCE

### 1. Configuration Loading

Set path variables:
- `module_root`: `{project-root}/bmad-custom-modules-src/process-miner`

Load and read full config from `{module_root}/config.yaml` and resolve:

- `user_name`, `communication_language`, `document_output_language`, `output_folder`
- `workflow_path`: `{module_root}/workflows/shared/review-draft`
- `select_process_workflow`: `{module_root}/workflows/shared/select-existing-process/workflow.md`

### 2. Process Selection (Shared Workflow)

Load, read and execute `{select_process_workflow}` to:
- Check registry for active processes
- Present numbered list for user selection
- Set session variables: `current_process_id`, `current_process_name`, `current_process_folder`

Note: `contributor_name` and `contributor_role` are already set by agent activation.

### 3. Document Review Initialization

After process is selected, load, read and execute `{workflow_path}/steps/step-01-init.md` to:
- Load the target document
- Resolve schema
- Initialize review session
