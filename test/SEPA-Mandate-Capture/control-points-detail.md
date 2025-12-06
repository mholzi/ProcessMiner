# Control Points & Compliance: SEPA Mandate Capture

**Process ID:** P-SEPA-MC-001
**Document Type:** Control Point Detail Analysis
**Last Updated:** 2025-12-04
**Related Document:** [AS-IS Process Documentation](./as-is-process-documentation.md)

---

## Executive Summary

The SEPA Mandate Capture process implements 14 control points designed to ensure regulatory compliance, prevent fraud, maintain data integrity, and provide complete audit trails. The control framework addresses requirements from the SEPA Direct Debit Rulebook, EU Anti-Money Laundering Directive (6AMLD), German banking regulations (MaRisk), and GDPR.

Current control effectiveness is assessed at 82% overall, with 11 controls operating effectively and 3 requiring improvement. The primary gaps relate to external IBAN validation limitations (CP03), quality sampling coverage (CP14), and duplicate detection precision (CP04). The control framework provides strong protection against unauthorized mandate registration and sanctions violations, but opportunities exist to optimize manual control execution and reduce false positives.

Annual control cost is estimated at €145,000 in direct execution effort, with additional €32,000 in control gap remediation activities.

---

## Control Point Summary Table

> **Quick Reference:** All identified control points with compliance mapping at a glance. Click any CP# for full details below.

| CP# | Control Name | Type | Regulation/Policy | Process Step | Effectiveness | Risk Level |
|-----|--------------|------|-------------------|--------------|---------------|------------|
| CP01 | Creditor ID Verification | Preventive | SEPA Rulebook | PS04 | High | High |
| CP02 | IBAN Format Validation | Preventive | ISO 13616 | PS05 | High | Medium |
| CP03 | IBAN Existence Check | Preventive | SEPA Rulebook | PS05 | Medium | Medium |
| CP04 | Duplicate Detection | Detective | Internal Policy | PS07 | Medium | Low |
| CP05 | Sanctions Screening | Preventive | EU AML Directive | PS08 | High | Critical |
| CP06 | Four-Eyes Principle | Preventive | MaRisk | PS09 | High | High |
| CP07 | Signature Validation | Preventive | SEPA Rulebook | PS03 | Medium | High |
| CP08 | Mandate Date Validation | Preventive | SEPA Rulebook | PS06 | High | Low |
| CP09 | UMR Uniqueness | Preventive | SEPA Rulebook | PS06 | High | Medium |
| CP10 | Creditor Limit Check | Preventive | Internal Policy | PS04 | High | Medium |
| CP11 | Audit Trail Logging | Detective | MaRisk | All | High | High |
| CP12 | Daily Reconciliation | Detective | Internal Policy | Post-PS10 | Medium | Medium |
| CP13 | Exception Management | Corrective | Internal Policy | All | Medium | Medium |
| CP14 | Quality Sampling | Detective | Internal Policy | Weekly | Low | Low |

---

## Control Statistics

| Metric | Value |
|--------|-------|
| Total Control Points | 14 |
| Regulatory Controls | 10 |
| Internal Policy Controls | 4 |
| Automated Controls | 8 |
| Manual Controls | 6 |
| High-Effectiveness Controls | 8 |
| Controls Needing Improvement | 3 |
| Segregation of Duties Controls | 1 |

---

## Regulatory Coverage Matrix

> *Mapping of regulations to controls - ensures complete compliance coverage*

