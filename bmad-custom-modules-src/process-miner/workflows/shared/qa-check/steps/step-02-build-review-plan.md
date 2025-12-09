---
name: 'step-02-build-review-plan'
description: 'Analyze loaded documents and build adversarial attack plan - SILENT MODE'

# Path Definitions
module_root: '{project-root}/bmad-custom-modules-src/process-miner'
workflow_path: '{module_root}/workflows/shared/qa-check'

# File References
thisStepFile: '{workflow_path}/steps/step-02-build-review-plan.md'
nextStepFile: '{workflow_path}/steps/step-03-execute-checks.md'
workflowFile: '{workflow_path}/workflow.md'

# Execution Mode
execution_mode: silent
---

# Step 2: Build Adversarial Review Plan (SILENT)

## STEP GOAL

Analyze the loaded documents to understand their structure, extract metrics, and build a targeted attack plan. Execute silently - no user output.

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

- If analysis fails → Create finding, continue with partial data
- If counts mismatch → Create finding, note discrepancy
- **NEVER STOP** - Always continue to next action

---

## EXECUTION SEQUENCE (SILENT)

### 1. Extract Structured Data Metrics

```
<action silent="true">
IF qa_findings.documents.structured_data.loaded == true:

Extract and store:

metrics = {
  "schema_version": structured_data.$schema || "unknown",
  "process_id": structured_data.session.process.id,
  "process_name": structured_data.session.process.name,
  "validation_status": structured_data.validation.status,

  "id_counts": {
    "process_steps": count(structured_data.process_steps) || 0,
    "exceptions": count(structured_data.process_exceptions) || 0,
    "pain_points": count(structured_data.pain_points) || 0,
    "controls": count(structured_data.controls) || 0,
    "systems": count(structured_data.systems) || 0
  },

  "metadata_status": {
    "purpose": structured_data.metadata.purpose != null,
    "trigger": structured_data.metadata.trigger != null,
    "frequency": structured_data.metadata.frequency != null,
    "volume": structured_data.metadata.volume != null,
    "confidence": structured_data.metadata.confidence != null
  },

  "id_lists": {
    "ps_ids": extract all PS### IDs from process_steps,
    "ex_ids": extract all EX### IDs from process_exceptions,
    "pp_ids": extract all PP### IDs from pain_points,
    "cp_ids": extract all CP### IDs from controls,
    "sys_ids": extract all SYS### IDs from systems
  },

  "unknowns": structured_data.validation.unknowns || [],
  "overrides": structured_data.validation.overrides || []
}

Store metrics in qa_findings.metrics

ELSE:
  Set qa_findings.metrics = null
  Note: ID validation checks will be limited
</action>
```

### 2. Analyze Main Document Structure (Schema-Driven)

