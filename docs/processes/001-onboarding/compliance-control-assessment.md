# Compliance & Control Assessment: Onboarding

**Document Type:** Regulatory & Control Analysis
**Business Unit:** Corporate Bank
**Region:** Global
**Control Analyst:** Markus
**Date:** 2025-12-09
**Version:** 1.0 (Final)

---

## Executive Summary

The Onboarding process (ONB-001) demonstrates **strong compliance posture** with comprehensive control coverage across all applicable regulations. This assessment evaluated the process against 10 regulatory frameworks, identifying 8 control points that provide effective risk mitigation.

### Key Findings

| Metric | Value | Status |
|--------|-------|--------|
| Regulations Assessed | 10 | 5 fully applicable |
| Controls Mapped | 8 | Full coverage |
| Compliance Gaps | 0 | No critical gaps |
| Average Control Effectiveness | 4.4/5 | Strong |
| Risk Reduction | 64% | Effective |

### Compliance Status

**Fully Compliant:** AMLD 4, AMLD 5, AMLD 6, FATF Recommendations, GDPR

The process has no material compliance gaps. All regulatory requirements have mapped controls with documented evidence and audit trails.

### Risk Profile

| Category | Inherent Risk | Residual Risk | Status |
|----------|---------------|---------------|--------|
| Compliance | High (6.8) | Low (2.8) | Acceptable |
| Fraud | High (8.0) | Low (2.0) | Acceptable |
| Legal | Critical (9.0) | Low (2.0) | Acceptable |

Two risks require ongoing monitoring:
- **RCM-ONB-003:** Hidden beneficial ownership (semi-automated control)
- **RCM-ONB-008:** Data retention compliance (manual process)

### Control Effectiveness

| Rating | Controls | Percentage |
|--------|----------|------------|
| Highly Effective | 5 | 62.5% |
| Effective | 2 | 25.0% |
| Partially Effective | 1 | 12.5% |

One control (CP-ONB-008: Data Retention) requires improvement due to manual execution.

### Regulatory Outlook

Three regulatory changes will impact this process:
- **AMLR (2026-2027):** High impact - EU AML Regulation replacing directives
- **AMLA (2026):** Medium impact - New EU AML supervisor
- **EU AI Act (2025-2026):** Medium impact - Affects automated screening

### Recommendations Summary

| Priority | Count | Key Actions |
|----------|-------|-------------|
| High | 2 | Automate data retention; AMLR readiness |
| Medium | 4 | Consent validation; audit integration; AI Act assessment |
| Low | 1 | Documentation standardisation |

**Quick Wins:** 3 low-effort improvements can be implemented immediately.

### Conclusion

The Onboarding process maintains strong regulatory compliance with effective controls. The recommended improvements focus on automation enhancement and regulatory preparedness rather than gap remediation. The process is well-positioned for TO-BE transformation with a solid compliance foundation.

**Overall Confidence:** HIGH
**Basis:** Systematic analysis with legal review validation

---

## 1. Regulatory Framework Mapping

### 1.1 Applicable Regulations

| REG# | Regulation | Jurisdiction | Applicability | Specific Requirements | Compliance Status |
|------|------------|--------------|---------------|----------------------|-------------------|
| REG-ONB-001 | AMLD 4 (4th Anti-Money Laundering Directive) | EU | Fully applicable | Customer Due Diligence (CDD) requirements; Beneficial ownership identification | Compliant |
| REG-ONB-002 | AMLD 5 (5th Anti-Money Laundering Directive) | EU | Fully applicable | Enhanced CDD for high-risk third countries; Beneficial ownership register access | Compliant |
| REG-ONB-003 | AMLD 6 (6th Anti-Money Laundering Directive) | EU | Fully applicable | Harmonised list of 22 predicate offences | Compliant |
| REG-ONB-004 | MLR 2017 (Money Laundering Regulations) | UK | Reference only | UK AML framework guidance | N/A |
| REG-ONB-005 | JMLSG Guidance | UK | Reference only | UK industry AML guidance | N/A |
| REG-ONB-006 | BSA (Bank Secrecy Act) | US | Reference only | US AML framework guidance | N/A |
| REG-ONB-007 | USA PATRIOT Act | US | Reference only | US anti-terrorism financing guidance | N/A |
| REG-ONB-008 | FinCEN Regulations | US | Reference only | US financial crimes guidance | N/A |
| REG-ONB-009 | FATF Recommendations | Global | Fully applicable | Recommendation 10: Customer Due Diligence; Recommendation 12: Politically Exposed Persons (PEPs) | Compliant |
| REG-ONB-010 | GDPR (General Data Protection Regulation) | EU | Fully applicable | Article 7: Consent requirements | Compliant |

