---
name: 'step-03-execute-checks'
description: 'Execute all validation checks systematically - SILENT MODE'

# Path Definitions
module_root: '{project-root}/bmad-custom-modules-src/process-miner'
workflow_path: '{module_root}/workflows/shared/qa-check'

# File References
thisStepFile: '{workflow_path}/steps/step-03-execute-checks.md'
nextStepFile: '{workflow_path}/steps/step-04-summary.md'
workflowFile: '{workflow_path}/workflow.md'

# Execution Mode
execution_mode: silent
---

# Step 3: Execute Adversarial Validation (SILENT)

## STEP GOAL

Execute all validation checks from the attack plan using **schema-driven rules**. Find 3-10 specific issues minimum. Execute silently - no user output.

## EXECUTION MODE: SILENT

**CRITICAL:** This step runs silently.
- NO display output to user
- NO menus or pauses
- Log all findings
- Auto-proceed to summary step when complete

## SCHEMA-DRIVEN VALIDATION

This step uses validation rules loaded in Step 1:
- **ID patterns** from schema (not hardcoded)
- **Incomplete markers** from schema (e.g., [TBD], [TODO])
- **Required references** per section from schema
- **Valid values** for control types, effectiveness ratings, risk levels
- **Section definitions** with sync_enabled flags

Falls back to hardcoded rules if schema not loaded.

---

## MANDATORY EXECUTION RULES:

### Silent Mode Rules:

- 🔇 **NO OUTPUT** - Do not display anything to user
- ⚡ **NO PAUSES** - Do not wait for input
- 📝 **LOG EVERYTHING** - Record all issues as findings
- ➡️ **AUTO-PROCEED** - Immediately load next step when done

### Adversarial Rules:

- 🎯 **MINIMUM 3 FINDINGS** - If fewer found, look harder
- ⚔️ **CHALLENGE EVERYTHING** - Assume errors exist
- 📋 **BE SPECIFIC** - Each finding needs exact location and evidence

### Error Handling:

- If check fails → Create finding for the failure, continue
- If data missing → Skip check, note in findings
- **NEVER STOP** - Always continue to next check

---

## EXECUTION SEQUENCE (SILENT)

### 1. Execute Phase 1: ID Integrity (Schema-Driven)

```
<action silent="true">
IF attack_plan.phase_1_id_integrity.enabled == true:

// Get schema-driven ID patterns
id_patterns = qa_findings.validation_rules.id_patterns
// e.g., { process_step: "PS\\d{3}", exception: "EX\\d{3}", journey_touchpoint: "JT\\d{3}", ... }

**Check 1.1: ID Sequence Integrity (Dynamic per Schema)**
FOR EACH id_type, pattern IN id_patterns:
  - Get ids from metrics.id_lists[id_type] (e.g., ps_ids, ex_ids, jt_ids)
  - IF ids exist and count > 0:
    - Extract numeric portion of each ID using pattern
    - Sort numerically
    - Check for gaps: if [1,2,4,5] → gap at 3
    - Check for duplicates
    - FOR EACH gap or duplicate:
      Add finding:
      {
        "id": "CHK-1.1-{id_type}-{seq}",
        "severity": "HIGH",
        "category": "ID Integrity",
        "phase": 1,
        "check_id": "1.1",
        "title": "{id_type} sequence gap at {number}" OR "Duplicate {id_type} found: {id}",
        "location": "structured-data.json → {collection}",
        "description": "{id_type} ID sequence has gap/duplicate",
        "impact": "May indicate missing items or data corruption",
        "evidence": "IDs found: [{list}], Pattern: {pattern}, Expected: [{expected}]",
        "recommendation": "Review items and renumber or add missing entry"
      }

**Check 1.2: Parent Linkage Validation (Dynamic)**
// Check parent relationships based on document type
IF qa_findings.document_type == "as_is_process":
  // EX# → PS# linkage
  FOR EACH ex_id IN metrics.id_lists.exception:
    - Get parent_step_id from structured_data.process_exceptions[ex_id]
    - Verify parent_step_id exists in metrics.id_lists.process_step
    - IF NOT: Add HIGH finding

ELSE IF qa_findings.document_type == "cx_journey":
  // FP# → JT# linkage (friction points link to journey touchpoints)
  FOR EACH fp_id IN metrics.id_lists.friction_point:
    - Get parent_touchpoint_id from structured_data.friction_points[fp_id]
    - Verify parent exists in metrics.id_lists.journey_touchpoint
    - IF NOT: Add HIGH finding

// Generic parent linkage for any schema-defined relationships
FOR EACH child_type IN schema.child_parent_relationships:
  Validate all linkages exist

**Check 1.3: Source Attribution (PP# or equivalent)**
- For each pain_point/friction_point type ID:
  - Get source_type and source_id
  - Verify both fields exist and are non-empty
  - IF source_id references an ID, verify that ID exists in appropriate list
  - IF missing: Add finding (severity based on what's missing)

**Check 1.4: Requirement/Regulation Tracing (CP# or equivalent)**
- For each control_point type ID:
  - Get requirement_ref or regulation_ref
  - IF both null/empty:
    Add finding:
    {
      "severity": "MEDIUM",
      "title": "Control point lacks regulatory tracing",
      "description": "{cp_id} has no requirement_ref or regulation_ref"
    }

**Check 1.5: Reference Usage Validation (SYS# or equivalent)**
- For each system/channel type ID:
  - Search all primary IDs (PS#, JT#, etc.) for references
  - IF not referenced anywhere:
    Add finding:
    {
      "severity": "LOW",
      "title": "Unused {id_type} documented",
      "description": "{id} is documented but not referenced by any primary item"
    }

**Check 1.6: Orphaned ID Detection**
- Collect all IDs referenced in main_doc_analysis.id_references (using schema patterns)
- Compare against IDs in metrics.id_lists
- FOR EACH ID referenced but not in JSON: Add HIGH finding
- FOR EACH ID in JSON but never referenced: Add LOW finding

**Check 1.7: Cross-ID Consistency**
- Compare IDs in JSON vs IDs in markdown documents
- Use schema patterns for matching
- Flag mismatches

Mark phase_1 complete in qa_findings.phases_completed
</action>
```