```
<action silent="true">
IF qa_findings.documents.main_document.loaded == true:

// Get validation rules from Step 1 (schema-derived or fallback)
validation_rules = qa_findings.validation_rules

// Build expected sections from schema (if available) or use defaults
IF validation_rules.sections != null:
  sections_expected = validation_rules.sections.map(s => s.title_pattern)
  sync_enabled_sections = validation_rules.sections.filter(s => s.sync_enabled)
  detail_document_map = validation_rules.sections
    .filter(s => s.detail_document != null)
    .map(s => { section: s.title_pattern, detail_doc: s.detail_document, id_prefix: s.structured_id_prefix })
ELSE:
  // Fallback to hardcoded defaults
  sections_expected = [
    "Executive Summary",
    "Process Overview",
    "Process Steps",
    "Systems & Tools",
    "Controls & Compliance",
    "Known Issues"
  ]
  sync_enabled_sections = []
  detail_document_map = []

// Build ID patterns from schema (if available)
IF validation_rules.id_patterns != null:
  id_patterns = validation_rules.id_patterns
  // Dynamic - supports any ID types defined in schema (PS#, EX#, JT#, FP#, etc.)
ELSE:
  id_patterns = {
    "process_step": "PS\\d{3}",
    "exception": "EX\\d{3}",
    "control_point": "CP\\d{3}",
    "pain_point": "PP\\d{3}",
    "system": "SYS\\d{3}"
  }

// Get incomplete markers from schema (if available)
IF validation_rules.incomplete_markers != null:
  incomplete_markers = validation_rules.incomplete_markers
ELSE:
  incomplete_markers = ["[TBD]", "[Unknown]", "[TODO]", "{{.*}}", "..."]

Parse markdown to identify:

main_doc_analysis = {
  "schema_source": validation_rules.source,
  "document_type": qa_findings.document_type,

  "sections_found": [list of ## headings found],
  "sections_expected": sections_expected,
  "sections_missing": [expected - found],
  "sync_enabled_sections": sync_enabled_sections,
  "detail_document_map": detail_document_map,

  "content_flags": {
    "has_incomplete_markers": search for each marker in incomplete_markers,
    "incomplete_marker_locations": [{ marker: "...", location: "section X", line: N }],
    "has_empty_sections": sections with < 50 characters,
    "placeholder_locations": [list of locations where markers found]
  },

  "id_references": {
    // Dynamically extract based on id_patterns from schema
    FOR EACH pattern_name, pattern_regex IN id_patterns:
      "{pattern_name}_refs": extract all matches for pattern_regex
  },

  "required_references_check": {
    // Check each section for required references from schema
    FOR EACH section_num, required_ids IN validation_rules.required_references:
      section_num: {
        "required": required_ids,
        "found": [which required IDs are present],
        "missing": [which required IDs are missing]
      }
  },

  "word_count": total words in document,
  "section_word_counts": {section: count for each section}
}

Store in qa_findings.main_doc_analysis

ELSE:
  Set qa_findings.main_doc_analysis = null
</action>
```

### 3. Analyze Detail Documents (Schema-Driven)

```
<action silent="true">
// Get validation rules and detail document map from schema
validation_rules = qa_findings.validation_rules
detail_document_map = qa_findings.main_doc_analysis?.detail_document_map || []

// Get control-specific schema if loaded (for required fields, ratings, etc.)
control_schema = qa_findings.schemas_loaded?.detail_schemas?.control_points

For each detail document [exceptions_detail, pain_points_detail, control_points_detail]:

IF qa_findings.documents.{doc}.loaded == true:

  // Determine required fields from schema (if available)
  IF {doc} == "control_points_detail" AND control_schema != null:
    required_fields = control_schema.confidence_rules.required_control_fields
    // e.g., [control_id, control_name, control_type, regulation, effectiveness, control_activity, evidence_captured]
    valid_effectiveness_ratings = control_schema.effectiveness_ratings.map(r => r.rating)
    // e.g., ["Highly Effective", "Effective", "Partially Effective", "Ineffective", "Not Operating"]
    valid_control_types = control_schema.control_types.by_purpose + control_schema.control_types.by_execution
    // e.g., ["Preventive", "Detective", "Corrective", "Automated", "Manual", "Semi-Automated"]
    valid_risk_levels = control_schema.risk_levels.map(r => r.level)
    // e.g., ["Critical", "High", "Medium", "Low"]
  ELSE IF {doc} == "exceptions_detail":
    required_fields = ["exception_id", "parent_step_id", "description", "handling"]
    valid_effectiveness_ratings = null
    valid_control_types = null
    valid_risk_levels = null
  ELSE IF {doc} == "pain_points_detail":
    required_fields = ["pain_point_id", "source_type", "source_id", "severity", "description"]
    valid_effectiveness_ratings = null
    valid_control_types = null
    valid_risk_levels = null
  ELSE:
    required_fields = []
    valid_effectiveness_ratings = null
    valid_control_types = null
    valid_risk_levels = null

  // Get ID pattern for this document type from schema
  id_prefix = detail_document_map.find(d => d.detail_doc matches {doc})?.id_prefix
  IF id_prefix AND validation_rules.id_patterns:
    id_pattern = find pattern in validation_rules.id_patterns where prefix matches id_prefix
  ELSE:
    // Fallback patterns
    IF {doc} == "exceptions_detail": id_pattern = "EX\\d{3}"
    ELSE IF {doc} == "pain_points_detail": id_pattern = "PP\\d{3}"
    ELSE IF {doc} == "control_points_detail": id_pattern = "CP\\d{3}"

  detail_analysis = {
    "document": "{doc}",
    "schema_source": validation_rules.source,
    "id_pattern": id_pattern,
    "entry_count": count entries (## headings or structured items),
    "ids_found": [list of IDs matching id_pattern in this document],
    "has_empty_entries": boolean,
    "empty_entry_ids": [list of IDs with minimal content],

    "required_fields_check": {
      "required_fields": required_fields,
      "complete": count entries with all required fields populated,
      "incomplete": count entries missing required fields,
      "incomplete_ids": [list of IDs missing fields],
      "missing_fields_detail": [{ id: "CP001", missing: ["effectiveness", "evidence_captured"] }]
    },

    // Schema-driven value validation (for control_points_detail)
    "value_validation": {
      "effectiveness_ratings": {
        "valid_values": valid_effectiveness_ratings,
        "invalid_entries": [entries with invalid effectiveness values]
      },
      "control_types": {
        "valid_values": valid_control_types,
        "invalid_entries": [entries with invalid control types]
      },
      "risk_levels": {
        "valid_values": valid_risk_levels,
        "invalid_entries": [entries with invalid risk levels]
      }
    }
  }

  Store in qa_findings.detail_analysis.{doc}

ELSE:
  Set qa_findings.detail_analysis.{doc} = null
</action>
```

