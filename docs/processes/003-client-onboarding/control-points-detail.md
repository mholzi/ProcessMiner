# Control Points & Compliance: Client Onboarding

**Process ID:** COB-003
**Document Type:** Control Point Detail Analysis
**Last Updated:** 2025-12-10
**Related Document:** [AS-IS Process Documentation](./as-is-process-documentation.md)

---

## Executive Summary

The BizBanking Client Onboarding process has **16 documented control points** ensuring regulatory compliance across key banking regulations. The control framework is comprehensive, covering AMLD 5/6 requirements for AML/KYC, GDPR for data protection, PSD2 for authentication, and CRD IV/CRR for credit risk management.

The control design follows a preventive-first philosophy with 12 preventive controls and 4 detective controls. Execution is a balanced mix of automated (4), semi-automated (4), and manual (8) controls. The manual control concentration in KYC reflects the judgment required for identity verification and risk assessment.

Overall control effectiveness is HIGH, with no significant compliance breaches in the past 12 months. Internal Audit completed control testing in Q3 2024 with no material findings. Key areas for improvement include increasing automation in document verification and enhancing the welcome call completion rate.

---

## Control Point Summary Table

| CP# | Control Name | Type | Regulation | Process Step | Effectiveness | Owner |
|-----|--------------|------|------------|--------------|---------------|-------|
| CP-COB-001 | Customer Identification | PREVENTIVE | REG-COB-001 | PS-COB-002 | HIGH | KYC Analyst |
| CP-COB-002 | Beneficial Owner Identification | PREVENTIVE | REG-COB-001 | PS-COB-002 | HIGH | KYC Analyst |
| CP-COB-003 | Data Protection Consent | PREVENTIVE | REG-COB-003 | PS-COB-001 | HIGH | Operations Officer |
| CP-COB-004 | Strong Customer Authentication | PREVENTIVE | REG-COB-004 | PS-COB-004 | HIGH | IT/Operations |
| CP-COB-005 | Product Disclosure | PREVENTIVE | REG-COB-006 | PS-COB-005 | MEDIUM | Relationship Manager |
| CP-COB-006 | Document Completeness Check | PREVENTIVE | REG-COB-001, REG-COB-003 | PS-COB-001 | HIGH | Operations Officer |
| CP-COB-007 | PEP & Sanctions Screening | PREVENTIVE | REG-COB-001, REG-COB-002 | PS-COB-002 | HIGH | KYC Analyst |
| CP-COB-008 | Customer Risk Assessment | PREVENTIVE | REG-COB-001 | PS-COB-002 | HIGH | KYC Analyst |
| CP-COB-009 | EDD Escalation | DETECTIVE | REG-COB-001 | PS-COB-002 | HIGH | Compliance Officer |
| CP-COB-010 | Credit Bureau Check | PREVENTIVE | REG-COB-005, REG-COB-006 | PS-COB-003 | HIGH | Credit Analyst |
| CP-COB-011 | Creditworthiness Assessment | PREVENTIVE | REG-COB-005, REG-COB-006 | PS-COB-003 | HIGH | Credit Analyst |
| CP-COB-012 | Credit Approval Authority | PREVENTIVE | REG-COB-005 | PS-COB-003 | HIGH | Credit Manager |
| CP-COB-013 | Account Configuration Verification | DETECTIVE | Internal Policy | PS-COB-004 | MEDIUM | Operations Officer |
| CP-COB-014 | Four-Eyes Account Creation | PREVENTIVE | SoD Policy | PS-COB-004 | HIGH | Team Lead |
| CP-COB-015 | Welcome Call Quality | DETECTIVE | CX Policy | PS-COB-005 | MEDIUM | Relationship Manager |
| CP-COB-016 | Quality Sampling Review | DETECTIVE | QA Policy | PS-COB-006 | HIGH | Team Lead |

---

## Control Statistics

