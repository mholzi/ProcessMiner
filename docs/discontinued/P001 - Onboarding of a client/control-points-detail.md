# Control Point Details: Onboarding of a client

**Process ID:** P001
**Parent Document:** [As-Is Process Documentation](./as-is-process-documentation.md)
**Last Updated:** 2025-12-03
**Version:** 1.0 (Test Data)

---

## About This Document

This document provides detailed analysis of all control points identified in the Onboarding of a client process. Each control includes regulatory mapping, effectiveness assessment, and compliance analysis.

For summary view, see the [main process documentation](./as-is-process-documentation.md#4-control-points-and-compliance).

---

## Control Point Index

| CP# | Control Name | Type | Regulation | Effectiveness |
|-----|--------------|------|------------|---------------|
| CP-01-001 | KYC Identity Verification | Preventive | AML Directive | Effective |
| CP-01-002 | Sanctions Screening | Detective | OFAC/EU Sanctions | Effective |
| CP-01-003 | Data Consent Capture | Preventive | GDPR | Partially Effective |
| CP-01-004 | High-Risk Client Approval | Preventive | Internal Policy | Effective |

**Statistics:**
- Total Controls: 4
- Preventive: 3
- Detective: 1
- Effective: 3
- Partially Effective: 1

---

## Detailed Control Analysis

### CP-01-001: KYC Identity Verification

**Completeness:** 95% | **Confidence:** HIGH

#### Control Summary

Verify customer identity through document validation and biometric checks before allowing account activation.

#### Control Details

| Attribute | Value |
|-----------|-------|
| **Control Type** | Preventive |
| **Control Owner** | Compliance Team |
| **Regulation** | AML Directive (6AMLD) |
| **Linked Steps** | PS-01-001 (Sign In) |
| **Automation Level** | 80% Automated |

#### Control Description

All new customers must complete identity verification before their account is activated. This includes:
- Document verification (passport, ID card, driving license)
- Biometric face matching (selfie vs document photo)
- Address verification (utility bill, bank statement)
- PEP (Politically Exposed Person) screening
- Adverse media check

#### Verification Method

1. Customer uploads identity documents via mobile app or web
2. Automated OCR extracts document data
3. AI validates document authenticity (checks for tampering)
4. Biometric matching compares selfie to document photo
5. Data cross-referenced with government databases where available
6. Manual review triggered if confidence score < 85%

#### Evidence Captured

- Document images (encrypted storage)
- Biometric confidence score
- Verification timestamp
- Operator ID (for manual reviews)
- Decision rationale

#### Effectiveness Assessment

| Metric | Target | Actual | Status |
|--------|--------|--------|--------|
| False Positive Rate | <5% | 3.2% | Met |
| False Negative Rate | <0.1% | 0.05% | Met |
| Average Processing Time | <2 min | 1.5 min | Met |
| Manual Review Rate | <20% | 18% | Met |

**Overall Effectiveness:** Effective

#### Gaps & Weaknesses

- Document verification less reliable for non-EU documents
- Biometric matching struggles with certain demographics
- Manual review capacity limited during peak periods

#### Improvement Recommendations

1. Expand document template library for non-EU countries
2. Implement bias testing for biometric algorithms
3. Cross-train additional staff for manual reviews

---

### CP-01-002: Sanctions Screening

**Completeness:** 95% | **Confidence:** HIGH

#### Control Summary

Screen all new customers against international sanctions lists before account activation.

#### Control Details

| Attribute | Value |
|-----------|-------|
| **Control Type** | Detective |
| **Control Owner** | Compliance Team |
| **Regulation** | OFAC, EU Sanctions Regulations |
| **Linked Steps** | PS-01-001 (Sign In) |
| **Automation Level** | 95% Automated |

#### Control Description

Real-time screening of customer name and associated entities against:
- OFAC SDN List (US)
- EU Consolidated Sanctions List
- UN Security Council Sanctions
- UK HM Treasury Sanctions
- National PEP databases

#### Verification Method

1. Customer data submitted to sanctions screening engine
2. Fuzzy matching against all configured lists
3. Potential matches reviewed by Compliance
4. True matches escalated to MLRO
5. False positives cleared and documented

#### Evidence Captured

- Screening timestamp
- Lists checked
- Match results (including near-matches)
- Clearance decision and rationale
- Reviewer ID

#### Effectiveness Assessment

| Metric | Target | Actual | Status |
|--------|--------|--------|--------|
| Screening Coverage | 100% | 100% | Met |
| List Update Frequency | Daily | Hourly | Exceeded |
| False Match Rate | <2% | 1.1% | Met |
| True Match Detection | 100% | 100% | Met |

**Overall Effectiveness:** Effective

#### Gaps & Weaknesses

- Name transliteration variations can cause false negatives
- Batch processing for existing customer re-screening has 24h lag

#### Improvement Recommendations

1. Implement phonetic matching for transliteration issues
2. Move to real-time continuous screening

---

### CP-01-003: Data Consent Capture

**Completeness:** 80% | **Confidence:** MEDIUM

#### Control Summary

Capture explicit customer consent for data processing activities as required by GDPR.

#### Control Details

| Attribute | Value |
|-----------|-------|
| **Control Type** | Preventive |
| **Control Owner** | Digital Team / DPO |
| **Regulation** | GDPR Article 6, 7 |
| **Linked Steps** | PS-01-002 (Initial Communications) |
| **Automation Level** | 70% Automated |

#### Control Description

Before sending marketing communications, capture explicit opt-in consent:
- Marketing email consent
- SMS notification consent
- Phone contact consent
- Third-party data sharing consent
- Analytics and profiling consent

#### Verification Method

1. Consent form presented during onboarding flow
2. Customer selects consent options (granular choice)
3. Timestamp and consent version recorded
4. Consent stored in CRM with audit trail
5. Withdrawal mechanism available in customer portal

#### Evidence Captured

- Consent timestamp
- Consent version (form version)
- IP address
- Device fingerprint
- Individual consent selections

#### Effectiveness Assessment

| Metric | Target | Actual | Status |
|--------|--------|--------|--------|
| Consent Capture Rate | 100% | 92% | Not Met |
| Granular Consent | Yes | Partial | Not Met |
| Withdrawal Processing | <24h | <24h | Met |
| Audit Trail Complete | 100% | 100% | Met |

**Overall Effectiveness:** Partially Effective

#### Gaps & Weaknesses

- 8% of customers bypass consent form (technical bug)
- Granular consent options not fully implemented
- Consent version tracking incomplete for legacy customers
- No re-consent mechanism for policy changes

#### Improvement Recommendations

1. Fix consent form bypass bug (CRITICAL)
2. Implement full granular consent options
3. Build re-consent workflow for policy updates
4. Backfill consent records for legacy customers

---

### CP-01-004: High-Risk Client Approval

**Completeness:** 90% | **Confidence:** HIGH

#### Control Summary

Escalate high-risk client onboarding to senior management for approval.

#### Control Details

| Attribute | Value |
|-----------|-------|
| **Control Type** | Preventive |
| **Control Owner** | MLRO / CEO |
| **Regulation** | Internal Risk Policy |
| **Linked Steps** | PS-01-001 (Sign In) |
| **Automation Level** | 50% Automated |

#### Control Description

Clients meeting high-risk criteria require escalated approval:
- Defence sector (NACE code)
- High-risk jurisdictions
- PEP or PEP-related
- Complex ownership structures
- Cash-intensive businesses
- Cryptocurrency-related activities

#### Verification Method

1. Risk scoring engine evaluates client profile
2. High-risk flag triggers workflow pause
3. Enhanced due diligence documentation gathered
4. Compliance Officer reviews and prepares memo
5. MLRO or CEO approval required
6. Decision documented with rationale

#### Evidence Captured

- Risk score and factors
- Enhanced due diligence documents
- Approval memo
- Decision (approve/decline)
- Approver ID and timestamp
- Conditions attached (if any)

#### Effectiveness Assessment

| Metric | Target | Actual | Status |
|--------|--------|--------|--------|
| High-Risk Detection | 100% | 99.5% | Met |
| Approval Turnaround | 5 days | 4 days | Met |
| Documentation Complete | 100% | 98% | Met |
| Post-Approval Monitoring | Yes | Yes | Met |

**Overall Effectiveness:** Effective

#### Gaps & Weaknesses

- Risk scoring model needs annual recalibration
- Some edge cases require manual risk assessment
- Approval process slower for complex cases

#### Improvement Recommendations

1. Annual model validation and recalibration
2. Expand automated risk indicators
3. Create fast-track for lower-complexity high-risk cases

---

## Regulatory Framework Mapping

| Regulation | Controls | Compliance Status | Last Audit | Next Audit |
|------------|----------|-------------------|------------|------------|
| AML Directive (6AMLD) | CP-01-001, CP-01-002 | Compliant | 2024-09-15 | 2025-09-15 |
| GDPR | CP-01-003 | Partially Compliant | 2024-06-01 | 2025-06-01 |
| OFAC Regulations | CP-01-002 | Compliant | 2024-11-01 | 2025-05-01 |
| EU Sanctions | CP-01-002 | Compliant | 2024-11-01 | 2025-05-01 |
| Internal Risk Policy | CP-01-004 | Compliant | 2024-12-01 | 2025-12-01 |

---

## Control Testing Schedule

| CP# | Test Type | Frequency | Last Test | Next Test | Result |
|-----|-----------|-----------|-----------|-----------|--------|
| CP-01-001 | Sample Testing | Quarterly | 2024-10-15 | 2025-01-15 | Pass |
| CP-01-002 | Automated Testing | Daily | 2025-12-03 | Daily | Pass |
| CP-01-003 | Walkthrough | Monthly | 2024-11-15 | 2024-12-15 | Fail |
| CP-01-004 | Sample Testing | Quarterly | 2024-09-30 | 2024-12-31 | Pass |

---

## Change Log

| Date | Contributor | Role | Changes |
|------|-------------|------|---------|
| 2025-12-03 | Markus | CEO | Document initialized |
| 2025-12-03 | Markus | CEO | Added mock test data for all controls |

---

_Generated by ProcessMiner Process Documentation Analyst_