**Summary:**
- **Total Regulations:** 10
- **Fully Applicable:** 5 (AMLD 4, AMLD 5, AMLD 6, FATF, GDPR)
- **Reference Only:** 5 (MLR 2017, JMLSG, BSA, USA PATRIOT Act, FinCEN)

### 1.2 Regional Requirements

No additional regional requirements beyond the core regulations identified above.

### 1.3 Industry Standards

No industry standards (ISO 27001, PCI-DSS, SOC 2, etc.) currently apply to this process.

> **Section Confidence:** HIGH | **Basis:** Legal review

---

## 2. Control Point Inventory

### 2.1 Control Summary

| CP# | Control Name | Type | Automation | Owner | Effectiveness |
|-----|--------------|------|------------|-------|---------------|
| CP-ONB-001 | KYC Defence Industry Screening | PREVENTIVE | Automated | Compliance Officer | HIGH |
| CP-ONB-002 | Customer Identity Verification (CDD) | PREVENTIVE | Automated | Compliance Officer | HIGH |
| CP-ONB-003 | Beneficial Ownership Identification | PREVENTIVE | Semi-Automated | Compliance Officer | MEDIUM |
| CP-ONB-004 | PEP Screening | PREVENTIVE | Automated | Compliance Officer | HIGH |
| CP-ONB-005 | High-Risk Country Screening | PREVENTIVE | Automated | Compliance Officer | HIGH |
| CP-ONB-006 | Data Processing Consent Capture | PREVENTIVE | Automated | Data Protection Officer | HIGH |
| CP-ONB-007 | Communication Opt-In Verification | DETECTIVE | Automated | Marketing Operations | MEDIUM |
| CP-ONB-008 | Customer Data Retention Compliance | PREVENTIVE | Manual | Data Protection Officer | MEDIUM |

**Summary:**
- **Total Controls:** 8
- **Preventive Controls:** 7
- **Detective Controls:** 1
- **Automated:** 5 | **Semi-Automated:** 1 | **Manual:** 2

### 2.2 Control-to-Regulation Mapping

| CP# | Control Name | REG-ONB-001 (AMLD4) | REG-ONB-002 (AMLD5) | REG-ONB-003 (AMLD6) | REG-ONB-009 (FATF) | REG-ONB-010 (GDPR) |
|-----|--------------|---------------------|---------------------|---------------------|--------------------|--------------------|
| CP-ONB-001 | KYC Defence Industry Screening | ✓ | ✓ | ✓ | ✓ | |
| CP-ONB-002 | Customer Identity Verification | ✓ | | | ✓ (R10) | |
| CP-ONB-003 | Beneficial Ownership ID | ✓ | ✓ | | ✓ (R24) | |
| CP-ONB-004 | PEP Screening | | | | ✓ (R12) | |
| CP-ONB-005 | High-Risk Country Screening | | ✓ | | | |
| CP-ONB-006 | Data Processing Consent | | | | | ✓ (Art.7) |
| CP-ONB-007 | Communication Opt-In | | | | | ✓ (Art.7) |
| CP-ONB-008 | Data Retention Compliance | ✓ | | | | ✓ |

### 2.3 Control-to-Process Step Mapping

| CP# | Control Name | PS-001 | PS-002 | PS-003 | PS-004 | PS-005 | PS-006 | PS-007 | PS-008 |
|-----|--------------|--------|--------|--------|--------|--------|--------|--------|--------|
| CP-ONB-001 | KYC Defence Industry Screening | | ✓ | | | | | | |
| CP-ONB-002 | Customer Identity Verification | ✓ | | | | | | | |
| CP-ONB-003 | Beneficial Ownership ID | ✓ | | | | | | | |
| CP-ONB-004 | PEP Screening | ✓ | ✓ | | | | | | |
| CP-ONB-005 | High-Risk Country Screening | ✓ | ✓ | | | | | | |
| CP-ONB-006 | Data Processing Consent | ✓ | | | | | | | |
| CP-ONB-007 | Communication Opt-In | | ✓ | ✓ | | | | | |
| CP-ONB-008 | Data Retention Compliance | | | | | | | | ✓ |

### 2.4 Control Details

#### CP-ONB-001: KYC Defence Industry Screening
- **Type:** PREVENTIVE
- **Description:** Screens new BizBanking customers during activation to identify those in defence industry. Terminates onboarding and sends decline notification when detected.
- **Regulations:** AMLD 4/5/6, FATF
- **Process Steps:** PS-ONB-002
- **How Performed:** Automated KYC screening checks customer industry classification against restricted industries list
- **Owner:** Emma Schultz (Compliance Officer)
- **Effectiveness:** HIGH
- **Evidence:** KYC screening logs, decline notifications