### 2. Execute Phase 2: Cross-Document Integrity

```
<action silent="true">
IF attack_plan.phase_2_cross_document.enabled == true:

**Check 2.1: Count Synchronization**
- Compare metrics.id_counts.process_steps vs count of PS# in main document
- Compare metrics.id_counts.exceptions vs count of EX# in exceptions_detail
- Compare metrics.id_counts.pain_points vs count of PP# in pain_points_detail
- Compare metrics.id_counts.controls vs count of CP# in control_points_detail
- FOR EACH mismatch:
  Add finding:
  {
    "severity": "HIGH",
    "title": "Count mismatch: {type}",
    "description": "JSON has {json_count} {type}, document has {doc_count}",
    "evidence": "JSON: {json_count}, Document: {doc_count}, Difference: {diff}"
  }

**Check 2.2-2.4: Detail Document Alignment**
- For each ID type (EX#, PP#, CP#):
  - Get IDs from JSON
  - Search corresponding detail document for each ID
  - FOR EACH ID in JSON not found in detail doc:
    Add finding:
    {
      "severity": "HIGH",
      "title": "Missing detail entry: {id}",
      "description": "{id} exists in structured-data.json but not in {detail_doc}",
      "recommendation": "Add {id} section to {detail_doc}"
    }

**Check 2.5: Reference Resolution**
- For each cross-reference in main_doc_analysis.id_references:
  - Verify the referenced ID exists in appropriate document
  - FOR EACH broken reference:
    Add finding (HIGH severity)

**Check 2.6: Phantom Reference Detection**
- Find IDs mentioned in documents that don't exist in JSON
- FOR EACH phantom:
  Add finding:
  {
    "severity": "HIGH",
    "title": "Phantom reference: {id}",
    "description": "Document references {id} but it doesn't exist in structured data"
  }

**Check 2.7: Bidirectional Link Verification**
- For each item in detail docs, verify it's referenced in main doc
- FOR EACH orphaned detail item:
  Add finding (MEDIUM severity)

Mark phase_2 complete
</action>
```

### 3. Execute Phase 3: Documentation Completeness (Schema-Driven)

