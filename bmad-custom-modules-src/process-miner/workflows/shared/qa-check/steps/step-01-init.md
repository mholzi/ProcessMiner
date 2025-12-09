---
name: 'step-01-init'
description: 'Load process documents and verify all files exist - SILENT MODE'

# Path Definitions
module_root: '{project-root}/bmad-custom-modules-src/process-miner'
workflow_path: '{module_root}/workflows/shared/qa-check'

# File References
thisStepFile: '{workflow_path}/steps/step-01-init.md'
nextStepFile: '{workflow_path}/steps/step-02-build-review-plan.md'
workflowFile: '{workflow_path}/workflow.md'

# QA Checklist
qa_checklist: '{workflow_path}/qa-checklist.md'

# Schema files for validation rules
schema_folder: '{module_root}/templates'
schemas:
  as_is_process: '{schema_folder}/as-is-process-documentation.schema.yaml'
  compliance_control: '{schema_folder}/compliance-control-assessment.schema.yaml'
  control_points_detail: '{schema_folder}/control-points-detail.schema.yaml'
  cx_journey: '{schema_folder}/cx-journey-documentation.schema.yaml'

# Process Documents to Validate
structuredDataFile: '{current_process_folder}/structured-data.json'
mainDocumentFile: '{current_process_folder}/as-is-process-documentation.md'
exceptionsDetailFile: '{current_process_folder}/exceptions-detail.md'
painPointsDetailFile: '{current_process_folder}/pain-points-detail.md'
controlPointsDetailFile: '{current_process_folder}/control-points-detail.md'

# Execution Mode
execution_mode: silent
---

# Step 1: Initialize QA Review (SILENT)

## STEP GOAL

Load all process documentation files and verify they exist. Initialize the findings collection. Execute silently - no user output until Step 4.

## EXECUTION MODE: SILENT

**CRITICAL:** This step runs silently.
- NO display output to user
- NO menus or pauses
- Log all errors as findings
- Auto-proceed to next step immediately

---

## MANDATORY EXECUTION RULES:

### Silent Mode Rules:

- 🔇 **NO OUTPUT** - Do not display anything to user
- ⚡ **NO PAUSES** - Do not wait for input
- 📝 **LOG EVERYTHING** - Record all issues as findings
- ➡️ **AUTO-PROCEED** - Immediately load next step when done

### Error Handling:

- If file missing → Create CRITICAL finding, continue
- If file unreadable → Create CRITICAL finding, continue
- If JSON invalid → Create CRITICAL finding, continue
- **NEVER STOP** - Always continue to next action

---

## EXECUTION SEQUENCE (SILENT)

### 1. Initialize Session Context

```
<action silent="true">
Set session variables:
- qa_start_time = {{timestamp}}
- process_id = {current_process_id}
- process_name = {current_process_name}
- reviewer = {contributor_name}
- reviewer_role = {contributor_role}
</action>
```

### 2. Initialize Findings Collection

```
<action silent="true">
Create findings tracking object:

qa_findings = {
  "session": {
    "process_id": "{current_process_id}",
    "process_name": "{current_process_name}",
    "reviewer": "{contributor_name}",
    "reviewer_role": "{contributor_role}",
    "started": "{{qa_start_time}}",
    "status": "IN_PROGRESS"
  },
  "documents": {
    "structured_data": { "path": "{structuredDataFile}", "loaded": false, "content": null },
    "main_document": { "path": "{mainDocumentFile}", "loaded": false, "content": null },
    "exceptions_detail": { "path": "{exceptionsDetailFile}", "loaded": false, "content": null },
    "pain_points_detail": { "path": "{painPointsDetailFile}", "loaded": false, "content": null },
    "control_points_detail": { "path": "{controlPointsDetailFile}", "loaded": false, "content": null }
  },
  "findings": [],
  "summary": {
    "critical": 0,
    "high": 0,
    "medium": 0,
    "low": 0,
    "total": 0
  },
  "phases_completed": []
}
</action>
```

### 3. Load Documents (with error handling)