#### CP-ONB-002: Customer Identity Verification (CDD)
- **Type:** PREVENTIVE
- **Description:** Verifies customer identity documents and information before account activation proceeds. Core CDD requirement under AML regulations.
- **Regulations:** AMLD 4 (Art.13), FATF R10
- **Process Steps:** PS-ONB-001
- **How Performed:** Automated document verification via KYC Screening System; ID documents matched against customer-provided information
- **Owner:** Emma Schultz (Compliance Officer)
- **Effectiveness:** HIGH
- **Evidence:** Identity verification records, document images, verification timestamps

#### CP-ONB-003: Beneficial Ownership Identification
- **Type:** PREVENTIVE
- **Description:** Identifies and verifies beneficial owners (>25% ownership) for corporate/business customers. Required for legal persons and arrangements.
- **Regulations:** AMLD 4 (Art.14), AMLD 5, FATF R24
- **Process Steps:** PS-ONB-001
- **How Performed:** Semi-automated - system prompts for BO information; manual review for complex ownership structures
- **Owner:** Emma Schultz (Compliance Officer)
- **Effectiveness:** MEDIUM (complex structures require manual review)
- **Evidence:** BO declaration forms, corporate registry checks, ownership charts

#### CP-ONB-004: PEP Screening
- **Type:** PREVENTIVE
- **Description:** Screens customers and beneficial owners against Politically Exposed Persons databases. Triggers enhanced due diligence when matches found.
- **Regulations:** FATF R12
- **Process Steps:** PS-ONB-001, PS-ONB-002
- **How Performed:** Automated screening against global PEP databases; manual escalation for positive matches
- **Owner:** Emma Schultz (Compliance Officer)
- **Effectiveness:** HIGH
- **Evidence:** PEP screening results, escalation records, EDD documentation

#### CP-ONB-005: High-Risk Country Screening
- **Type:** PREVENTIVE
- **Description:** Screens customers with connections to high-risk third countries (per EU/FATF lists). Triggers enhanced due diligence requirements.
- **Regulations:** AMLD 5
- **Process Steps:** PS-ONB-001, PS-ONB-002
- **How Performed:** Automated country risk screening based on customer nationality, residence, and business operations
- **Owner:** Emma Schultz (Compliance Officer)
- **Effectiveness:** HIGH
- **Evidence:** Country risk screening logs, EDD records for high-risk matches

#### CP-ONB-006: Data Processing Consent Capture
- **Type:** PREVENTIVE
- **Description:** Captures explicit, informed consent for personal data processing at customer sign-in. Ensures lawful basis for data processing under GDPR.
- **Regulations:** GDPR Art.7
- **Process Steps:** PS-ONB-001
- **How Performed:** Automated consent capture integrated into digital sign-in flow; granular consent options presented
- **Owner:** Data Protection Officer
- **Effectiveness:** HIGH
- **Evidence:** Consent records with timestamps, consent text versions, withdrawal logs

#### CP-ONB-007: Communication Opt-In Verification
- **Type:** DETECTIVE
- **Description:** Verifies customer has provided consent before sending marketing/promotional communications. Checks opt-in status before each communication.
- **Regulations:** GDPR Art.7
- **Process Steps:** PS-ONB-002, PS-ONB-003
- **How Performed:** Automated check in Email Marketing Platform against consent database before campaign dispatch
- **Owner:** James Chen (Marketing Operations)
- **Effectiveness:** MEDIUM (depends on consent database accuracy)
- **Evidence:** Communication logs, opt-in verification records, suppression list logs

#### CP-ONB-008: Customer Data Retention Compliance
- **Type:** PREVENTIVE
- **Description:** Ensures customer data is retained per regulatory requirements (5 years for AML) while respecting GDPR data minimisation principles.
- **Regulations:** AMLD 4, GDPR
- **Process Steps:** PS-ONB-008
- **How Performed:** Manual review at journey close-out to ensure retention policies applied; data categorised for appropriate retention periods
- **Owner:** Data Protection Officer
- **Effectiveness:** MEDIUM (manual process)
- **Evidence:** Retention policy documentation, data classification records, deletion logs

### 2.5 Segregation of Duties (SoD) Controls

| Activity | SoD Requirement | Enforcement | Status |
|----------|-----------------|-------------|--------|
| KYC Review & Approval | Four-eyes principle | Automated workflow | ✓ Enforced |

**SoD Notes:**
- KYC screening requires separate maker and checker roles
- System prevents same-person approval
- Automated workflow enforces four-eyes principle

> **Section Confidence:** HIGH | **Basis:** Legal review

---

## 3. Compliance Gap Analysis

### 3.1 Current vs Required

**Regulatory Coverage Assessment:**

