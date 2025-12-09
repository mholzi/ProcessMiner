---
name: Import Existing Documentation
description: Pre-read and analyze existing process documentation to extract structured data. Identifies gaps and missing information to reduce redundant SME questioning.
web_bundle: true
---

# Import & Analyze Documentation Workflow

**Goal:** Import and analyze existing process documentation to extract structured data, identify gaps, and prepare for SME validation - honoring existing work before conducting interviews.

**Your Role:** In addition to your name, communication_style, and persona, you are also a documentation analyst and data extraction specialist collaborating with a process owner or SME. This is a partnership, not a client-vendor relationship. You bring expertise in pattern recognition, structured data extraction, and gap analysis, while the user brings their domain knowledge and source documentation. Work together as equals.

---

## WORKFLOW ARCHITECTURE

This uses **step-file architecture** for disciplined execution:

### Core Principles

- **Micro-file Design**: Each step is a self-contained instruction file that is a part of an overall workflow that must be followed exactly
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

## WORKFLOW PRINCIPLES

- **Import Before Interview** - Honor existing work, don't duplicate effort
- **Multi-Format Support** - PDF, Word, Markdown, PowerPoint, Excel, plain text, URLs
- **Intelligent Extraction** - Identify process steps, pain points, controls, systems
- **Gap Analysis** - What's present vs what's missing for full documentation
- **Structured Output** - Extract data in JSON format compatible with start-new-process workflow
- **Preserve Source** - Link extracted data back to source document locations

---

## WORKFLOW PARAMETERS

This workflow uses the shared `select-existing-process` workflow for process selection. Additional parameters can be passed:

| Parameter | Values | Description |
|-----------|--------|-------------|
| `return_mode` | `continue_elicitation` \| `standalone` | Optional. Controls workflow completion behavior |
| `import_mode` | `auto` \| `fresh` \| `augment` \| `replace` | Optional. Controls how existing data is handled |
| `doc_category` | string | Optional. Pre-set document category (from agent menu data) |

**Session variables set by upstream:**
- `contributor_name`, `contributor_role` - Set by agent activation
- `current_process_id`, `current_process_name`, `current_process_folder` - Set by select-existing-process workflow

**return_mode behavior:**
- `continue_elicitation`: Auto-return to calling workflow after completion (no menu)
- `standalone` (default): Show [M] Main Menu / [E] Exit options

**import_mode behavior:**
- `auto` (default): Detect existing data and prompt user for choice
- `fresh`: No existing data expected, create new (fails if data exists)
- `augment`: Merge with existing data, preserving SME-validated content
- `replace`: Overwrite existing data with new imports

---

## INITIALIZATION SEQUENCE

### 1. Configuration Loading

Load and read full config from `{module_root}/config.yaml` and resolve:

- `output_folder`, `user_name`, `communication_language`, `document_output_language`
- `structured_id_system` for ID generation

Set path variables:
- `module_root`: `{project-root}/bmad-custom-modules-src/process-miner`
- `workflow_path`: `{module_root}/workflows/shared/import-existing-docs`
- `select_process_workflow`: `{module_root}/workflows/shared/select-existing-process/workflow.md`

### 2. Process Selection (Shared Workflow)

Load, read and execute `{select_process_workflow}` to:
- Check registry for active processes
- Present numbered list for user selection
- Set session variables: `current_process_id`, `current_process_name`, `current_process_folder`

Note: `contributor_name` and `contributor_role` are already set by agent activation.

### 3. First Step EXECUTION

After process is selected, load, read the full file and then execute `{workflow_path}/steps/step-01-collect.md` to begin the workflow.

---

## WORKFLOW STEPS OVERVIEW

| Step | Name | Goal |
|------|------|------|
| 1 | Document Collection | Collect and store source documents |
| 2 | Document Analysis | Extract structured data from each document |
| 3 | Data Consolidation | Merge, deduplicate, and assign IDs |
| 4 | Gap Analysis | Identify missing information |
| 5 | Structured Output | Generate JSON output file |
| 6 | SME Validation | Review and validate with SME |
| 7 | Integration & Handoff | Prepare for downstream workflows |

---

## OUTPUT FILES

- **Extracted Data**: `{current_process_folder}/imported-data.json`
- **Gap Analysis**: `{current_process_folder}/gap-analysis.md`
- **Source Documents**: `{current_process_folder}/source-documentation/` (preserved originals)

**Documentation (populated from templates):**
- **Main Documentation**: `{current_process_folder}/as-is-process-documentation.md`
- **Pain Points Detail**: `{current_process_folder}/pain-points-detail.md`
- **Exceptions Detail**: `{current_process_folder}/exceptions-detail.md`
- **Control Points Detail**: `{current_process_folder}/control-points-detail.md`

> Note: Documentation files are populated with extracted data and confidence indicators. Missing fields are marked `[REQUIRES SME INPUT]` for completion via start-new-process workflow.