### 4. Build Attack Plan (Schema-Driven)

```
<action silent="true">
// Get validation rules from Step 1
validation_rules = qa_findings.validation_rules

Based on analysis, create targeted attack plan:

attack_plan = {
  "schema_source": validation_rules.source,
  "document_type": qa_findings.document_type,

  "phase_1_id_integrity": {
    "enabled": qa_findings.metrics != null,
    "id_patterns": validation_rules.id_patterns,  // Schema-derived patterns
    "checks": [
      // Dynamically build checks based on ID patterns in schema
      FOR EACH id_type, pattern IN validation_rules.id_patterns:
        {"id": "1.{n}", "name": "{id_type} Sequence", "target": metrics.id_lists[id_type], "pattern": pattern},
        {"id": "1.{n+1}", "name": "{id_type} Duplicates", "target": metrics.id_lists[id_type], "pattern": pattern}

      // Standard relationship checks
      {"id": "1.x", "name": "Parent Linkage Validation", "target": "all child IDs"},
      {"id": "1.x", "name": "Orphaned IDs", "target": "all"},
      {"id": "1.x", "name": "Cross-ID Consistency", "target": "all"}
    ],
    "risk_areas": identify_high_risk_ids()
  },

  "phase_2_cross_document": {
    "enabled": qa_findings.metrics != null && qa_findings.main_doc_analysis != null,
    "sync_enabled_sections": qa_findings.main_doc_analysis.sync_enabled_sections,
    "detail_document_map": qa_findings.main_doc_analysis.detail_document_map,
    "checks": [
      {"id": "2.1", "name": "Count Synchronization", "target": "json vs markdown"},
      // Dynamic checks based on schema-defined sync sections
      FOR EACH section IN sync_enabled_sections:
        {"id": "2.{n}", "name": "{section.id_prefix}# in Detail Doc", "target": section.detail_document}

      {"id": "2.x", "name": "Reference Resolution", "target": main_doc_analysis.id_references},
      {"id": "2.x", "name": "Phantom References", "target": "all"},
      {"id": "2.x", "name": "Bidirectional Links", "target": "all"}
    ],
    "risk_areas": identify_sync_risks()
  },

  "phase_3_completeness": {
    "enabled": qa_findings.main_doc_analysis != null,
    "sections_expected": qa_findings.main_doc_analysis.sections_expected,  // From schema
    "incomplete_markers": validation_rules.incomplete_markers,  // From schema
    "required_references": validation_rules.required_references,  // From schema
    "checks": [
      {"id": "3.1", "name": "Required Sections", "target": main_doc_analysis.sections_missing, "source": "schema"},
      {"id": "3.2", "name": "Incomplete Markers", "target": main_doc_analysis.content_flags.incomplete_marker_locations, "markers": validation_rules.incomplete_markers},
      {"id": "3.3", "name": "Empty Sections", "target": main_doc_analysis.content_flags.has_empty_sections},
      {"id": "3.4", "name": "Required References by Section", "target": main_doc_analysis.required_references_check, "source": "schema"},
      {"id": "3.5", "name": "Confidence Levels", "target": "metadata", "thresholds": validation_rules.confidence_thresholds},
      {"id": "3.6", "name": "Metadata Fields", "target": metrics.metadata_status}
    ],
    "risk_areas": main_doc_analysis.sections_missing
  },

  "phase_4_compliance": {
    "enabled": qa_findings.detail_analysis.control_points_detail != null,
    "control_types": validation_rules.control_types,  // From schema
    "effectiveness_ratings": validation_rules.effectiveness_ratings,  // From schema
    "risk_levels": validation_rules.risk_levels,  // From schema
    "checks": [
      {"id": "4.1", "name": "Control Coverage", "target": "PS# with compliance implications"},
      {"id": "4.2", "name": "Regulatory References", "target": metrics.id_lists.cp_ids},
      {"id": "4.3", "name": "Risk Levels", "target": "CP# and PP#", "valid_values": validation_rules.risk_levels},
      {"id": "4.4", "name": "Effectiveness Ratings", "target": "CP#", "valid_values": validation_rules.effectiveness_ratings},
      {"id": "4.5", "name": "Control Types", "target": "CP#", "valid_values": validation_rules.control_types},
      {"id": "4.6", "name": "Mitigation Documentation", "target": "PP# items"}
    ],
    "risk_areas": identify_compliance_gaps()
  },

  "phase_5_data_quality": {
    "enabled": qa_findings.metrics != null,
    "id_patterns": validation_rules.id_patterns,  // From schema
    "checks": [
      {"id": "5.1", "name": "Required Fields", "target": "all JSON objects"},
      {"id": "5.2", "name": "Date Formats", "target": "timestamp fields"},
      {"id": "5.3", "name": "Status Values", "target": "status enums"},
      {"id": "5.4", "name": "ID Format Patterns", "target": "all IDs", "patterns": validation_rules.id_patterns},
      {"id": "5.5", "name": "Schema Validity", "target": "structured-data.json"},
      {"id": "5.6", "name": "Logical Consistency", "target": "timestamps, statuses"}
    ],
    "risk_areas": identify_data_quality_risks()
  },

  "total_checks": count all enabled checks,
  "high_risk_count": count all risk areas,
  "estimated_findings": estimate based on risk_areas
}

Store in qa_findings.attack_plan
</action>
```

