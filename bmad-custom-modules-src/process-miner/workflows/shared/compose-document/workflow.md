---
name: compose-document
description: Generate AS-IS process documentation
web_bundle: false
status: placeholder
parameters:
  - doc_type: process-asis

# Process selection - use shared workflow
select_process_workflow: "{module_root}/workflows/shared/select-existing-process/workflow.md"
---

# Compose Document Workflow

**Goal:** Generate structured AS-IS process documentation from captured data.

**Status:** Placeholder - Implementation pending

## Parameters

- `doc_type`: Document type to generate
  - `process-asis` - AS-IS process documentation
  - `compliance-assessment` - Compliance assessment document
  - `cx-journey` - Client journey document
  - `innovation-analysis` - Innovation analysis document

## Session Variables

Set by upstream:
- `contributor_name`, `contributor_role` - Set by agent activation
- `current_process_id`, `current_process_name`, `current_process_folder` - Set by select-existing-process workflow

## Initialization Sequence

### 1. Process Selection (Shared Workflow)

Load, read and execute `{select_process_workflow}` to:
- Select process from registry
- Set session variables: `current_process_id`, `current_process_name`, `current_process_folder`

### 2. Execute Workflow

After process is selected, execute document composition.

## Output Format

Multi-altitude documentation:
1. Executive Summary (2-page visual-first)
2. Full Documentation (detailed specifications)

## Functionality

1. Load process data
2. Generate executive summary
3. Generate detailed documentation
4. Include structured references
5. Output to configured location