| REG# | Regulation | Key Requirements | Controls Mapped | Coverage Status |
|------|------------|------------------|-----------------|-----------------|
| REG-ONB-001 | AMLD 4 | CDD, Beneficial ownership | CP-001, CP-002, CP-003, CP-008 | FULL |
| REG-ONB-002 | AMLD 5 | Enhanced CDD, BO register | CP-001, CP-003, CP-005 | FULL |
| REG-ONB-003 | AMLD 6 | Predicate offences | CP-001 | FULL |
| REG-ONB-009 | FATF | CDD (R10), PEPs (R12) | CP-001, CP-002, CP-003, CP-004 | FULL |
| REG-ONB-010 | GDPR | Consent (Art.7) | CP-006, CP-007, CP-008 | FULL |

**Gap Assessment Result:** No critical compliance gaps identified.

All fully applicable regulations have mapped controls providing adequate coverage.

| Requirement Area | Control Coverage | Gap Status |
|-----------------|------------------|------------|
| Customer Due Diligence | CP-ONB-002 | No Gap |
| Beneficial Ownership | CP-ONB-003 | No Gap |
| PEP Screening | CP-ONB-004 | No Gap |
| High-Risk Country Screening | CP-ONB-005 | No Gap |
| Restricted Industry Screening | CP-ONB-001 | No Gap |
| Data Processing Consent | CP-ONB-006, CP-007 | No Gap |
| Data Retention | CP-ONB-008 | No Gap |

### 3.2 Risk Exposure

**Risk Exposure Summary:**

| Risk Level | Gap Count | Remediation Needed |
|------------|-----------|-------------------|
| Critical | 0 | N/A |
| High | 0 | N/A |
| Medium | 0 | N/A |
| Low | 0 | N/A |

**Total Gaps:** 0
**Highest Risk Level:** N/A

The process has comprehensive control coverage across all applicable regulations. No material compliance gaps exist that require immediate remediation.

### 3.3 Remediation Needs

No remediation required for compliance gaps.

**Improvement Opportunities (Non-Gap):**

| # | Area | Current State | Opportunity | Priority |
|---|------|---------------|-------------|----------|
| IMP-001 | Beneficial Ownership (CP-003) | Semi-automated, MEDIUM effectiveness | Automate complex structure analysis | LOW |
| IMP-002 | Communication Opt-In (CP-007) | MEDIUM effectiveness | Improve consent database accuracy | LOW |
| IMP-003 | Data Retention (CP-008) | Manual process | Automate retention policy enforcement | LOW |

> **Section Confidence:** HIGH | **Basis:** Systematic analysis of regulatory requirements vs control mapping

---

## 4. Control Effectiveness Assessment

### 4.1 Effectiveness Summary

| CEA# | Control | Consistency | Detection | Evidence | Accountability | Timeliness | Score | Rating |
|------|---------|-------------|-----------|----------|----------------|------------|-------|--------|
| CEA-ONB-001 | CP-ONB-001: KYC Defence Industry Screening | 5 | 5 | 5 | 5 | 5 | 5.0 | Highly Effective |
| CEA-ONB-002 | CP-ONB-002: Customer Identity Verification | 5 | 5 | 5 | 5 | 5 | 5.0 | Highly Effective |
| CEA-ONB-003 | CP-ONB-003: Beneficial Ownership ID | 4 | 4 | 4 | 4 | 4 | 4.0 | Effective |
| CEA-ONB-004 | CP-ONB-004: PEP Screening | 5 | 5 | 5 | 5 | 5 | 5.0 | Highly Effective |
| CEA-ONB-005 | CP-ONB-005: High-Risk Country Screening | 5 | 5 | 5 | 5 | 5 | 5.0 | Highly Effective |
| CEA-ONB-006 | CP-ONB-006: Data Processing Consent | 5 | 5 | 5 | 4 | 5 | 4.8 | Highly Effective |
| CEA-ONB-007 | CP-ONB-007: Communication Opt-In | 4 | 3 | 4 | 4 | 5 | 4.0 | Effective |
| CEA-ONB-008 | CP-ONB-008: Data Retention Compliance | 3 | 3 | 3 | 4 | 3 | 3.2 | Partially Effective |

**Rating Distribution:**

| Rating | Count | Percentage |
|--------|-------|------------|
| Highly Effective (4.5-5.0) | 5 | 62.5% |
| Effective (3.5-4.4) | 2 | 25.0% |
| Partially Effective (2.5-3.4) | 1 | 12.5% |
| Ineffective (1.5-2.4) | 0 | 0% |
| Not Operating (1.0-1.4) | 0 | 0% |

**Average Effectiveness Score:** 4.4/5

### 4.2 Control Strengths