### 5. Identify Risk Areas (Helper Functions)

```
<action silent="true">
identify_high_risk_ids():
  - IDs with gaps in sequence
  - High counts (>20 items) that are error-prone
  - Any IDs already flagged in validation.unknowns

identify_sync_risks():
  - Count mismatches between JSON and markdown
  - Missing detail documents
  - References to IDs not in JSON

identify_compliance_gaps():
  - PS# without associated CP#
  - CP# without requirement_ref
  - PP# without severity

identify_data_quality_risks():
  - Empty required fields in JSON
  - Invalid date formats
  - Status values not in enum
</action>
```

### 6. Record Phase Completion

```
<action silent="true">
Add "phase-2-plan" to qa_findings.phases_completed
Set phase_2_end_time = {{timestamp}}
</action>
```

### 7. Auto-Proceed to Next Step

```
<action silent="true">
IMMEDIATELY load, read entire file, then execute {nextStepFile}
DO NOT pause or wait for user input
</action>
```

---

## DATA STRUCTURES CREATED

| Structure | Purpose |
|-----------|---------|
| `qa_findings.metrics` | ID counts, metadata status, ID lists from JSON |
| `qa_findings.main_doc_analysis` | Section analysis, content flags, references |
| `qa_findings.detail_analysis.*` | Entry counts, completeness for each detail doc |
| `qa_findings.attack_plan` | Targeted checks for Step 3 |

---

## SUCCESS CRITERIA (Internal - Not Displayed)

- ✅ Metrics extracted from structured data (if loaded)
- ✅ Main document analyzed (if loaded)
- ✅ Detail documents analyzed (if loaded)
- ✅ Attack plan built with enabled/disabled phases
- ✅ Risk areas identified
- ✅ Auto-proceeded to Step 3

---

## FAILURE MODE

There is no failure that stops execution. Missing data results in disabled check phases, but execution continues.
