# Import Documentation Workflow - Validation Checklist

Use this checklist to verify successful workflow completion and ensure all deliverables meet quality standards.

---

## Pre-Execution Checklist

- [ ] `current_process_folder` variable is set
- [ ] Config file is accessible at `{module_root}/config.yaml`
- [ ] User has source documents ready

---

## Step 1: Document Collection

- [ ] Source documentation folder created at `{current_process_folder}/source-documentation/`
- [ ] All source documents copied/stored with original filenames
- [ ] Document metadata captured (format, original path, stored path)
- [ ] Processing queue populated with all documents
- [ ] User confirmed ready to proceed

**Quality Check:**
- At least one document collected
- All file formats detected correctly
- No documents lost during storage

---

## Step 2: Document Analysis

- [ ] All documents in queue analyzed
- [ ] Process steps extracted with pattern recognition
- [ ] Pain points identified where mentioned
- [ ] Controls extracted with regulatory references
- [ ] Systems and tools identified
- [ ] Roles extracted where mentioned
- [ ] Confidence scores assigned to all elements
- [ ] Source references captured (document, page/section)
- [ ] Per-document summaries displayed
- [ ] Cumulative summary displayed

**Quality Check:**
- All documents processed completely
- Extraction used appropriate keywords
- Confidence scores reflect extraction certainty

---

## Step 3: Data Consolidation

- [ ] All extracted data merged into unified lists
- [ ] Duplicates identified using semantic similarity
- [ ] Duplicates consolidated with all source references preserved
- [ ] Structured IDs assigned (PS-XX-###, PP-XX-###, CP-XX-###, SYS-XX-###)
- [ ] Cross-references built where evident
- [ ] Conflicts documented with source citations
- [ ] Conflicts presented to user for resolution (if any)

**Quality Check:**
- No source references lost during consolidation
- IDs follow structured ID system
- Distinct items not incorrectly merged
- Conflicts flagged, not auto-resolved

---

## Step 4: Gap Analysis

- [ ] Extracted data compared against documentation requirements
- [ ] Process metadata completeness assessed
- [ ] Process steps completeness assessed
- [ ] Pain points completeness assessed
- [ ] Controls completeness assessed
- [ ] Systems completeness assessed
- [ ] Cross-references completeness assessed
- [ ] Completeness score calculated
- [ ] Gap categories populated (complete/partial/missing/unclear)
- [ ] Gap analysis report saved to `{current_process_folder}/gap-analysis.md`

**Quality Check:**
- All requirement categories checked
- Completeness score is accurate
- No false gaps created
- No real gaps missed

---

## Step 5: Structured Output

- [ ] JSON file created at `{current_process_folder}/imported-data.json`
- [ ] import_metadata section populated
- [ ] process_metadata section populated
- [ ] process_steps array populated with all extracted steps
- [ ] pain_points array populated
- [ ] controls array populated
- [ ] systems array populated
- [ ] gaps section populated from gap analysis
- [ ] conflicts section populated
- [ ] All confidence scores included
- [ ] All source references included

**Quality Check:**
- JSON is valid and parseable
- Schema matches specification
- All elements included regardless of confidence
- File saved successfully

---

## Step 6: SME Validation

- [ ] Process steps presented with confidence scores
- [ ] SME validated/corrected process steps
- [ ] Pain points presented (or none confirmed)
- [ ] SME validated/corrected pain points
- [ ] Controls presented (or none confirmed)
- [ ] SME validated/corrected controls
- [ ] Systems presented (or none confirmed)
- [ ] SME validated/corrected systems
- [ ] Gap analysis reviewed with SME
- [ ] All corrections applied to JSON
- [ ] Confidence scores updated to "validated" where applicable
- [ ] Validation metadata added (validator, date, changes)
- [ ] Updated JSON saved

**Quality Check:**
- SME was authority on all corrections
- All changes tracked
- No assumptions made without SME input

---

## Step 7: Integration & Handoff

- [ ] Documentation templates loaded (if available)
- [ ] Templates populated with validated data
- [ ] Confidence indicators applied correctly
- [ ] Missing fields marked `[REQUIRES SME INPUT]`
- [ ] Documentation files saved:
  - [ ] `as-is-process-documentation.md`
  - [ ] `pain-points-detail.md`
  - [ ] `exceptions-detail.md`
  - [ ] `control-points-detail.md`
- [ ] Gap choice handled appropriately (F/L/U)
- [ ] Final summary displayed
- [ ] return_mode handled correctly:
  - [ ] If standalone: [M]/[E] menu shown
  - [ ] If continue_elicitation: Auto-return to calling workflow

**Quality Check:**
- All files saved and accessible
- Handoff information clear
- Downstream workflow can consume output

---

## Final Deliverables Checklist

### Files Created

| File | Path | Status |
|------|------|--------|
| Imported Data JSON | `{current_process_folder}/imported-data.json` | [ ] |
| Gap Analysis Report | `{current_process_folder}/gap-analysis.md` | [ ] |
| Source Documents | `{current_process_folder}/source-documentation/` | [ ] |
| Main Documentation | `{current_process_folder}/as-is-process-documentation.md` | [ ] |
| Pain Points Detail | `{current_process_folder}/pain-points-detail.md` | [ ] |
| Exceptions Detail | `{current_process_folder}/exceptions-detail.md` | [ ] |
| Control Points Detail | `{current_process_folder}/control-points-detail.md` | [ ] |

### Data Quality

- [ ] All extracted items have source references
- [ ] All extracted items have confidence scores
- [ ] All gaps are documented
- [ ] All conflicts are resolved or documented
- [ ] SME validation is complete

### Downstream Readiness

- [ ] JSON schema compatible with start-new-process workflow
- [ ] Documentation ready for SME review
- [ ] Gap list ready for follow-up elicitation
- [ ] All files in expected locations

---

## Workflow Failure Indicators

### Critical Failures (Workflow Invalid)

- Proceeded without collecting documents
- Generated content without source documents
- Auto-resolved conflicts without SME input
- Skipped validation steps
- Did not save required files
- Showed menu when return_mode was set

### Quality Warnings (Review Required)

- Completeness score < 50%
- High number of low-confidence extractions
- Many unresolved conflicts
- Extensive gaps remaining
- SME made significant corrections

---

## Notes

_Use this section to document any issues, special considerations, or follow-up items from the workflow execution._