| Control | Rating | Key Strength |
|---------|--------|--------------|
| CP-ONB-001 | 5.0 | Fully automated screening with complete audit trail |
| CP-ONB-002 | 5.0 | Automated document verification with timestamp evidence |
| CP-ONB-004 | 5.0 | Real-time PEP database screening with escalation workflow |
| CP-ONB-005 | 5.0 | Automated country risk assessment integrated at onboarding |
| CP-ONB-006 | 4.8 | Granular consent capture embedded in sign-in flow |

**Common Strength Factors:**
- Full automation eliminates human error and inconsistency
- System-enforced execution ensures 100% coverage
- Complete audit trails with timestamps for regulatory evidence
- Clear ownership with defined escalation paths

### 4.3 Control Weaknesses

| Control | Rating | Key Weakness | Root Cause |
|---------|--------|--------------|------------|
| CP-ONB-008 | 3.2 | Inconsistent timing, partial evidence | Manual process dependent on individual compliance |
| CP-ONB-007 | 4.0 | Detection capability limited | Depends on consent database accuracy |
| CP-ONB-003 | 4.0 | Complex structures require manual review | Cannot fully automate BO analysis |

**CP-ONB-008 Weakness Analysis:**
- **Consistency (3):** Manual review at Day 180 sometimes delayed or missed
- **Detection (3):** No automated check for retention policy violations
- **Evidence (3):** Documentation varies by analyst
- **Timeliness (3):** Close-out reviews often batched, causing delays

### 4.4 Improvement Opportunities

| Priority | Control | Improvement | Expected Impact |
|----------|---------|-------------|-----------------|
| 1 | CP-ONB-008 | Automate data retention policy enforcement | Consistency 3→5, Evidence 3→5 |
| 2 | CP-ONB-007 | Implement real-time consent database validation | Detection 3→4 |
| 3 | CP-ONB-003 | Enhance BO analysis automation for common structures | Consistency 4→5 |

> **Section Confidence:** HIGH | **Basis:** Control design analysis and automation level assessment

---

## 5. Audit Trail Requirements

### 5.1 Audit Trail by Control

| ATR# | Control | Data Elements | Retention | Storage | Access | Status |
|------|---------|---------------|-----------|---------|--------|--------|
| ATR-ONB-001 | CP-ONB-001: KYC Defence Screening | Customer ID, industry code, screening result, timestamp, decline reason | 5 years | KYC Screening System | Compliance, Audit, Legal | Complete |
| ATR-ONB-002 | CP-ONB-002: Identity Verification | Customer ID, document type, verification result, document images, timestamp | 5 years | KYC Screening System | Compliance, Audit | Complete |
| ATR-ONB-003 | CP-ONB-003: Beneficial Ownership | Customer ID, BO names, ownership %, verification docs, reviewer ID | 5 years | KYC Screening System | Compliance, Audit | Complete |
| ATR-ONB-004 | CP-ONB-004: PEP Screening | Customer ID, PEP match result, database version, escalation ID | 5 years | KYC Screening System | Compliance, Audit | Complete |
| ATR-ONB-005 | CP-ONB-005: High-Risk Country | Customer ID, country codes, risk score, EDD trigger flag | 5 years | KYC Screening System | Compliance, Audit | Complete |
| ATR-ONB-006 | CP-ONB-006: Data Consent | Customer ID, consent type, consent text version, timestamp, IP address | Duration + 1yr | Consent Management System | DPO, Audit, Legal | Complete |
| ATR-ONB-007 | CP-ONB-007: Communication Opt-In | Customer ID, communication ID, opt-in status check, timestamp | 3 years | Email Marketing Platform | Marketing, Compliance | Partial |
| ATR-ONB-008 | CP-ONB-008: Data Retention | Customer ID, retention category, review date, analyst ID | 5 years | Document Management | DPO, Compliance | Partial |

### 5.2 Retention Requirements by Regulation

| Regulation | Minimum Retention | Applicable Controls |
|------------|-------------------|---------------------|
| AMLD 4/5/6 | 5 years after relationship ends | CP-001, CP-002, CP-003, CP-004, CP-005, CP-008 |
| FATF | 5 years | CP-001, CP-002, CP-003, CP-004, CP-005 |
| GDPR | Duration of processing + 1 year | CP-006, CP-007, CP-008 |

### 5.3 Audit Readiness Assessment

| Readiness Level | Controls | Access Method |
|-----------------|----------|---------------|
| Complete - Self-service | CP-001, CP-002, CP-003, CP-004, CP-005, CP-006 | KYC system audit reports |
| Partial - Manual extraction | CP-007, CP-008 | IT support required |

**Audit Trail Gaps:**
- **ATR-ONB-007:** Communication logs require manual extraction from Email Marketing Platform
- **ATR-ONB-008:** Retention review documentation varies by analyst; no centralised repository