| Metric | Value |
|--------|-------|
| Total Control Points | 16 |
| Regulatory Controls | 12 |
| Internal Policy Controls | 4 |
| Automated Controls | 4 |
| Semi-Automated Controls | 4 |
| Manual Controls | 8 |
| Preventive Controls | 12 |
| Detective Controls | 4 |
| High-Effectiveness Controls | 13 |
| Controls Needing Improvement | 3 |
| Segregation of Duties Controls | 3 |

---

## Regulatory Coverage Matrix

| Regulation | Requirement | Control(s) | Coverage Status |
|------------|-------------|------------|-----------------|
| CDD Regulations 2010 | Customer identity verification | CP-COB-001 | FULL |
| AML Act 2010 | Beneficial owner identification | CP-COB-002 | FULL |
| GDPR | Data processing consent | CP-COB-003 | FULL |
| PSD2 | Strong authentication | CP-COB-004 | FULL |
| Consumer Protection Code | Product disclosure | CP-COB-005 | FULL |

---

## Control Type Breakdown

| Type | Count | Automated | Manual | Effectiveness Avg |
|------|-------|-----------|--------|-------------------|
| Preventive | 5 | 1 | 4 | HIGH |
| Detective | 0 | 0 | 0 | N/A |
| Corrective | 0 | 0 | 0 | N/A |

---

## Detailed Control Point Analysis

### CP-COB-001: Customer Identification

| Attribute | Value |
|-----------|-------|
| **Control ID** | CP-COB-001 |
| **Type** | PREVENTIVE - MANUAL |
| **Regulation** | CDD Regulations 2010 |
| **Process Step** | PS-COB-002: KYC & Identity Verification |
| **Effectiveness** | HIGH — No breaches in 12 months |
| **Owner** | KYC Analyst |

#### Description

All clients must be positively identified using government-issued identification documents before a banking relationship can be established. The KYC Analyst verifies that identification documents are genuine, valid, and match the client's stated identity. This includes validating document features, checking expiry dates, and confirming photographic likeness.

For corporate clients, this extends to verifying the identity of all directors and authorized signatories. The verification is documented in the KYC Platform (Fenergo) with copies of all identity documents retained.

#### Control Activities

- Review government-issued ID (passport, national ID card, driving license)
- Validate document authenticity using UV light and document verification tools
- Confirm document is within validity period
- Match photographic likeness to video call or in-person verification
- Record verification outcome in KYC Platform

#### Testing/Validation Approach

Internal Audit conducts annual testing of KYC files, sampling 10% of onboarded clients to verify identification procedures were followed. Quality Check (PS-COB-006) reviews 20% of cases for compliance. Any failures are reported to Compliance for remediation.

#### Regulatory Requirement Source

CDD Regulations 2010, Section 33: "A designated person shall identify its customer and verify the customer's identity on the basis of documents, data or information obtained from a reliable source which is independent of the customer."

#### Gap Analysis

No significant gaps identified. Current procedures align with regulatory requirements.

#### Improvement Recommendations

- Implement automated document verification using AI/ML to reduce manual effort
- Consider biometric verification for digital channel applications
- Enhance training on detecting fraudulent documents

---

### CP-COB-002: Beneficial Owner Identification

| Attribute | Value |
|-----------|-------|
| **Control ID** | CP-COB-002 |
| **Type** | PREVENTIVE - MANUAL |
| **Regulation** | AML Act 2010 |
| **Process Step** | PS-COB-002: KYC & Identity Verification |
| **Effectiveness** | HIGH — Comprehensive coverage |
| **Owner** | KYC Analyst |

#### Description

For all corporate clients, the bank must identify and verify all Ultimate Beneficial Owners (UBOs) — individuals who ultimately own or control 25% or more of the company. This control prevents the misuse of corporate structures to obscure the identity of those who ultimately benefit from the banking relationship.

The KYC Analyst reviews ownership documentation, traces through corporate layers, and identifies all natural persons meeting the UBO threshold. Each UBO is then subject to the same identification and verification procedures as direct customers.