```
<action silent="true">
IF attack_plan.phase_3_completeness.enabled == true:

// Get schema-driven rules
validation_rules = qa_findings.validation_rules
incomplete_markers = validation_rules.incomplete_markers
// e.g., ["[TBD]", "[Unknown]", "[TODO]", "{{.*}}", "..."]
required_references = validation_rules.required_references
// e.g., { 2: ["PS#", "SYS#"], 3: ["EX#", "PS#"], ... }
sections_expected = attack_plan.phase_3_completeness.sections_expected
// From schema sections array

**Check 3.1: Required Sections (Schema-Driven)**
- For each section in main_doc_analysis.sections_missing:
  Add finding:
  {
    "severity": "HIGH",
    "title": "Missing required section: {section}",
    "description": "Main document missing '{section}' section (defined in schema)",
    "evidence": "Expected sections from schema: [{sections_expected}]",
    "recommendation": "Add {section} section to {main_document_file}"
  }

**Check 3.2: Incomplete Marker Detection (Schema-Driven)**
// Use markers from schema instead of hardcoded list
- For each marker IN incomplete_markers:
  - Search main document for occurrences
  - For each location found:
    Add finding:
    {
      "severity": "MEDIUM",
      "title": "Incomplete marker found: {marker}",
      "location": "{file}:{section}:{line}",
      "description": "Found '{marker}' indicating incomplete content",
      "evidence": "Context: '{surrounding_context}'",
      "recommendation": "Replace '{marker}' with actual content"
    }

**Check 3.3: Empty Section Detection**
- For each section with < 50 characters:
  Add finding:
  {
    "severity": "MEDIUM",
    "title": "Section has minimal content: {section}",
    "description": "Section '{section}' has only {char_count} characters"
  }

**Check 3.4: Required References by Section (Schema-Driven)**
// Use required_references from schema
- For each section_num, required_ids IN required_references:
  - Check main_doc_analysis.required_references_check[section_num]
  - FOR EACH missing reference type:
    Add finding:
    {
      "severity": "MEDIUM",
      "title": "Missing required reference type in section {section_num}",
      "description": "Section {section_num} should contain {missing_id_type} references per schema",
      "evidence": "Required: [{required_ids}], Found: [{found_ids}]",
      "recommendation": "Add {missing_id_type} references to section {section_num}"
    }

**Check 3.5: Confidence Level Check (Schema Thresholds)**
- Get thresholds from validation_rules.confidence_thresholds
  // e.g., { high: 90, medium: 70 }
- Check metrics.metadata_status.confidence
- IF confidence < medium_threshold:
  Add finding:
  {
    "severity": "MEDIUM",
    "title": "Low confidence level",
    "description": "Process confidence is below {medium_threshold}% threshold (schema-defined)",
    "evidence": "Current confidence: {confidence}%, Threshold: {medium_threshold}%"
  }

**Check 3.6: Metadata Field Check**
- For each false value in metrics.metadata_status:
  Add finding:
  {
    "severity": "MEDIUM",
    "title": "Missing metadata: {field}",
    "description": "Process metadata field '{field}' is not populated"
  }

Mark phase_3 complete
</action>
```

### 4. Execute Phase 4: Compliance Coverage (Schema-Driven)