| Regulation | Requirement | Control(s) | Coverage Status |
|------------|-------------|------------|-----------------|
| SEPA Core DD Rulebook | Valid Creditor Identifier | CP01 | Full |
| SEPA Core DD Rulebook | Valid IBAN | CP02, CP03 | Partial |
| SEPA Core DD Rulebook | Unique Mandate Reference | CP09 | Full |
| SEPA Core DD Rulebook | Valid Authorization (Signature) | CP07 | Full |
| SEPA Core DD Rulebook | Mandate Date Requirements | CP08 | Full |
| SEPA B2B DD Rulebook | Same as Core + B2B specifics | CP01-CP09 | Full |
| EU 6th AML Directive | Customer Screening | CP05 | Full |
| EU 6th AML Directive | Record Keeping | CP11 | Full |
| MaRisk (Germany) | Dual Control Principle | CP06 | Full |
| MaRisk (Germany) | Audit Trail | CP11 | Full |
| MaRisk (Germany) | Operational Risk Controls | CP13 | Full |
| GDPR | Data Processing Records | CP11 | Full |
| GDPR | Data Minimization | - | Partial |

---

## Control Type Breakdown

| Type | Count | Automated | Manual | Effectiveness Avg |
|------|-------|-----------|--------|-------------------|
| Preventive | 9 | 6 | 3 | 85% |
| Detective | 4 | 2 | 2 | 70% |
| Corrective | 1 | 0 | 1 | 75% |

---

## Detailed Control Point Analysis

### CP01: Creditor ID Verification

#### Overview

| Attribute | Value |
|-----------|-------|
| **Control ID** | CP01 |
| **Control Name** | Creditor ID Verification |
| **Control Type** | Preventive |
| **Category** | Authorization |
| **Process Step(s)** | PS04 |
| **Control Owner** | Payment Operations Manager |
| **Execution** | Automated + Manual Review |
| **Frequency** | Per mandate |
| **Effectiveness Rating** | High (92%) |
| **Last Audit Date** | 2025-09-15 |

#### Control Description

> *What does this control do? What risk does it mitigate?*

Verifies that the Creditor Identifier on the mandate exists in the bank's Creditor Registry, that the creditor is in "Active" status, and that the creditor is authorized to submit the mandate type (Core or B2B). This control prevents mandates from unauthorized or unknown creditors entering the system.

#### Regulatory/Policy Requirement

> *What regulation or policy mandates this control?*

**Regulation/Policy:** SEPA Direct Debit Rulebook (EPC guidance)

**Specific Requirement:** "The Creditor must have a valid Creditor Identifier assigned by a national authority. The Creditor Bank must verify the Creditor has the authority to present Collection transactions."

**Penalty for Non-Compliance:** Scheme suspension, financial penalties, reputational damage

#### Control Objective

> *What is this control designed to achieve?*

Ensure only authorized creditors with valid, active Creditor Identifiers can register mandates. Prevent unauthorized entities from initiating direct debit collections through the bank.

#### Risk Addressed

> *What risk does this control mitigate?*

**Risk Category:** Authorization / Fraud
**Risk Description:** Unauthorized entities registering mandates to fraudulently collect funds from debtors
**Inherent Risk Level:** High
**Residual Risk (with control):** Low

#### Control Activity

> *How is this control performed? Step-by-step.*

1. System extracts Creditor ID from mandate data
2. Automated lookup against Creditor Registry
3. System validates:
   - Creditor ID exists (format and content)
   - Creditor status = "Active"
   - Creditor authorized for mandate type (Core/B2B)
   - Creditor within collection limits
4. If all checks pass: Mandate proceeds to PS05
5. If any check fails: Mandate routed to exception queue (EX01)
6. Manual review confirms system decision for edge cases

#### Timing and Frequency

| Attribute | Value |
|-----------|-------|
| **Frequency** | Per mandate (100%) |
| **Timing** | Real-time at PS04 |
| **Duration** | <2 seconds automated; 4-6 min manual review |
| **Trigger** | Mandate arrival at validation stage |

#### Execution Details

> *Who performs this control and how?*

**Performer:** MMS system (automated), Payment Ops staff (exception review)
**Method:** Database lookup with status validation
**System(s) Used:** Mandate Management System, Creditor Registry, CRM
**Automation Level:** 95% automated, 5% manual exception handling