**Recommendations:**
1. Integrate Email Marketing Platform logs into central audit repository
2. Standardise data retention review documentation template
3. Implement automated audit trail extraction for all controls

> **Section Confidence:** HIGH | **Basis:** Regulatory retention requirements and system capability analysis

---

## 6. Risk & Compliance Matrix

### 6.1 Risk Matrix

| RCM# | Risk | Category | Inherent Risk | Regulations | Controls | Residual Risk | Status |
|------|------|----------|---------------|-------------|----------|---------------|--------|
| RCM-ONB-001 | Money Laundering - Restricted Industry | Compliance | High (8) | REG-001, REG-002, REG-003, REG-009 | CP-001 | Low (2) | Acceptable |
| RCM-ONB-002 | Identity Fraud - False ID | Fraud | High (8) | REG-001, REG-009 | CP-002 | Low (2) | Acceptable |
| RCM-ONB-003 | Hidden Beneficial Ownership | Compliance | High (7) | REG-001, REG-002, REG-009 | CP-003 | Medium (4) | Monitor |
| RCM-ONB-004 | PEP Exposure | Compliance | High (8) | REG-009 | CP-004 | Low (2) | Acceptable |
| RCM-ONB-005 | High-Risk Country Exposure | Compliance | High (7) | REG-002 | CP-005 | Low (2) | Acceptable |
| RCM-ONB-006 | Data Privacy Breach - No Consent | Legal | Critical (9) | REG-010 | CP-006 | Low (2) | Acceptable |
| RCM-ONB-007 | Marketing Non-Compliance | Compliance | Medium (5) | REG-010 | CP-007 | Low (3) | Acceptable |
| RCM-ONB-008 | Data Retention Non-Compliance | Compliance | Medium (6) | REG-001, REG-010 | CP-008 | Medium (4) | Monitor |

### 6.2 Risk Summary by Category

| Category | Count | Inherent Avg | Residual Avg | Overall Status |
|----------|-------|--------------|--------------|----------------|
| Compliance | 6 | 6.8 | 2.8 | Acceptable |
| Fraud | 1 | 8.0 | 2.0 | Acceptable |
| Legal | 1 | 9.0 | 2.0 | Acceptable |

### 6.3 Risk Reduction Analysis

| Metric | Value |
|--------|-------|
| Average Inherent Risk | 7.3 |
| Average Residual Risk | 2.6 |
| **Risk Reduction** | **64%** |

### 6.4 Risks Requiring Monitoring

| RCM# | Risk | Residual | Rationale | Action |
|------|------|----------|-----------|--------|
| RCM-ONB-003 | Hidden Beneficial Ownership | Medium (4) | Semi-automated control; complex structures require manual review | Enhance BO automation |
| RCM-ONB-008 | Data Retention Non-Compliance | Medium (4) | Manual process; inconsistent execution | Automate retention enforcement |

### 6.5 Control Coverage Heat Map

| Risk ↓ / Control → | CP-001 | CP-002 | CP-003 | CP-004 | CP-005 | CP-006 | CP-007 | CP-008 |
|--------------------|--------|--------|--------|--------|--------|--------|--------|--------|
| RCM-ONB-001 | ● | | | | | | | |
| RCM-ONB-002 | | ● | | | | | | |
| RCM-ONB-003 | | | ● | | | | | |
| RCM-ONB-004 | | | | ● | | | | |
| RCM-ONB-005 | | | | | ● | | | |
| RCM-ONB-006 | | | | | | ● | | |
| RCM-ONB-007 | | | | | | | ● | |
| RCM-ONB-008 | | | | | | | | ● |

**Legend:** ● = Primary control for risk

> **Section Confidence:** HIGH | **Basis:** Control effectiveness analysis and regulatory mapping

---

## 7. Regulatory Change Impact

### 7.1 Upcoming Regulatory Changes

| RCI# | Regulation | Change Description | Effective Date | Impact | Controls Affected | Status |
|------|------------|-------------------|----------------|--------|-------------------|--------|
| RCI-ONB-001 | AMLD 6 | Enhanced predicate offences harmonisation across EU member states | Jan 2025 | Low | CP-001 | Completed |
| RCI-ONB-002 | AMLR (EU AML Regulation) | Single EU AML Rulebook replacing AMLD directives with directly applicable regulation | 2026-2027 | High | CP-001, CP-002, CP-003, CP-004, CP-005 | Not Started |
| RCI-ONB-003 | AMLA (EU AML Authority) | New EU-level AML supervisor with direct oversight powers | 2026 | Medium | CP-001, CP-002, CP-003, CP-004, CP-005 | Not Started |

### 7.2 Impact Summary