```
<action silent="true">
IF attack_plan.phase_4_compliance.enabled == true:

// Get schema-driven compliance rules
validation_rules = qa_findings.validation_rules
valid_control_types = validation_rules.control_types
// e.g., { by_purpose: ["Preventive", "Detective", "Corrective"], by_execution: ["Automated", "Manual", "Semi-Automated"] }
valid_effectiveness_ratings = validation_rules.effectiveness_ratings
// e.g., [{ rating: "Highly Effective", score: 5 }, { rating: "Effective", score: 4 }, ...]
valid_risk_levels = validation_rules.risk_levels
// e.g., [{ level: "Critical", score_range: "9-10" }, { level: "High", score_range: "7-8" }, ...]

**Check 4.1: Control Coverage**
- Identify PS# (or JT# for CX) that likely need controls (keywords: approve, verify, check, validate, authorize, sign-off)
- For each identified primary ID:
  - Check if there's a CP# linked to it
  - IF NOT:
    Add finding:
    {
      "severity": "MEDIUM",
      "title": "Potential control gap at {id}",
      "description": "Step {id} ({name}) appears to need a control but none documented"
    }

**Check 4.2: Regulatory Reference Verification**
- For each CP# lacking requirement_ref AND regulation_ref:
  Add finding (already captured in 1.4, skip if duplicate)

**Check 4.3: Risk Level Validation (Schema-Driven)**
// Use valid_risk_levels from schema
- For each CP# with risk_level:
  - Validate risk_level is in valid_risk_levels.map(r => r.level)
  - IF invalid:
    Add finding:
    {
      "severity": "MEDIUM",
      "title": "Invalid risk level for {cp_id}",
      "description": "Risk level '{value}' is not valid per schema",
      "evidence": "Found: '{value}', Valid values: [{valid_risk_levels}]",
      "recommendation": "Use one of: {valid_risk_levels}"
    }
- For each CP# without risk_level: Add MEDIUM finding
- For each PP# without severity: Add MEDIUM finding

**Check 4.4: Effectiveness Rating Validation (Schema-Driven)**
// Use valid_effectiveness_ratings from schema
- For each CP# with effectiveness:
  - Validate effectiveness is in valid_effectiveness_ratings.map(r => r.rating)
  - IF invalid:
    Add finding:
    {
      "severity": "MEDIUM",
      "title": "Invalid effectiveness rating for {cp_id}",
      "description": "Effectiveness '{value}' is not valid per schema",
      "evidence": "Found: '{value}', Valid values: [{valid_ratings}]",
      "recommendation": "Use one of: {valid_ratings}"
    }

**Check 4.5: Control Type Validation (Schema-Driven)**
// Use valid_control_types from schema
- For each CP# with control_type:
  - Validate control_type is in valid_control_types (by_purpose + by_execution)
  - IF invalid:
    Add finding:
    {
      "severity": "LOW",
      "title": "Non-standard control type for {cp_id}",
      "description": "Control type '{value}' is not in schema-defined list",
      "evidence": "Found: '{value}', Valid values: [{valid_types}]"
    }

**Check 4.6: Mitigation Documentation**
- For each PP#:
  - Check if mitigation/resolution field exists
  - IF missing:
    Add finding:
    {
      "severity": "LOW",
      "title": "Pain point lacks mitigation: {pp_id}",
      "description": "Pain point {pp_id} has no documented mitigation strategy"
    }

Mark phase_4 complete
</action>
```

### 5. Execute Phase 5: Data Quality (Schema-Driven)

```
<action silent="true">
IF attack_plan.phase_5_data_quality.enabled == true:

// Get schema-driven ID patterns
validation_rules = qa_findings.validation_rules
id_patterns = validation_rules.id_patterns
// e.g., { process_step: "PS\\d{3}", exception: "EX\\d{3}", journey_touchpoint: "JT\\d{3}", ... }

**Check 5.1: Required Field Population**
- For each object in structured_data:
  - Check required fields based on object type
  - FOR EACH null/empty required field:
    Add finding:
    {
      "severity": "HIGH" if critical field else "MEDIUM",
      "title": "Empty required field: {object}.{field}",
      "location": "structured-data.json → {path}",
      "description": "Required field '{field}' is null or empty"
    }

**Check 5.2: Date Format Validation**
- For each date/timestamp field:
  - Validate ISO 8601 format
  - FOR EACH invalid:
    Add finding (MEDIUM)

**Check 5.3: Status Value Validation**
- Check validation.status is in [DRAFT, IN_PROGRESS, REVIEW, APPROVED, ARCHIVED]
- Check other status fields against their enums
- FOR EACH invalid:
  Add finding (MEDIUM)

**Check 5.4: ID Format Pattern Validation (Schema-Driven)**
// Use id_patterns from schema - supports dynamic ID types
FOR EACH id_type, pattern IN id_patterns:
  - Get all IDs of this type from structured data
  - Verify each ID matches pattern regex
  - FOR EACH invalid:
    Add finding:
    {
      "severity": "LOW",
      "title": "Invalid {id_type} format: {id}",
      "description": "ID '{id}' does not match expected pattern",
      "evidence": "Found: '{id}', Expected pattern: {pattern}",
      "recommendation": "Rename to match pattern (e.g., {example_valid_id})"
    }

// Example patterns from schemas:
// as-is-process: PS\d{3}, EX\d{3}, PP\d{3}, CP\d{3}, SYS\d{3}
// cx-journey: JT\d{3}, FP\d{3}, CH\d{3}, EI\d{3}
// compliance-control: REG\d{3}, CP\d{3}, GAP\d{3}, CEA\d{3}, ATR\d{3}, RCM\d{3}, RCI\d{3}, CIR\d{3}

**Check 5.5: Schema Structure Validation**
- Verify JSON has expected structure
- (Already done in Step 1, reference those findings)

**Check 5.6: Logical Consistency**
- Verify session.started <= session.last_updated
- Verify checkpoint.step is valid step number
- FOR EACH inconsistency:
  Add finding (MEDIUM)

Mark phase_5 complete
</action>
```