#### Control Activities

- Review company ownership structure documentation
- Trace ownership through all corporate layers
- Identify all natural persons with 25%+ ownership
- Verify identity of each UBO using standard procedures
- Document ownership structure in KYC Platform

#### Testing/Validation Approach

Annual AML audit includes UBO identification testing. Sample files reviewed to confirm all UBOs correctly identified and verified. Complex structure cases receive enhanced scrutiny.

#### Regulatory Requirement Source

AML Act 2010, Section 25: "A designated person shall take reasonable measures to verify the identity of any beneficial owner so that the designated person is satisfied that it knows who the beneficial owner is."

#### Gap Analysis

Complex multi-layer structures (>3 levels) may not be fully traced in all cases. Exception EX-COB-005 addresses this with Senior KYC Analyst review.

#### Improvement Recommendations

- Implement automated ownership tracing tools
- Subscribe to corporate registry APIs for real-time ownership data
- Develop specialist training for complex structure analysis

---

### CP-COB-003: Data Protection Consent

| Attribute | Value |
|-----------|-------|
| **Control ID** | CP-COB-003 |
| **Type** | PREVENTIVE - MANUAL |
| **Regulation** | GDPR |
| **Process Step** | PS-COB-001: Application Receipt & Initial Triage |
| **Effectiveness** | HIGH — Embedded in application form |
| **Owner** | Operations Officer |

#### Description

Before processing any client application, explicit consent must be obtained for the collection, processing, and storage of personal data. The privacy notice and consent clauses are embedded in the application form, and clients must actively confirm their consent before the application can proceed.

This control ensures the bank has a lawful basis for processing personal data and that clients are informed about how their data will be used, stored, and shared.

#### Control Activities

- Present privacy notice at application submission
- Obtain explicit consent checkbox/signature
- Record consent timestamp and version
- Provide data subject rights information
- Store consent record for audit trail

#### Testing/Validation Approach

Monthly spot checks verify consent is recorded for all new clients. GDPR compliance team conducts quarterly reviews. Data Subject Access Requests (DSARs) are tracked to validate consent records.

#### Regulatory Requirement Source

GDPR Article 6(1)(a): "Processing shall be lawful only if and to the extent that... the data subject has given consent to the processing of his or her personal data for one or more specific purposes."

#### Gap Analysis

No significant gaps. Consent mechanism is robust and auditable.

#### Improvement Recommendations

- Implement granular consent options (marketing vs. essential processing)
- Add consent refresh mechanism for long-term relationships
- Enhance consent withdrawal process

---

### CP-COB-004: Strong Customer Authentication

| Attribute | Value |
|-----------|-------|
| **Control ID** | CP-COB-004 |
| **Type** | PREVENTIVE - AUTOMATED |
| **Regulation** | PSD2 |
| **Process Step** | PS-COB-004: Account Setup & Configuration |
| **Effectiveness** | HIGH — 99.9% system uptime |
| **Owner** | IT/Operations |

#### Description

When setting up online banking access, Strong Customer Authentication (SCA) is enforced requiring at least two of three factors: something the customer knows (password), something the customer has (mobile device), and something the customer is (biometric). This prevents unauthorized access to newly created accounts.

The SCA mechanism is fully automated through the online banking platform, with no manual override capability.

#### Control Activities

- Generate temporary credentials with one-time password
- Require mobile device registration for second factor
- Enforce password complexity requirements
- Validate SCA completion before enabling account access
- Log all authentication events

#### Testing/Validation Approach

Continuous automated monitoring of SCA success/failure rates. Penetration testing annually validates SCA cannot be bypassed. Regulatory reporting on SCA performance submitted quarterly.

#### Regulatory Requirement Source

PSD2 Article 97: "Member States shall ensure that a payment service provider applies strong customer authentication where the payer... accesses its payment account online."

#### Gap Analysis

No gaps identified. Control is fully automated with comprehensive logging.

#### Improvement Recommendations