| Impact Level | Count | Action Required |
|--------------|-------|-----------------|
| High | 1 | Major control updates needed |
| Medium | 1 | Some adjustments required |
| Low | 1 | Minor updates only |

### 7.3 Key Change Analysis: AMLR (RCI-ONB-002)

**Background:** The EU is replacing the current directive-based approach (AMLD 4/5/6) with a directly applicable regulation (AMLR), creating a single EU AML Rulebook.

**Expected Changes:**
- Standardised CDD requirements across all EU member states
- Enhanced beneficial ownership transparency requirements
- New requirements for crypto-asset service providers
- Stricter EDD requirements for high-risk third countries
- Cash payment limits

**Impact on Onboarding Controls:**
| Control | Expected Impact | Preparation Needed |
|---------|-----------------|-------------------|
| CP-001 | Update screening criteria | Monitor final text |
| CP-002 | Enhanced CDD procedures | Review ID verification requirements |
| CP-003 | Stricter BO requirements | Prepare for lower thresholds |
| CP-004 | Updated PEP definitions | Review database coverage |
| CP-005 | New high-risk country list | Prepare for list updates |

### 7.4 Horizon Scanning

| Item | Description | Expected Timeline | Potential Impact |
|------|-------------|-------------------|------------------|
| EU AI Act | AI-based KYC/screening systems may require transparency and explainability compliance | 2025-2026 | Medium - affects automated controls CP-001 to CP-005 |
| DORA | Digital Operational Resilience Act - IT resilience requirements for financial services | Jan 2025 | Low - affects KYC system operational resilience |
| eIDAS 2.0 | EU Digital Identity Wallet may change identity verification landscape | 2026+ | Medium - may affect CP-002 identity verification |

### 7.5 Recommended Actions

| Priority | Action | Timeline | Owner |
|----------|--------|----------|-------|
| 1 | Monitor AMLR final text publication | Ongoing | Compliance |
| 2 | Gap analysis against AMLR requirements | Q1 2026 | Compliance |
| 3 | Update control documentation for AMLR | Q2 2026 | Compliance |
| 4 | Assess AI Act impact on automated controls | Q2 2025 | IT/Compliance |

> **Section Confidence:** HIGH | **Basis:** Known EU regulatory pipeline and published timelines

---

## 8. Control Improvement Recommendations

### 8.1 Consolidated Recommendations

| CIR# | Control | Recommendation | Priority | Effort | Expected Benefit |
|------|---------|----------------|----------|--------|------------------|
| CIR-ONB-001 | CP-008 | Automate data retention policy enforcement with system-triggered reviews at Day 180 | High | Medium | Effectiveness 3.2→4.5; eliminate manual inconsistency |
| CIR-ONB-002 | CP-007 | Implement real-time consent database validation before each communication dispatch | Medium | Low | Detection 3→4; reduce marketing compliance risk |
| CIR-ONB-003 | CP-003 | Enhance beneficial ownership automation for common corporate structures (single shareholder, simple hierarchies) | Medium | High | Reduce manual review burden; improve consistency 4→5 |
| CIR-ONB-004 | CP-007 | Integrate Email Marketing Platform logs into central audit repository | Medium | Low | Complete audit trail; enable self-service audit access |
| CIR-ONB-005 | CP-008 | Standardise data retention review documentation template with mandatory fields | Low | Low | Consistent evidence capture; easier audit preparation |
| CIR-ONB-006 | All AML | Prepare AMLR readiness assessment and conduct gap analysis against draft regulation | High | Medium | Regulatory preparedness for 2026-2027 implementation |
| CIR-ONB-007 | CP-001 to CP-005 | Assess EU AI Act impact on automated screening controls; document explainability | Medium | Low | Proactive compliance with AI transparency requirements |

### 8.2 Priority Matrix

| Priority / Effort | Low Effort | Medium Effort | High Effort |
|-------------------|------------|---------------|-------------|
| **High** | | CIR-001, CIR-006 | |
| **Medium** | CIR-002, CIR-004, CIR-007 | | CIR-003 |
| **Low** | CIR-005 | | |

### 8.3 Quick Wins

| CIR# | Recommendation | Impact | Implementation |
|------|----------------|--------|----------------|
| CIR-ONB-002 | Real-time consent validation | Reduce compliance risk | Add validation check to Email Marketing Platform workflow |
| CIR-ONB-004 | Audit log integration | Complete audit trail | Configure log export from Email Marketing Platform |
| CIR-ONB-005 | Documentation template | Consistent evidence | Create standardised review form |

### 8.4 Implementation Roadmap