```
<action silent="true">
For each document in [structured_data, main_document, exceptions_detail, pain_points_detail, control_points_detail]:

TRY:
  - Read file from {document.path}
  - IF successful:
    - Store content in qa_findings.documents.{document}.content
    - Set qa_findings.documents.{document}.loaded = true

CATCH file_not_found:
  - Set qa_findings.documents.{document}.loaded = false
  - Add finding:
    {
      "id": "INIT-{seq}",
      "severity": "CRITICAL",
      "category": "Document Loading",
      "phase": 1,
      "title": "Missing document: {document_name}",
      "location": "{document.path}",
      "description": "Required document not found at expected location",
      "impact": "Cannot validate {document_type} - entire validation category blocked",
      "evidence": "File does not exist: {document.path}",
      "recommendation": "Create document using appropriate workflow or template"
    }
  - Increment qa_findings.summary.critical
  - Increment qa_findings.summary.total

CATCH file_read_error:
  - Set qa_findings.documents.{document}.loaded = false
  - Add finding:
    {
      "id": "INIT-{seq}",
      "severity": "CRITICAL",
      "category": "Document Loading",
      "phase": 1,
      "title": "Cannot read document: {document_name}",
      "location": "{document.path}",
      "description": "File exists but cannot be read",
      "impact": "Cannot validate {document_type}",
      "evidence": "Read error: {error_message}",
      "recommendation": "Check file permissions and format"
    }
  - Increment qa_findings.summary.critical
  - Increment qa_findings.summary.total

CONTINUE to next document (never stop)
</action>
```

### 4. Validate JSON Structure (if loaded)

```
<action silent="true">
IF qa_findings.documents.structured_data.loaded == true:

TRY:
  - Parse JSON content
  - Validate has required top-level keys: session, metadata, process_steps, process_exceptions, pain_points, controls, systems, validation
  - Store parsed object for later use

CATCH json_parse_error:
  - Add finding:
    {
      "id": "INIT-{seq}",
      "severity": "CRITICAL",
      "category": "Data Integrity",
      "phase": 1,
      "title": "Invalid JSON in structured-data.json",
      "location": "{structuredDataFile}",
      "description": "JSON parsing failed - file is malformed",
      "impact": "Cannot perform any ID validation or cross-document checks",
      "evidence": "Parse error: {error_message} at position {position}",
      "recommendation": "Fix JSON syntax errors in structured-data.json"
    }
  - Increment qa_findings.summary.critical
  - Increment qa_findings.summary.total

CATCH missing_required_keys:
  - For each missing key, add finding:
    {
      "id": "INIT-{seq}",
      "severity": "HIGH",
      "category": "Schema Compliance",
      "phase": 1,
      "title": "Missing required key in structured-data.json: {key_name}",
      "location": "{structuredDataFile}",
      "description": "Required top-level key '{key_name}' not found in JSON structure",
      "impact": "Related validation checks will be skipped",
      "evidence": "Key '{key_name}' not present in JSON root",
      "recommendation": "Add '{key_name}' section to structured-data.json"
    }
  - Increment qa_findings.summary.high
  - Increment qa_findings.summary.total
</action>
```

### 5. Detect Document Type and Load Primary Schema

```
<action silent="true">
Detect primary document type from main document filename or content:

IF mainDocumentFile contains "as-is-process":
  primary_schema_path = {schemas.as_is_process}
  document_type = "as_is_process"
ELSE IF mainDocumentFile contains "compliance-control":
  primary_schema_path = {schemas.compliance_control}
  document_type = "compliance_control"
ELSE IF mainDocumentFile contains "cx-journey":
  primary_schema_path = {schemas.cx_journey}
  document_type = "cx_journey"
ELSE:
  primary_schema_path = {schemas.as_is_process}  // Default
  document_type = "as_is_process"

Store document_type in qa_findings.document_type
</action>
```

### 6. Load Schema Files

```
<action silent="true">
schemas_loaded = {
  "primary": null,
  "detail_schemas": {}
}

// Load primary schema
TRY:
  - Load {primary_schema_path}
  - Parse YAML content
  - Store in schemas_loaded.primary
  - Extract validation rules:
    - id_patterns (e.g., PS\\d{3}, EX\\d{3}, etc.)
    - incomplete_markers (e.g., [TBD], [TODO], etc.)
    - required_references by section
    - sections with sync_enabled flags
    - confidence_rules (thresholds)

CATCH file_not_found OR yaml_parse_error:
  - Add finding:
    {
      "id": "INIT-{seq}",
      "severity": "MEDIUM",
      "category": "Schema Loading",
      "phase": 1,
      "title": "Primary schema file not found or invalid",
      "location": "{primary_schema_path}",
      "description": "Could not load validation schema - using hardcoded fallbacks",
      "impact": "Validation will use default rules instead of schema-defined rules",
      "evidence": "Error: {error_message}",
      "recommendation": "Ensure schema file exists at {primary_schema_path}"
    }
  - Increment qa_findings.summary.medium
  - Increment qa_findings.summary.total
  - Set schemas_loaded.primary = null (will use fallbacks)

// Load control-points-detail schema (always needed for CP# validation)
TRY:
  - Load {schemas.control_points_detail}
  - Parse YAML content
  - Store in schemas_loaded.detail_schemas.control_points

CATCH:
  - Continue without (optional schema)

Store schemas_loaded in qa_findings.schemas_loaded
</action>
```

