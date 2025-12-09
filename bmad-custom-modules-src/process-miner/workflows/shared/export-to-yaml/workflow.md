---
name: export-to-yaml
description: Export process data to YAML format
web_bundle: false
status: placeholder
parameters:
  - schema: process-asis-schema

# Process selection - use shared workflow
select_process_workflow: "{module_root}/workflows/shared/select-existing-process/workflow.md"
---

# Export to YAML Workflow

**Goal:** Export process data in structured YAML format for downstream processing.

**Status:** Placeholder - Implementation pending

## Parameters

- `schema`: Export schema to use
  - `process-asis-schema` - AS-IS process schema
  - `compliance-schema` - Compliance data schema
  - `cx-journey-schema` - Customer journey schema
  - `innovation-schema` - Innovation analysis schema

## Session Variables

Set by upstream:
- `contributor_name`, `contributor_role` - Set by agent activation
- `current_process_id`, `current_process_name`, `current_process_folder` - Set by select-existing-process workflow

## Initialization Sequence

### 1. Process Selection (Shared Workflow)

Load, read and execute `{select_process_workflow}` to:
- Select process from registry
- Set session variables: `current_process_id`, `current_process_name`, `current_process_folder`

### 2. Execute Export

After process is selected, execute YAML export.

## Output

Structured YAML file with:
- Process metadata
- Steps with IDs (PS#)
- Exceptions (EX#)
- Pain points (PP#)
- Control points (CP#)
- Systems (SYS#)
- Cross-references