#### Evidence & Audit Trail

> *What evidence is captured? How is it retained?*

**Evidence Captured:**
- Creditor ID lookup timestamp
- Validation result (pass/fail with reason)
- Staff ID for any manual decisions
- System logs of database queries

**Retention Period:** 10 years (as per mandate retention)

**Storage Location:** MMS audit tables, archived to long-term storage annually

**Audit Trail Quality:** High - complete, timestamped, immutable

#### Effectiveness Assessment

| Criteria | Rating | Notes |
|----------|--------|-------|
| Consistently Performed | High | 100% mandate coverage |
| Exceptions Caught | High | 92% of invalid creditors caught |
| Evidence Quality | High | Complete audit trail |
| Owner Accountability | High | Clear ownership |
| Timely Execution | High | Real-time |
| **Overall Effectiveness** | **High (92%)** | |

#### Control Gaps & Weaknesses

> *What issues exist with this control?*

- 8% of invalid creditors initially pass (caught at later stages)
- Multi-system lookup creates latency (PP04)
- New creditor onboarding delays can cause valid mandates to be rejected
- Creditor limit updates not always timely

#### Segregation of Duties

**SoD Applicable:** No (automated control)
**SoD Enforced:** N/A
**Conflicting Roles:** N/A

#### Improvement Recommendations

1. Single integrated creditor data view to improve accuracy
2. Real-time creditor onboarding status integration
3. Creditor pre-validation at mandate submission point

#### Transformation Considerations

**Non-Negotiable Elements:**
- Every mandate must be validated against authorized creditors
- Creditor ID format and checksum validation
- Active status verification

**Optimization Opportunities:**
- Reduce lookup time through system integration
- Pre-cleared creditor lists for high-volume submitters

**Automation Potential:** Already 95% automated; focus on reducing manual exceptions

---

### CP02: IBAN Format Validation

#### Overview

| Attribute | Value |
|-----------|-------|
| **Control ID** | CP02 |
| **Control Name** | IBAN Format Validation |
| **Control Type** | Preventive |
| **Category** | Data Integrity |
| **Process Step(s)** | PS05 |
| **Control Owner** | Payment Operations Manager |
| **Execution** | Fully Automated |
| **Frequency** | Per mandate |
| **Effectiveness Rating** | High (98%) |
| **Last Audit Date** | 2025-09-15 |

#### Control Description

Validates that the debtor's IBAN conforms to ISO 13616 standard, including correct length for country, valid country code, and correct check digits. This prevents processing of structurally invalid IBANs that would fail in clearing.

#### Regulatory/Policy Requirement

**Regulation/Policy:** ISO 13616, SEPA Rulebook

**Specific Requirement:** "The IBAN must conform to the international standard ISO 13616"

**Penalty for Non-Compliance:** Transaction rejection at clearing, processing fees, client complaints

#### Control Activity

1. System parses IBAN from mandate data
2. Validate country code (ISO 3166-1 alpha-2)
3. Validate length for country (varies by country)
4. Calculate and verify check digits (MOD 97)
5. If valid: Proceed to CP03 (existence check)
6. If invalid: Route to exception queue (EX02)

#### Evidence & Audit Trail

**Evidence Captured:**
- IBAN value submitted
- Validation algorithm result
- Specific failure reason if invalid

**Audit Trail Quality:** High - algorithmic, deterministic, fully logged

#### Effectiveness Assessment

| Criteria | Rating | Notes |
|----------|--------|-------|
| Consistently Performed | High | 100% coverage |
| Exceptions Caught | High | 98% format errors caught |
| Evidence Quality | High | Complete |
| **Overall Effectiveness** | **High (98%)** | |

#### Control Gaps & Weaknesses