| Phase | CIR# | Description | Owner | Target |
|-------|------|-------------|-------|--------|
| **Phase 1: Quick Wins** | CIR-002, CIR-004, CIR-005 | Low-effort improvements | Marketing Ops / DPO | Q1 2025 |
| **Phase 2: Core Improvements** | CIR-001 | Data retention automation | IT / DPO | Q2 2025 |
| **Phase 3: Regulatory Prep** | CIR-006, CIR-007 | AMLR and AI Act readiness | Compliance | Q3-Q4 2025 |
| **Phase 4: Enhancement** | CIR-003 | BO automation enhancement | IT / Compliance | 2026 |

### 8.5 Expected Outcomes

| Metric | Current | After Implementation |
|--------|---------|---------------------|
| Average Control Effectiveness | 4.4/5 | 4.7/5 |
| Controls with Complete Audit Trail | 75% | 100% |
| Manual Controls | 2 | 1 |
| Regulatory Readiness | Reactive | Proactive |

> **Section Confidence:** HIGH | **Basis:** Consolidated analysis from Steps 4-8

---

## 9. Document Confidence Summary

| Section | Confidence | Basis |
|---------|------------|-------|
| 1. Regulatory Framework | HIGH | Legal review |
| 2. Control Inventory | HIGH | AI analysis + regulatory mapping |
| 3. Compliance Gaps | HIGH | Systematic requirement-control analysis |
| 4. Control Effectiveness | HIGH | Control design and automation assessment |
| 5. Audit Trail | HIGH | Regulatory retention requirements |
| 6. Risk Matrix | HIGH | Control effectiveness analysis |
| 7. Regulatory Change | HIGH | EU regulatory pipeline |
| 8. Recommendations | HIGH | Consolidated analysis |
| **Overall** | **HIGH** | **Systematic analysis with legal review** |

---

## 10. Traceability Summary

### Regulation → Control Traceability

| REG# | Regulation | Controls Mapped | Coverage |
|------|------------|-----------------|----------|
| REG-ONB-001 | AMLD 4 | CP-001, CP-002, CP-003, CP-008 | 100% |
| REG-ONB-002 | AMLD 5 | CP-001, CP-003, CP-005 | 100% |
| REG-ONB-003 | AMLD 6 | CP-001 | 100% |
| REG-ONB-009 | FATF | CP-001, CP-002, CP-003, CP-004 | 100% |
| REG-ONB-010 | GDPR | CP-006, CP-007, CP-008 | 100% |

### Control → Process Step Traceability

| CP# | Control | Process Steps |
|-----|---------|---------------|
| CP-ONB-001 | KYC Defence Screening | PS-ONB-002 |
| CP-ONB-002 | Identity Verification | PS-ONB-001 |
| CP-ONB-003 | Beneficial Ownership | PS-ONB-001 |
| CP-ONB-004 | PEP Screening | PS-ONB-001, PS-ONB-002 |
| CP-ONB-005 | High-Risk Country | PS-ONB-001, PS-ONB-002 |
| CP-ONB-006 | Data Consent | PS-ONB-001 |
| CP-ONB-007 | Communication Opt-In | PS-ONB-002, PS-ONB-003 |
| CP-ONB-008 | Data Retention | PS-ONB-008 |

### Control → Audit Trail Traceability

| CP# | ATR# | Evidence Status |
|-----|------|-----------------|
| CP-ONB-001 | ATR-ONB-001 | Complete |
| CP-ONB-002 | ATR-ONB-002 | Complete |
| CP-ONB-003 | ATR-ONB-003 | Complete |
| CP-ONB-004 | ATR-ONB-004 | Complete |
| CP-ONB-005 | ATR-ONB-005 | Complete |
| CP-ONB-006 | ATR-ONB-006 | Complete |
| CP-ONB-007 | ATR-ONB-007 | Partial |
| CP-ONB-008 | ATR-ONB-008 | Partial |

---

## Change Log

| Date | Contributor | Role | Changes |
|------|-------------|------|---------|
| 2025-12-09 | Markus | COO | Initial documentation |
| 2025-12-09 | Markus | COO | Completed full compliance analysis: 10 regulations, 8 controls, 8 risks, 7 recommendations |

---

## Companion Documents

| Document | Purpose | Link |
|----------|---------|------|
| AS-IS Process Documentation | Current state process analysis | [as-is-process-documentation.md](./as-is-process-documentation.md) |
| Exception Details | Full exception analysis | [exceptions-detail.md](./exceptions-detail.md) |
| Pain Point Details | Full pain point analysis | [pain-points-detail.md](./pain-points-detail.md) |
| Control Point Details | Full control analysis | [control-points-detail.md](./control-points-detail.md) |

---

_Generated by ProcessMiner Control Analyst_
_Document ID: ONB-001-CCA_
_Analysis Method: Progressive Elicitation with AI-Assisted Assessment_