### 6. Verify Minimum Threshold

```
<action silent="true">
total_findings = qa_findings.findings.length

IF total_findings < 3:
  // Need to look deeper - execute additional checks

  **Additional Check A: Content Quality**
  - Search for vague language: "some", "various", "etc.", "and so on"
  - Search for weak descriptions < 20 words
  - FOR EACH found:
    Add finding (LOW)

  **Additional Check B: Terminology Consistency**
  - Check if same concept uses different terms
  - FOR EACH inconsistency:
    Add finding (LOW)

  **Additional Check C: Cross-Reference Completeness**
  - Check if all relationships are bidirectional
  - FOR EACH one-way reference:
    Add finding (LOW)

  // Recount
  total_findings = qa_findings.findings.length

  IF total_findings < 3:
    // Add meta-finding
    Add finding:
    {
      "severity": "LOW",
      "title": "Documentation is unusually clean",
      "description": "Fewer than 3 issues found. Either documentation is excellent or review was insufficient."
    }
</action>
```

### 7. Calculate Summary Statistics

```
<action silent="true">
Update qa_findings.summary:
{
  "critical": count findings where severity == "CRITICAL",
  "high": count findings where severity == "HIGH",
  "medium": count findings where severity == "MEDIUM",
  "low": count findings where severity == "LOW",
  "total": qa_findings.findings.length,

  "by_phase": {
    "phase_1": count findings where phase == 1,
    "phase_2": count findings where phase == 2,
    "phase_3": count findings where phase == 3,
    "phase_4": count findings where phase == 4,
    "phase_5": count findings where phase == 5,
    "init": count findings where phase == "init",
    "additional": count findings where phase == "additional"
  },

  "by_category": {
    // Group by finding.category
  }
}

// Determine assessment
IF qa_findings.summary.critical > 0:
  qa_findings.assessment = "BLOCKED"
ELSE IF qa_findings.summary.high > 0:
  qa_findings.assessment = "CONDITIONAL"
ELSE:
  qa_findings.assessment = "ACCEPTABLE"
</action>
```

### 8. Record Completion

```
<action silent="true">
qa_findings.session.status = "COMPLETE"
qa_findings.session.completed = {{timestamp}}
qa_findings.phases_completed = ["init", "plan", "phase_1", "phase_2", "phase_3", "phase_4", "phase_5", "summary"]
</action>
```

### 9. Auto-Proceed to Summary Step

```
<action silent="true">
IMMEDIATELY load, read entire file, then execute {nextStepFile}
DO NOT pause or wait for user input
</action>
```

---

## FINDINGS STRUCTURE

Each finding follows this structure:
```json
{
  "id": "CHK-{phase}.{check}-{seq}",
  "severity": "CRITICAL|HIGH|MEDIUM|LOW",
  "category": "Category Name",
  "phase": 1-5 or "init" or "additional",
  "check_id": "1.1",
  "title": "Short descriptive title",
  "location": "file → path → element",
  "description": "Detailed description of issue",
  "impact": "Why this matters",
  "evidence": "Specific data proving the issue",
  "recommendation": "How to fix it",
  "schema_source": "schema" or "hardcoded_fallback"  // NEW: indicates rule source
}
```

---

## SUCCESS CRITERIA (Internal - Not Displayed)

- ✅ All enabled phases executed
- ✅ Minimum 3 findings identified
- ✅ Each finding has complete details
- ✅ Summary statistics calculated
- ✅ Assessment determined
- ✅ Auto-proceeded to Step 4 (Summary)

---

## FAILURE MODE

There is no failure that stops execution. ALL errors become findings and execution continues.