- Cannot detect typos that still pass check digit (rare but possible)
- Does not verify account exists (that's CP03)

---

### CP03: IBAN Existence Check

#### Overview

| Attribute | Value |
|-----------|-------|
| **Control ID** | CP03 |
| **Control Name** | IBAN Existence Check |
| **Control Type** | Preventive |
| **Category** | Data Integrity |
| **Process Step(s)** | PS05 |
| **Control Owner** | Payment Operations Manager |
| **Execution** | Automated (internal), Manual (external) |
| **Frequency** | Per mandate |
| **Effectiveness Rating** | Medium (75%) |
| **Last Audit Date** | 2025-09-15 |

#### Control Description

Verifies that the debtor's IBAN corresponds to an actual, active account. For internal accounts (held at the bank), performs real-time Core Banking lookup. For external accounts (other banks), limited to IBAN directory lookup which confirms bank routing but not account existence.

#### Regulatory/Policy Requirement

**Regulation/Policy:** SEPA Rulebook, Internal Policy

**Specific Requirement:** "The Creditor Bank should take reasonable steps to ensure the Debtor Account exists"

**Penalty for Non-Compliance:** R-transactions (returns), fees, client complaints

#### Control Activity

1. Identify if IBAN is internal or external (based on BIC)
2. **Internal IBAN:**
   - Query Core Banking for account existence
   - Verify account status (not closed/blocked)
   - Confirm account type allows direct debits
3. **External IBAN:**
   - Lookup IBAN in external directory
   - Confirm bank/branch exists
   - Cannot verify individual account exists
4. Log validation result
5. If issues: Route to exception handling

#### Effectiveness Assessment

| Criteria | Rating | Notes |
|----------|--------|-------|
| Consistently Performed | High | 100% coverage attempted |
| Exceptions Caught | Medium | Internal: 95%, External: 50% |
| Evidence Quality | Medium | External validation limited |
| **Overall Effectiveness** | **Medium (75%)** | External gap reduces overall |

#### Control Gaps & Weaknesses

- **Critical Gap:** External IBAN existence cannot be verified pre-collection
- ~15% of mandates have external IBANs with 2% return rate from bad accounts
- Industry-wide limitation, not unique to this bank
- No cost-effective solution currently available

#### Improvement Recommendations

1. Third-party IBAN verification service evaluation
2. Risk-based approach: flag external IBANs for enhanced monitoring
3. Monitor EPC's Request-to-Pay initiative for future capabilities

---

### CP04: Duplicate Detection

#### Overview

| Attribute | Value |
|-----------|-------|
| **Control ID** | CP04 |
| **Control Name** | Duplicate Detection |
| **Control Type** | Detective |
| **Category** | Data Integrity |
| **Process Step(s)** | PS07 |
| **Control Owner** | Payment Operations Manager |
| **Execution** | Automated detection, Manual review |
| **Frequency** | Per mandate |
| **Effectiveness Rating** | Medium (70%) |
| **Last Audit Date** | 2025-09-15 |

#### Control Description

Detects potential duplicate mandates by comparing new submissions against existing registered mandates. Uses key fields (Creditor ID + Debtor IBAN + UMR) for exact match detection and fuzzy matching for near-duplicates.

#### Risk Addressed

**Risk Category:** Data Integrity / Fraud
**Risk Description:** Duplicate mandate registration enabling double-charging of debtors
**Inherent Risk Level:** Medium
**Residual Risk (with control):** Low

#### Control Activity

1. System extracts key fields from new mandate
2. Query existing mandates for exact match (Creditor ID + IBAN + UMR)
3. If exact match: Flag as potential duplicate
4. Query for near-matches (fuzzy algorithm)
5. If potential match score >80%: Flag for review
6. Manual review determines: True Duplicate / Amendment / False Positive
7. Log decision and rationale

#### Effectiveness Assessment

| Criteria | Rating | Notes |
|----------|--------|-------|
| Consistently Performed | High | 100% coverage |
| Exceptions Caught | Medium | 70% true positives |
| Evidence Quality | High | Detailed logging |
| **Overall Effectiveness** | **Medium (70%)** | High false positive rate |

#### Control Gaps & Weaknesses

- 30% false positive rate creates manual review burden (PP06)
- SEPA rules allow certain duplicate scenarios (amendments)
- Cannot distinguish amendment from new mandate automatically
- Limited context in review screen

#### Improvement Recommendations

1. Rules engine for auto-resolution of known scenarios
2. Amendment vs new mandate classification
3. Enhanced review screen with historical context

---

### CP05: Sanctions Screening

#### Overview

| Attribute | Value |
|-----------|-------|
| **Control ID** | CP05 |
| **Control Name** | Sanctions Screening |
| **Control Type** | Preventive |
| **Category** | Compliance (AML) |
| **Process Step(s)** | PS08 |
| **Control Owner** | Compliance Manager |
| **Execution** | Automated screening, Manual hit review |
| **Frequency** | Per mandate |
| **Effectiveness Rating** | High (95%) |
| **Last Audit Date** | 2025-09-15 |

#### Control Description

Screens both creditor and debtor against sanctions lists (EU, UN, OFAC) and Politically Exposed Persons (PEP) databases. Any match results in immediate hold and escalation to Compliance for investigation.

#### Regulatory/Policy Requirement

**Regulation/Policy:** EU 6th Anti-Money Laundering Directive, German GwG, OFAC regulations

**Specific Requirement:** "Financial institutions must screen customers against applicable sanctions and PEP lists and report any matches to competent authorities"

**Penalty for Non-Compliance:** Regulatory sanctions (up to €5M or 10% of turnover), criminal prosecution, license revocation

#### Control Activity

1. Extract party names and identifiers from mandate
2. Submit to Sanctions Screening Platform (real-time API)
3. Screen against:
   - EU Consolidated Sanctions List
   - UN Security Council List
   - OFAC SDN List
   - PEP databases
4. If no match: Proceed to PS09
5. If match: Immediate hold, Compliance notification
6. Compliance investigation (see EX04 handling)
7. Document outcome (cleared / escalated / reported)

#### Evidence & Audit Trail

**Evidence Captured:**
- Screening request timestamp
- Lists screened against (with version/date)
- Match details if hit
- Investigation notes and decision
- Approver ID for clearance

**Retention Period:** 10 years (AML record keeping requirement)

**Audit Trail Quality:** High - regulatory requirement for complete records

#### Effectiveness Assessment

| Criteria | Rating | Notes |
|----------|--------|-------|
| Consistently Performed | High | 100% mandates screened |
| Exceptions Caught | High | All true hits escalated |
| Evidence Quality | High | Regulatory-grade audit trail |
| **Overall Effectiveness** | **High (95%)** | |

#### Control Gaps & Weaknesses

- 75% of hits are false positives (name similarity)
- Sequential processing adds 30-60 seconds per mandate (PP07)
- Investigation backlog during high-alert periods

#### Improvement Recommendations

1. Parallel processing during data entry
2. Enhanced fuzzy matching to reduce false positives
3. Pre-cleared creditor list for repeat high-volume clients
4. Real-time Compliance capacity monitoring

---

### CP06: Four-Eyes Principle

#### Overview

| Attribute | Value |
|-----------|-------|
| **Control ID** | CP06 |
| **Control Name** | Four-Eyes Principle |
| **Control Type** | Preventive |
| **Category** | Authorization |
| **Process Step(s)** | PS09 |
| **Control Owner** | Payment Operations Manager |
| **Execution** | Manual |
| **Frequency** | Per mandate |
| **Effectiveness Rating** | High (90%) |
| **Last Audit Date** | 2025-09-15 |

#### Control Description

Requires a second authorized person (approver) to review and approve each mandate registration. The approver must be different from the person who performed data entry. System enforces segregation by blocking same-user approval.

#### Regulatory/Policy Requirement

**Regulation/Policy:** MaRisk (AT 4.3.1), Internal Dual Control Policy

**Specific Requirement:** "For transactions with material risk, dual control (four-eyes principle) must be implemented to prevent errors and fraud"

**Penalty for Non-Compliance:** Regulatory findings, audit qualifications, fraud vulnerability

#### Control Activity

1. Data entry operator completes mandate in MMS
2. Mandate status changes to "Pending Approval"
3. System routes to approval queue
4. Approver (different user) reviews:
   - Key data fields match source document
   - Creditor validation passed
   - Sanctions screening cleared
   - No flags or warnings
5. Approver decision: Approve / Reject (with reason)
6. System validates approver ≠ data entry operator
7. If approved: Mandate proceeds to PS10
8. If rejected: Route to EX05 handling

#### Segregation of Duties

**SoD Applicable:** Yes
**SoD Enforced:** System-enforced
**Conflicting Roles:** Data Entry Operator cannot be Approver for same mandate

#### Effectiveness Assessment

| Criteria | Rating | Notes |
|----------|--------|-------|
| Consistently Performed | High | 100% mandates require approval |
| Exceptions Caught | High | 3% rejection rate (quality control) |
| Evidence Quality | High | Full audit trail |
| **Overall Effectiveness** | **High (90%)** | |

#### Control Gaps & Weaknesses

- Creates processing bottleneck (PP08)
- Limited approver pool causes capacity issues
- Quality of review may decline under time pressure
- No risk-based differentiation (all mandates treated equally)

#### Improvement Recommendations

1. Expand approver pool through training
2. Risk-based approval (auto-approve low-risk mandates)
3. Mobile approval for faster processing
4. Workload balancing across approvers

---

### CP07: Signature Validation

#### Overview

| Attribute | Value |
|-----------|-------|
| **Control ID** | CP07 |
| **Control Name** | Signature Validation |
| **Control Type** | Preventive |
| **Category** | Authorization |
| **Process Step(s)** | PS03 |
| **Control Owner** | Payment Operations Manager |
| **Execution** | Manual (paper), Automated (e-signature) |
| **Frequency** | Per mandate |
| **Effectiveness Rating** | Medium (80%) |
| **Last Audit Date** | 2025-09-15 |

#### Control Description

Verifies that the mandate bears a valid signature from the debtor (or authorized representative for corporate debtors), confirming authorization for direct debit collection. For paper mandates, visual inspection; for digital mandates, e-signature validation.

#### Risk Addressed

**Risk Category:** Authorization / Legal
**Risk Description:** Mandates without valid authorization could result in unauthorized collections, legal liability, and scheme violations
**Inherent Risk Level:** High
**Residual Risk (with control):** Medium

#### Control Activity

1. **Paper Mandates:**
   - Visual inspection of signature field
   - Verify signature present (not blank)
   - Check signature date present
   - For corporate: Verify signatory authority documentation
2. **Digital Mandates:**
   - E-signature certificate validation
   - Timestamp verification
   - Certificate chain validation
3. Log validation result
4. If issues: Route to EX07

#### Effectiveness Assessment

| Criteria | Rating | Notes |
|----------|--------|-------|
| Consistently Performed | Medium | Paper signatures subjective |
| Exceptions Caught | Medium | 80% catch rate for invalid |
| Evidence Quality | Medium | Paper - image only; Digital - certificate |
| **Overall Effectiveness** | **Medium (80%)** | Paper reduces overall |

#### Control Gaps & Weaknesses

- Paper signature validation is subjective
- Cannot verify signature authenticity (just presence)
- Corporate authorization documentation often missing
- No signature comparison database

#### Improvement Recommendations

1. Shift to e-signature mandates (more reliable validation)
2. Enhanced guidance for paper signature review
3. Corporate authorization workflow improvement

---

### CP08 - CP14: Additional Controls

#### CP08: Mandate Date Validation

**Type:** Preventive | **Effectiveness:** High (95%)

Validates mandate signature date is within acceptable range (not future-dated, not expired >12 months). Automated check with clear business rules.

#### CP09: UMR Uniqueness

**Type:** Preventive | **Effectiveness:** High (98%)

Ensures Unique Mandate Reference (UMR) is unique per creditor-debtor pair. System-enforced, aligned with SEPA Rulebook requirements.

#### CP10: Creditor Limit Check

**Type:** Preventive | **Effectiveness:** High (90%)

Verifies creditor has not exceeded collection limits. Automated check against creditor profile. Prevents concentration risk.

#### CP11: Audit Trail Logging

**Type:** Detective | **Effectiveness:** High (99%)

Comprehensive logging of all system actions, user activities, and decisions. Immutable audit trail meeting MaRisk requirements. Foundation for all other controls.

#### CP12: Daily Reconciliation

**Type:** Detective | **Effectiveness:** Medium (75%)

Daily reconciliation of mandates registered vs mandates in source systems. Identifies discrepancies for investigation. Manual process with system support.

**Gap:** Not fully automated, some reconciliation items age without resolution.

#### CP13: Exception Management

**Type:** Corrective | **Effectiveness:** Medium (75%)

Structured exception handling with escalation paths, SLAs, and tracking. Ensures exceptions are resolved appropriately.

**Gap:** Some exceptions lack clear ownership, aging exceptions not actively monitored.

#### CP14: Quality Sampling

**Type:** Detective | **Effectiveness:** Low (60%)

Weekly sampling of processed mandates for quality review. Identifies systematic errors and training needs.

**Gap:** Sample size too small (2%), sampling not statistically designed, results not always actioned.

---

## Control Framework Analysis

### Controls by Risk Level

| Risk Level | Control Count | Gap Count | Coverage |
|------------|---------------|-----------|----------|
| Critical | 1 (CP05) | 0 | 100% |
| High | 4 (CP01, CP06, CP07, CP11) | 1 | 95% |
| Medium | 6 (CP02-CP04, CP09, CP10, CP12) | 2 | 85% |
| Low | 3 (CP08, CP13, CP14) | 1 | 75% |

### Control Gaps Identified

> *Areas where controls are missing or insufficient*

| Gap ID | Description | Risk | Recommendation |
|--------|-------------|------|----------------|
| GAP-01 | External IBAN existence not verifiable | Medium | Third-party service evaluation |
| GAP-02 | High duplicate false positive rate | Low | Rules engine implementation |
| GAP-03 | Quality sampling inadequate | Low | Statistical sampling redesign |
| GAP-04 | Aging exceptions not monitored | Medium | Dashboard with alerting |

### Orphan Controls

> *Controls without clear regulatory requirement (potential waste)*

**CP14 (Quality Sampling):** While valuable, no specific regulation requires this control. However, it supports continuous improvement and should be retained but improved.

### Uncontrolled Requirements

> *Regulatory requirements without adequate controls (compliance risk)*

| Requirement | Regulation | Current Status | Risk |
|-------------|------------|----------------|------|
| GDPR Data Minimization | GDPR Art. 5 | No specific control | Low |
| B2B Mandate Confirmation | SEPA B2B Rules | Manual process | Low |

---

## Segregation of Duties Matrix

> *Critical for banking compliance - who can do what*

| Function | Data Entry | Approver | Manager | Compliance | System Enforced |
|----------|------------|----------|---------|------------|-----------------|
| Mandate Data Entry | ✓ | - | - | - | N/A |
| Mandate Approval | - | ✓ | ✓ | - | Yes |
| Exception Resolution | ✓ | ✓ | ✓ | - | No |
| Sanctions Decision | - | - | - | ✓ | Yes |
| Creditor Setup | - | - | ✓ | - | No |
| Limit Changes | - | - | ✓ | - | Two-approver |

---

## Audit Readiness Assessment

### Audit Trail Completeness

| Process Area | Trail Complete | Trail Partial | Trail Missing |
|--------------|----------------|---------------|---------------|
| Mandate Registration | ✓ | | |
| Exception Handling | | ✓ | |
| Sanctions Screening | ✓ | | |
| Approvals | ✓ | | |
| Client Notifications | | ✓ | |

### Last Audit Findings (2025-09-15)

1. **Finding A-01:** Quality sampling program needs statistical basis - **Status:** In progress
2. **Finding A-02:** Exception aging report not reviewed regularly - **Status:** Closed
3. **Finding A-03:** Creditor limit override documentation incomplete - **Status:** Closed

### Remediation Status

- 2 of 3 findings closed
- Quality sampling improvement planned for Q1 2026
- Overall audit rating: Satisfactory with observations

---

## Recommendations

### Critical (Compliance Risk)

1. **Close External IBAN Gap (CP03):** Evaluate third-party IBAN verification services by Q2 2026
2. **Enhance Sanctions False Positive Management (CP05):** Reduce false positives to <50% through tuning

### High Priority (Control Improvement)

1. **Four-Eyes Optimization (CP06):** Implement risk-based approval without compromising control
2. **Duplicate Detection Enhancement (CP04):** Rules engine for auto-resolution

### Medium Priority (Optimization)

1. **Quality Sampling Redesign (CP14):** Statistical sampling with action tracking
2. **Signature Validation Strengthening (CP07):** Shift to e-signature as default

---

## Input for Downstream Agents

### For Control Analyst Agent

> *Detailed input for control effectiveness analysis*

Focus areas for deep-dive assessment:
- CP03 (IBAN Existence) - external validation gap
- CP04 (Duplicate Detection) - false positive reduction
- CP06 (Four-Eyes) - efficiency vs control trade-off
- CP07 (Signature) - e-signature migration impact

### For Transformation Agent

> *Controls that must be preserved/enhanced in TO-BE*

**Non-Negotiable Controls:**
- CP01 (Creditor Verification) - every mandate
- CP05 (Sanctions Screening) - 100% screening required
- CP06 (Four-Eyes) - dual control principle
- CP11 (Audit Trail) - complete logging

**Controls to Enhance:**
- CP03 - add external IBAN validation
- CP04 - intelligent duplicate handling
- CP07 - e-signature default

### For IT Architect

> *Control automation opportunities and system requirements*

1. **API Integration:** Third-party IBAN validation service
2. **Rules Engine:** Duplicate resolution automation
3. **Mobile Capability:** Approval workflow on mobile
4. **Dashboard:** Real-time control monitoring

---

## Regulatory Quick Reference

### Applicable Regulations

| Regulation | Scope | Key Requirements | Controls Mapped |
|------------|-------|------------------|-----------------|
| SEPA DD Rulebook | Mandate validity | Creditor ID, IBAN, UMR, Signature | CP01-03, CP07-09 |
| EU 6AMLD | AML/CFT | Screening, record keeping | CP05, CP11 |
| MaRisk | Operational risk | Dual control, audit trail | CP06, CP11, CP13 |
| GDPR | Data protection | Processing records | CP11 |

### Upcoming Regulatory Changes

> *Regulations that may impact this process*

1. **Instant SEPA Mandates:** EPC exploring real-time mandate registration - may require <10 second processing
2. **PSD3 Draft:** May increase due diligence requirements for payment initiation
3. **Digital Operational Resilience Act (DORA):** New ICT risk requirements from 2025

---

## Change Log

| Date | Contributor | Role | Changes |
|------|-------------|------|---------|
| 2025-12-04 | ProcessMiner Analyst | Process Documentation Analyst | Initial control point analysis |

---

_Generated by ProcessMiner Process Documentation Analyst_
_Document ID: P-SEPA-MC-001-controls_