### 7. Build Validation Rules from Schema

```
<action silent="true">
IF schemas_loaded.primary != null:

  validation_rules = {
    "source": "schema",
    "schema_version": schemas_loaded.primary.schema_version,
    "template_name": schemas_loaded.primary.template_name,

    "id_patterns": schemas_loaded.primary.id_patterns,
    // e.g., { process_step: "PS\\d{3}", exception: "EX\\d{3}", ... }

    "incomplete_markers": schemas_loaded.primary.confidence_rules.incomplete_markers,
    // e.g., ["[TBD]", "[Unknown]", "[TODO]", "{{.*}}", "..."]

    "confidence_thresholds": {
      "high": schemas_loaded.primary.confidence_rules.high_threshold,
      "medium": schemas_loaded.primary.confidence_rules.medium_threshold
    },

    "required_references": schemas_loaded.primary.confidence_rules.required_references,
    // e.g., { 2: ["PS#", "SYS#"], 3: ["EX#", "PS#"], ... }

    "sections": schemas_loaded.primary.sections,
    // Full section definitions with sync_enabled, detail_document, etc.

    "control_types": schemas_loaded.detail_schemas.control_points?.control_types || null,
    "effectiveness_ratings": schemas_loaded.detail_schemas.control_points?.effectiveness_ratings || null,
    "risk_levels": schemas_loaded.detail_schemas.control_points?.risk_levels || null
  }

ELSE:
  // Fallback to hardcoded rules (backwards compatibility)
  validation_rules = {
    "source": "hardcoded_fallback",

    "id_patterns": {
      "process_step": "PS\\d{3}",
      "exception": "EX\\d{3}",
      "control_point": "CP\\d{3}",
      "pain_point": "PP\\d{3}",
      "system": "SYS\\d{3}"
    },

    "incomplete_markers": ["[TBD]", "[Unknown]", "[TODO]", "{{.*}}", "..."],

    "confidence_thresholds": { "high": 90, "medium": 70 },

    "required_references": {
      "2": ["PS#", "SYS#"],
      "3": ["EX#", "PS#"],
      "4": ["CP#", "PS#"],
      "9": ["PP#", "PS#"]
    },

    "sections": null,
    "control_types": null,
    "effectiveness_ratings": null,
    "risk_levels": null
  }

Store validation_rules in qa_findings.validation_rules
</action>
```

### 8. Load QA Checklist

```
<action silent="true">
TRY:
  - Load {qa_checklist}
  - Store checklist reference for Step 3

CATCH:
  - Add finding:
    {
      "id": "INIT-{seq}",
      "severity": "MEDIUM",
      "category": "Workflow Configuration",
      "phase": 1,
      "title": "QA checklist not found",
      "location": "{qa_checklist}",
      "description": "Validation checklist file missing",
      "impact": "Validation will proceed without checklist reference",
      "evidence": "File not found: {qa_checklist}",
      "recommendation": "Ensure qa-checklist.md exists in workflow folder"
    }
  - Increment qa_findings.summary.medium
  - Increment qa_findings.summary.total
  - Continue without checklist
</action>
```

### 9. Record Phase Completion

```
<action silent="true">
Add "phase-1-init" to qa_findings.phases_completed
Set phase_1_end_time = {{timestamp}}
</action>
```

### 10. Auto-Proceed to Next Step

```
<action silent="true">
IMMEDIATELY load, read entire file, then execute {nextStepFile}
DO NOT pause or wait for user input
</action>
```

---

## FINDINGS ADDED IN THIS STEP

| Finding Type | Severity | Trigger |
|--------------|----------|---------|
| Missing document | CRITICAL | Any of 5 required files not found |
| Unreadable document | CRITICAL | File exists but cannot be read |
| Invalid JSON | CRITICAL | structured-data.json parse failure |
| Missing JSON keys | HIGH | Required top-level keys absent |
| Missing schema | MEDIUM | Primary schema file not found or invalid |
| Missing checklist | MEDIUM | qa-checklist.md not found |

---

## SUCCESS CRITERIA (Internal - Not Displayed)

- ✅ All 5 document load attempts made
- ✅ Missing/error documents recorded as findings
- ✅ Findings collection initialized
- ✅ JSON validated (if loadable)
- ✅ Document type detected and primary schema loaded (or fallback used)
- ✅ Validation rules built from schema (or hardcoded fallback)
- ✅ Auto-proceeded to Step 2

---

## FAILURE MODE

There is no failure that stops execution. ALL errors become findings and execution continues.
