# QA Validation Checklist

Process documentation quality assurance checklist for **schema-driven** adversarial review.

---

## Review Information

- **Process:** `_______________`
- **Process ID:** `_______________`
- **Document Type:** `_______________` (as_is_process | compliance_control | cx_journey)
- **Schema Version:** `_______________`
- **Reviewer:** `_______________`
- **Date:** `_______________`

---

## Schema-Driven Validation

This checklist uses validation rules from template schema files:
- `as-is-process-documentation.schema.yaml`
- `compliance-control-assessment.schema.yaml`
- `control-points-detail.schema.yaml`
- `cx-journey-documentation.schema.yaml`

Schema provides: ID patterns, incomplete markers, required references, section definitions, valid values for control types/effectiveness/risk levels.

---

## Phase 1: ID Integrity (Schema-Driven)

| # | Check | Status | Findings |
|---|-------|--------|----------|
| 1.1 | All ID sequences complete (no gaps) - per schema patterns | [ ] | |
| 1.2 | No duplicate IDs - per schema patterns | [ ] | |
| 1.3 | Child items link to valid parent IDs (EX#→PS#, FP#→JT#, etc.) | [ ] | |
| 1.4 | Source attribution present (PP#, FP#) | [ ] | |
| 1.5 | Requirement/regulation tracing (CP#) | [ ] | |
| 1.6 | Reference IDs used (SYS#, CH#) | [ ] | |
| 1.7 | No orphaned IDs in any document | [ ] | |
| 1.8 | IDs in JSON match IDs in markdown (per schema patterns) | [ ] | |

**Phase 1 Total Findings:** `___`

---

## Phase 2: Cross-Document Integrity (Schema-Driven)

| # | Check | Status | Findings |
|---|-------|--------|----------|
| 2.1 | ID counts in JSON match document counts | [ ] | |
| 2.2-2.4 | IDs in JSON exist in detail docs (per schema sync_enabled sections) | [ ] | |
| 2.5 | All cross-references resolve | [ ] | |
| 2.6 | No phantom references (IDs mentioned but not defined) | [ ] | |
| 2.7 | Detail items referenced in main doc (bidirectional) | [ ] | |

**Phase 2 Total Findings:** `___`

---

## Phase 3: Documentation Completeness (Schema-Driven)

| # | Check | Status | Findings |
|---|-------|--------|----------|
| 3.1 | Required sections present (from schema `sections` array) | [ ] | |
| 3.2 | No incomplete markers (from schema `incomplete_markers`) | [ ] | |
| 3.3 | No empty sections (< 50 chars) | [ ] | |
| 3.4 | Required references per section (from schema `required_references`) | [ ] | |
| 3.5 | Confidence meets threshold (from schema `confidence_rules`) | [ ] | |
| 3.6 | Metadata fields populated | [ ] | |

**Incomplete Markers Checked (from schema):**
- [ ] `[TBD]`
- [ ] `[Unknown]`
- [ ] `[TODO]`
- [ ] `{{.*}}`
- [ ] `...`

**Phase 3 Total Findings:** `___`

---

## Phase 4: Compliance Coverage (Schema-Driven)

| # | Check | Status | Findings |
|---|-------|--------|----------|
| 4.1 | Compliance-sensitive steps have control points | [ ] | |
| 4.2 | Control points have regulatory references | [ ] | |
| 4.3 | Risk levels valid (from schema `risk_levels`) | [ ] | |
| 4.4 | Effectiveness ratings valid (from schema `effectiveness_ratings`) | [ ] | |
| 4.5 | Control types valid (from schema `control_types`) | [ ] | |
| 4.6 | Mitigation strategies documented | [ ] | |

**Valid Values (from control-points-detail.schema.yaml):**

*Risk Levels:* Critical, High, Medium, Low

*Effectiveness Ratings:* Highly Effective, Effective, Partially Effective, Ineffective, Not Operating

*Control Types (by purpose):* Preventive, Detective, Corrective

*Control Types (by execution):* Automated, Manual, Semi-Automated

**Phase 4 Total Findings:** `___`

---

## Phase 5: Data Quality (Schema-Driven)

| # | Check | Status | Findings |
|---|-------|--------|----------|
| 5.1 | No null required fields in JSON | [ ] | |
| 5.2 | No empty required sections in MD | [ ] | |
| 5.3 | Date formats valid (ISO 8601) | [ ] | |
| 5.4 | Status values from allowed set | [ ] | |
| 5.5 | ID formats match schema patterns | [ ] | |
| 5.6 | JSON structure valid | [ ] | |
| 5.7 | Timestamps logical (created <= updated) | [ ] | |

**ID Patterns (from schema - varies by document type):**

*as-is-process:* `PS\d{3}`, `EX\d{3}`, `PP\d{3}`, `CP\d{3}`, `SYS\d{3}`

*cx-journey:* `JT\d{3}`, `FP\d{3}`, `CH\d{3}`, `EI\d{3}`

*compliance-control:* `REG\d{3}`, `CP\d{3}`, `GAP\d{3}`, `CEA\d{3}`, `ATR\d{3}`, `RCM\d{3}`, `RCI\d{3}`, `CIR\d{3}`

**Phase 5 Total Findings:** `___`

---

## Summary

| Phase | Checks | Passed | Failed | Findings |
|-------|--------|--------|--------|----------|
| 1. ID Integrity | 8 | | | |
| 2. Cross-Document | 5 | | | |
| 3. Completeness | 6 | | | |
| 4. Compliance | 6 | | | |
| 5. Data Quality | 7 | | | |
| **TOTAL** | **32** | | | |

---

## Validation Source

- [ ] **Schema-driven** - Rules loaded from template schema files
- [ ] **Hardcoded fallback** - Schema not available, using default rules

---

## Assessment

- [ ] **BLOCKED** - Critical issues prevent approval
- [ ] **CONDITIONAL** - Approved with conditions
- [ ] **ACCEPTABLE** - Meets quality standards

---

## Sign-Off

| Role | Name | Date | Signature |
|------|------|------|-----------|
| Reviewer | | | |
| Process Owner | | | |

---

*QA Checklist v2.0 - Schema-Driven Validation - Process Miner Module*