- Add biometric option for enhanced convenience
- Implement behavioral analytics for risk-based authentication
- Consider passwordless authentication evolution

---

### CP-COB-005: Product Disclosure

| Attribute | Value |
|-----------|-------|
| **Control ID** | CP-COB-005 |
| **Type** | PREVENTIVE - MANUAL |
| **Regulation** | Consumer Protection Code |
| **Process Step** | PS-COB-005: Client Communication & Activation |
| **Effectiveness** | MEDIUM — Manual process with variability |
| **Owner** | Relationship Manager |

#### Description

Before a client begins using their account, they must receive comprehensive disclosure of product terms, fees, and conditions. The Relationship Manager sends the Welcome Pack containing all required disclosure documents and conducts a welcome call to ensure the client understands key terms.

This control ensures clients can make informed decisions about their banking products and are not surprised by fees or conditions.

#### Control Activities

- Generate Welcome Pack with all required disclosures
- Send fee schedule and terms & conditions
- Conduct welcome call covering key product features
- Document call completion and topics covered
- Provide channel for follow-up questions

#### Testing/Validation Approach

Quality Check samples 20% of cases for disclosure completeness. Client complaints related to undisclosed fees are tracked. Annual compliance review of disclosure documents.

#### Regulatory Requirement Source

Consumer Protection Code 2012, Section 4.1: "A regulated entity must ensure that... all information it provides to a consumer is clear, accurate, up to date, and written in plain English."

#### Gap Analysis

Welcome call completion rate is variable (see Pain Point PP-COB-006). Some clients may not receive verbal walkthrough of key terms if call is not completed.

#### Improvement Recommendations

- Create video walkthrough as alternative to live call
- Implement in-app disclosure acknowledgment
- Add automated disclosure tracking in CRM

---

## Control Framework Analysis

### Controls by Risk Level

| Risk Level | Control Count | Gap Count | Coverage |
|------------|---------------|-----------|----------|
| Critical | - | - | - |
| High | - | - | - |
| Medium | - | - | - |
| Low | - | - | - |

### Control Gaps Identified

> *Areas where controls are missing or insufficient*

*[To be completed]*

### Orphan Controls

> *Controls without clear regulatory requirement (potential waste)*

*[To be completed]*

### Uncontrolled Requirements

> *Regulatory requirements without adequate controls (compliance risk)*

*[To be completed]*

---

## Segregation of Duties Matrix

> *Critical for banking compliance - who can do what*

| Function | Maker | Checker | Approver | System Enforced |
|----------|-------|---------|----------|-----------------|
*[To be completed]*

---

## Audit Readiness Assessment

### Audit Trail Completeness

| Process Area | Trail Complete | Trail Partial | Trail Missing |
|--------------|----------------|---------------|---------------|
*[To be completed]*

### Last Audit Findings (if available)

*[To be completed]*

### Remediation Status

*[To be completed]*

---

## Recommendations

### Critical (Compliance Risk)

*[To be completed]*

### High Priority (Control Improvement)

*[To be completed]*

### Medium Priority (Optimization)

*[To be completed]*

---

## Input for Downstream Agents

### For Control Analyst Agent

> *Detailed input for control effectiveness analysis*

*[To be completed]*

### For Transformation Agent

> *Controls that must be preserved/enhanced in TO-BE*

*[To be completed]*

### For IT Architect

> *Control automation opportunities and system requirements*

*[To be completed]*

---

## Regulatory Quick Reference

### Applicable Regulations

| Regulation | Scope | Key Requirements | Controls Mapped |
|------------|-------|------------------|-----------------|
*[To be completed]*

### Upcoming Regulatory Changes

> *Regulations that may impact this process*

*[To be completed]*

---

## Change Log

| Date | Contributor | Role | Changes |
|------|-------------|------|---------|
| 2025-12-09 | Markus | RTM | Initial control point analysis |

---

_Generated by ProcessMiner Process Documentation Analyst_
_Document ID: COB-003-controls_
